# Guide: Organisational RFCs in Practice

## From internet protocols to business protocols

The internet RFC model translates directly to internal organisational specifications.

What's needed is a simple template that allows organisations to document their domain knowledge in a way that:

- Remains stable across technology changes
- Can be implemented multiple ways
- Is the source of truth
- Can be versioned and evolved
- Is accessible to both humans and AI

## The organisational RFC template

### RFC-001: Appointment Scheduling Protocol

**Title:** Appointment Scheduling Protocol

**Date:** 2024-07-25

**Status:** Active

**Authors:** Product Team, Clinical Operations

---

## 1. Overview

This RFC specifies the business protocol for scheduling patient appointments in a healthcare clinic. This protocol must be implemented by any system managing appointment booking, whether online, phone-based, or in-person. This specification is independent of technology choices, deployment architecture, or data storage mechanisms.

Different implementations may be built in different languages, frameworks, or platforms. All must conform to this protocol.

## 2. Scope

**In Scope:**
- Patient-initiated appointment booking
- Staff-initiated appointment creation
- Appointment cancellation and rescheduling
- Doctor availability management
- Conflict resolution

**Out of Scope:**
- Patient medical records
- Billing and insurance
- Telemedicine functionality
- Medical imaging systems

## 3. Core Entities

This section defines the entities (message types) that participate in the protocol.

### 3.1 Patient

Represents a person seeking medical care.

**Attributes:**
- `patient_id` (unique identifier)
- `name` (string)
- `email` (string, must be valid email format)
- `phone` (string, must be valid phone format)
- `date_of_birth` (date)
- `medical_record_number` (unique)
- `registration_date` (timestamp)

**Constraints:**
- `email` must follow RFC 5322
- `phone` must be in E.164 format
- `date_of_birth` must be in the past
- `medical_record_number` must be unique across all patients
- Once set, `patient_id` is immutable

### 3.2 Doctor

Represents a medical professional available for appointments.

**Attributes:**
- `doctor_id` (unique identifier)
- `name` (string)
- `speciality` (enumeration: Cardiology, Dermatology, Neurology, etc.)
- `office_location` (string)
- `years_of_experience` (integer, >= 0)

**Constraints:**
- `speciality` must be from the approved enumeration
- `years_of_experience` must be non-negative
- `office_location` must reference a valid Clinic

### 3.3 Appointment

Represents a scheduled interaction between a Patient and Doctor.

**Attributes:**
- `appointment_id` (unique identifier)
- `patient_id` (reference to Patient)
- `doctor_id` (reference to Doctor)
- `appointment_date` (date)
- `appointment_start_time` (time)
- `appointment_duration_minutes` (integer)
- `status` (enumeration: Scheduled, Completed, Cancelled, NoShow, Rescheduled)
- `reason_for_visit` (string)
- `created_timestamp` (timestamp)
- `created_by_actor` (enumeration: Patient, Staff)

**Constraints:**
- `appointment_date` must be in the future at creation time
- `appointment_date` must not be more than 90 days in the future
- `appointment_date` must be within clinic business days (Monday-Friday)
- `appointment_start_time` must be within clinic business hours (08:00-17:00)
- `appointment_start_time` must be at a 15-minute interval boundary (00, 15, 30, 45)
- `appointment_duration_minutes` must be 15, 30, 45, or 60
- No two appointments for the same Doctor can overlap
- `reason_for_visit` must not be empty

### 3.4 TimeSlot

Represents a specific 15-minute window in a doctor's availability.

**Attributes:**
- `timeslot_id` (unique identifier)
- `doctor_id` (reference to Doctor)
- `date` (date)
- `start_time` (time)
- `end_time` (time)
- `status` (enumeration: Available, Reserved, Unavailable)

**Constraints:**
- `date` must be a business day
- `start_time` must be within clinic business hours
- `end_time` must be exactly 15 minutes after `start_time`
- A TimeSlot can only transition from Available → Reserved → (Completed or Cancelled)
- A TimeSlot cannot transition backwards

