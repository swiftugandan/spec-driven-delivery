# Chapter 5: Bringing It Together

The complete specification layer

> A complete specification needs many pieces. Each piece answers a different question.

## The specification stack

We have now explored four layers of specification.

**Vision:** Why does this system exist?

**Requirements:** What specific observable behaviours must it have?

**Use Cases:** What are the complete interactions users perform?

**Domain Model:** What entities and relationships exist in the business?

Each layer is necessary, each answers a different question, and together they form a complete specification.

Let us see how they fit together.

## A complete example

Imagine a software team tasked with building an online appointment scheduling system for a clinic.

### Layer 1: Vision

The team begins by understanding why.

> Our clinic receives thirty appointment calls daily. Receptionists spend two hours per day on the phone. This diverts them from other important tasks. Patients often reach a busy signal. Working patients cannot call during business hours, so many book appointments in person, which wastes time. By allowing online appointment booking, we expect to reduce phone call volume by sixty percent, improve patient satisfaction, and reduce staff burden.

This vision is clear: it defines the problem, identifies the stakeholders, and explains the value.

### Layer 2: Requirements

Next, the team captures what the system must do.

**Requirement:** Patients must be able to book appointments online anytime.

**Requirement:** Appointments can only be booked between 8 AM and 5 PM Monday through Friday.

**Requirement:** Appointments can be booked up to 90 days in advance.

**Requirement:** Receptionists must be able to manually schedule appointments on behalf of patients.

**Requirement:** Appointment confirmation must be sent via email within one minute of booking.

**Requirement:** Patients must be able to view their upcoming appointments.

**Requirement:** Patients must be able to cancel appointments at least 24 hours in advance.

Notice that each requirement is specific and testable. An outside observer could verify whether the system meets each requirement.

### Layer 3: Use Cases

The team then describes complete interactions.

**Use Case: Schedule Appointment**

Actor: Clinic Patient

Preconditions:
- Patient is registered in the system
- Patient is logged in
- Doctor is accepting appointments
- Current time is before system booking cutoff (6 PM)

Main Success Scenario:
1. Patient selects desired doctor
2. System displays available appointment times (15-minute intervals)
3. Patient selects an appointment time
4. System validates the slot is still available
5. System creates the appointment record
6. System sends confirmation email to patient
7. System displays confirmation summary to patient

Alternative Flows:
- If no appointments are available: System suggests alternative doctors or dates
- If appointment is booked by another patient: System notifies patient and redisplays options
- If patient cancels at any point: System returns to doctor selection screen

Postconditions:
- Appointment exists in system
- Patient receives confirmation email
- Doctor's schedule reflects the appointment

**Use Case: Cancel Appointment**

Actor: Clinic Patient

Preconditions:
- Patient is logged in
- Patient has upcoming appointments
- Appointment is at least 24 hours away

Main Success Scenario:
1. Patient views their appointments
2. Patient selects an appointment to cancel
3. System displays cancellation confirmation message
4. Patient confirms cancellation
5. System deletes the appointment
6. System sends cancellation confirmation email
7. System returns the time slot to available

Alternative Flows:
- If appointment is within 24 hours: System displays message that cancellation is not allowed
- If patient chooses not to confirm: System returns to appointments list

Postconditions:
- Appointment is deleted
- Time slot becomes available again
- Patient receives cancellation confirmation

**Use Case: View Appointments**

Actor: Clinic Patient

Preconditions:
- Patient is logged in

Main Success Scenario:
1. Patient selects "My Appointments"
2. System retrieves all patient's appointments
3. System displays appointments sorted by date
4. Each appointment shows: doctor name, date, time, location

Alternative Flows:
- If patient has no appointments: System displays message "You have no upcoming appointments"

Postconditions:
- List of appointments is displayed

Additional use cases would cover receptionist actions, doctor availability management, and other capabilities.

### Layer 4: Domain Model

The team identifies business entities.

**Patient**
- Attributes: id, name, email, phone, registration_date, medical_record_number
- Constraints: Email must be valid, phone must be valid, medical_record_number must be unique
- Relationships: has many Appointments

**Doctor**
- Attributes: id, name, speciality, office_location, contact_number
- Constraints: Speciality must be from approved list
- Relationships: has many Appointments, has many Availability entries, works at many Clinics

**Appointment**
- Attributes: id, patient_id, doctor_id, date, time, duration, status, reason_for_visit
- Constraints: Cannot be in the past, cannot conflict with another appointment for same doctor, must be within clinic hours, cannot be on weekends
- Relationships: belongs to one Patient, belongs to one Doctor

**Clinic**
- Attributes: id, name, address, phone, business_hours_start, business_hours_end, timezone
- Relationships: has many Doctors, handles many Appointments