## 4. Protocol Messages

This section defines valid interactions and state transitions.

### 4.1 RequestScheduleAppointment

A patient or staff member requests to schedule an appointment.

**Initiator:** Patient or Staff Member

**Parameters:**
- `patient_id` (required)
- `doctor_id` (required)
- `preferred_date_range_start` (required, must be today or later)
- `preferred_date_range_end` (required, must be <= 90 days from today)

**Preconditions:**
- Patient with `patient_id` must exist and be registered
- Doctor with `doctor_id` must exist and accept appointments
- Request must arrive before system cutoff (18:00)

**Response: AppointmentScheduled (Success Case)**

**Attributes:**
- `appointment_id` (newly created)
- `appointment_date` and `appointment_start_time`
- `confirmation_number`
- `estimated_delivery_time_for_confirmation_email` (should be within 60 seconds)

**Response: NoAvailableSlots (Alternative Case)**

**Attributes:**
- `doctor_id` (who is not available)
- `requested_date_range`
- `suggested_alternatives` (list of other doctors with availability or future dates when this doctor is available)

**Response: ValidationError (Error Case)**

**Attributes:**
- `error_code` (specific validation failure)
- `error_message` (human-readable)

### 4.2 ReservationRaceCondition

**Problem:** Between the time the patient selected a slot and confirmed the booking, another patient reserved that slot.

**Solution:**
1. System checks availability again immediately before creating appointment
2. If slot is taken, return NoAvailableSlots with the next available slots
3. Patient may select a new time
4. No appointment is created in the database

This must be handled atomically, with the appointment either fully created or not created at all. No partial states.

### 4.3 CancelAppointment

A patient cancels an existing appointment.

**Initiator:** Patient

**Parameters:**
- `appointment_id` (required)

**Preconditions:**
- Appointment must exist and be in Scheduled status
- Appointment must be at least 24 hours in the future
- Request must come from the patient who created the appointment (or staff on their behalf)

**Response: AppointmentCancelled (Success Case)**

**Attributes:**
- `appointment_id`
- `cancellation_timestamp`
- `confirmation_that_notification_sent` (patient should receive email within 60 seconds)

**Response: TooLateToCancel (Error Case)**

**Attributes:**
- `appointment_id`
- `appointment_date_time`
- `hours_until_appointment`
- `message` (explaining that cancellations require 24-hour notice)

## 5. Data Consistency Rules

These rules must be maintained by any implementation.

**Rule 5.1: Appointment-TimeSlot Consistency**

For every Scheduled appointment, exactly one TimeSlot with status Reserved must exist for the same doctor, date, and time.

**Rule 5.2: Patient Uniqueness**

A patient cannot have two Scheduled appointments at the same time.

**Rule 5.3: Doctor Capacity**

A doctor cannot have more than one appointment in any given TimeSlot.

**Rule 5.4: Immutable History**

Once an appointment is Completed or Cancelled, its attributes (except status) cannot be changed. These are historical records.

**Rule 5.5: Temporal Consistency**

`appointment_date` must always be >= `created_date`. You cannot schedule an appointment in the past.

## 6. Notifications

When specific events occur, notifications must be sent within specified timeframes.

**Event: Appointment Created**
- **To:** Patient via email
- **Contains:** appointment details, confirmation number, cancellation instructions, reminder about 24-hour cancellation requirement
- **Delivery SLA:** Within 60 seconds

**Event: Appointment Cancelled**
- **To:** Patient via email
- **Contains:** appointment details, cancellation timestamp, confirmation that time slot is now available
- **Delivery SLA:** Within 60 seconds

**Event: Appointment Reminder**
- **Timing:** 24 hours before appointment
- **To:** Patient via email
- **Contains:** appointment details, how to reschedule or cancel
- **Delivery SLA:** Within 1 hour of the 24-hour mark

**Event: Appointment Completed**
- **To:** Patient via email (optional based on clinic policy)
- **Contains:** appointment summary, instructions for next steps

## 7. Enumeration Values

### Speciality Values
- Cardiology
- Dermatology
- Endocrinology
- Gastroenterology
- Neurology
- Orthopedics
- Psychiatry
- Urology

### Appointment status values
- `Scheduled`: Appointment is confirmed and waiting
- `Completed`: Appointment occurred
- `Cancelled`: Patient or staff cancelled the appointment
- `NoShow`: Patient did not arrive
- `Rescheduled`: Patient rescheduled to a different time

### TimeSlot Status Values
- `Available`: Open for booking
- `Reserved`: Appointment created for this slot
- `Unavailable`: Doctor unavailable (vacation, conference, etc.)

## 8. Business Rules

These are domain rules that govern behaviour.

**Rule 8.1: Maximum Advance Booking**

Appointments cannot be scheduled more than 90 days in advance. This is because doctor schedules are only confirmed 90 days out.

**Rule 8.2: Minimum Advance Notice for Cancellation**

Patients must provide at least 24 hours notice to cancel. This allows the clinic time to offer the slot to other patients.

**Rule 8.3: Business Hours Only**

Appointments can only occur between 08:00 and 17:00, Monday through Friday.

**Rule 8.4: 15-Minute Slots**

All appointments must align to 15-minute boundaries. Appointments cannot be 7 minutes or 22 minutes. This simplifies scheduling and reduces fragmentation.

**Rule 8.5: Doctor Speciality Matching**

The system should not prevent a patient from booking any doctor, but the UI may filter by speciality or suggest appropriate specialists.

**Rule 8.6: No Double-Booking**

No two appointments for the same doctor can overlap. This is a hard constraint enforced at the database level.

## 9. Implementation Notes

This section provides guidance for implementers without mandating specific technologies.

### 9.1 Persistence

Implementations must persist all state changes. They may use:
- Relational databases (PostgreSQL, MySQL, Oracle)
- Document stores (MongoDB, Firestore)
- Graph databases (Neo4j)
- Event stores

The choice does not affect protocol compliance. The important thing is that state is maintained correctly according to the constraints above.

### 9.2 Atomicity

The "create appointment" operation must be atomic: either the appointment is fully created with a TimeSlot reserved, or neither is created. Partial states must not be possible.

Most database systems support transactions sufficient for this.

### 9.3 Idempotency

Notification systems should be idempotent. Sending the same notification twice is acceptable. Missing a notification is not.

### 9.4 Clock Skew

If multiple servers exist, use a time service (NTP) to ensure clocks are synchronized. The 24-hour cancellation rule and reminder timing depend on accurate time.

### 9.5 Testing

All implementations should test:
- Valid appointment creation
- Rejection of appointments outside business hours
- Rejection of appointments > 90 days in advance
- Handling of race conditions (two simultaneous bookings for the same slot)
- Cancellation within and outside the 24-hour window
- Database consistency after failures

## 10. Versioning

This protocol is versioned. When changes occur, they are tracked.

**Version 1.0:** Initial specification
- Basic scheduling for single doctor per clinic
- Email notifications only

**Future Version 1.1 (Proposed):**
- Multiple clinic support
- SMS notifications
- Recurring appointments
- Group appointments

Implementations must document which protocol version they support.

## 11. References

- RFC 5322 (Internet Message Format)
- RFC 3339 (Date and Time on the Internet)
- ISO 8601 (Date and Time Format)
- Healthcare privacy regulations applicable to clinic's jurisdiction

---

## Why this matters

This specification is the source of truth.

A new team can implement appointment scheduling in Go. Another team implements it in Python. A third team rebuilds it in Rust.

All three systems interoperate with each other and with legacy systems, not through code sharing, but through protocol compliance.

When the clinic decides to add SMS reminders, the specification is updated (version 1.1). All implementations update to the new version, with none left tied to the old technology stack.

When the clinic needs to move to a new cloud provider, the application can be reimplemented on new infrastructure. The protocol remains the same, and patients experience no change.

The knowledge of "how appointment scheduling works" is now an organisational asset, not a software artifact.

It is durable, implementable, and testable. It is an RFC.