**Availability**
- Attributes: id, doctor_id, date, start_time, end_time, status
- Constraints: Must not conflict with appointments
- Relationships: belongs to one Doctor

**TimeSlot** (Value Object)
- Attributes: date, start_time, end_time, duration

## How they work together

These four layers work in concert.

When the AI implements "Schedule Appointment," it reads the use case.

The use case says: "System displays available appointment times."

The AI needs to know what an appointment is. It consults the domain model and finds the Appointment entity with its attributes and constraints.

The AI needs to know what a doctor is. It consults the domain model and finds Doctor with relationships to Clinic and Appointments.

The AI needs to understand the boundaries. It consults the vision and finds that the system serves one clinic with multiple doctors.

The AI needs to know the business rules. It consults the requirements and use cases and finds that appointments can only be booked during business hours, up to 90 days in advance, in 15-minute intervals.

With all this information, the AI can implement the feature correctly.

Without this information, the AI would have to guess.

## The specification is the source of truth

One critical principle: When requirements change, the specification is updated first.

This is a departure from traditional development.

In traditional development, requirements change. Developers modify code. Documentation falls out of date.

In specification-driven development, requirements change. Specifications are updated. Code is regenerated.

This keeps specifications aligned with reality.

## Maintaining specifications

Specifications must be maintained.

This requires discipline.

When a use case changes, the team updates it in the specification.

When a business rule changes, the domain model is updated.

When a new requirement emerges, it is added to the requirements list.

This maintenance overhead takes actual time and effort, but it pays for itself.

Why? Because when a use case changes, the implementation can be regenerated in minutes. When code is hand-written, changes mean hours or days of editing, testing, and review.

The return on investment for maintaining specifications is multiplicative.

## Specifications enable AI

Proper specifications are what allow AI to be effective.

Vague specifications lead to vague implementations, while clear, complete ones lead to implementations that are consistent and correct.

This is why the first half of this book focuses entirely on specifications.

Before any code is written, specifications must be complete.

## From specification to architecture

Specifications describe the business.

But specifications alone do not determine how to build the system.

Two organisations could have identical specifications yet build systems with completely different architectures.

One might choose a monolithic architecture. Another might choose microservices.

One might use Spring Boot. Another might use Quarkus.

One might use PostgreSQL. Another might use MongoDB.

Architecture answers: How should we build this?

Architecture sets constraints that guide these decisions.

## Architecture and skills

Architecture defines structural decisions.

Skills define implementation decisions.

Architecture says: "Use a modular monolith with REST APIs."

Skills say: "Use Spring Boot with constructor injection and Spring Data repositories."

Architecture says: "Validation belongs in the application layer."

Skills say: "Use Jakarta Validation annotations and validate in service methods."

Together, architecture and skills tell the AI exactly how to implement a specification. Without them, the AI has to guess, and most guesses produce code that doesn't fit the rest of the system.

## The complete workflow

The specification-driven development workflow is now clear.

1. **Vision:** Understand why the system exists.

2. **Requirements:** Capture what observable behaviours the system must have.

3. **Use Cases:** Describe complete interactions in detail.

4. **Domain Model:** Identify entities, attributes, relationships, and constraints.

5. **Architecture:** Define structural decisions and constraints.

6. **Skills:** Document implementation patterns and conventions.

7. **Implementation:** AI generates code from specifications and architecture.

8. **Testing:** AI generates tests from use cases.

9. **Review:** Humans validate correctness and business alignment.

10. **Deployment:** Feature is deployed using standard processes.

11. **Maintenance:** When requirements change, specifications are updated and implementation is regenerated.

Each stage has a purpose. Each stage reduces uncertainty.

## The payoff

Consider the difference in effort.

**Traditional approach:**
- Requirements vaguely described: 2 days
- Developers building and guessing: 5 days
- Rework due to misunderstandings: 3 days
- Testing and debugging: 2 days
- Total: 12 days

**Specification-driven approach:**
- Vision documented: 0.5 days
- Requirements captured: 1 day
- Use cases written: 1.5 days
- Domain model created: 1 day
- Architecture reviewed: 0 days (already exists)
- Skills reviewed: 0 days (already exist)
- AI implementation: 0.5 days
- Testing: 1 day
- Review: 1 day
- Total: 6.5 days

The specification-driven approach takes half the time. On second and subsequent features, the time is even less because specifications are often similar. On changes, the advantage grows even further, since regeneration is nearly free.

## What comes next

We have now established the foundation.

Chapters 6 through 8 cover architecture, skills, and the implementation workflow in detail.

The remaining chapters address practical questions:

How does this work with legacy systems?

How does team structure change?

What tooling supports this workflow?

How do we measure success?

But first, we must understand architecture.

Architecture is the bridge between what we want to build and how we build it.

That is the subject of the next chapter.
