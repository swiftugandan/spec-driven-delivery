# Chapter 3: Requirements and Use Cases

Specifying what the system must do

> Vague requirements produce beautiful mistakes.

## From vision to requirements

Vision explains why the system exists.

Requirements explain what the system actually does.

The leap from one to the other is not obvious.

Consider our clinic scheduling vision: Patients need to book appointments online without calling. Receptionists should still be able to book on behalf of patients.

That vision is clear.

But it immediately raises questions. What if no appointments are available? What if a patient tries to book at 3 AM? What if the same time slot is booked twice? How far into the future can patients book? Can they cancel? Can they reschedule?

These questions need answers.

Those answers are requirements.

## What is a requirement?

A requirement is an observable, testable statement about system behaviour.

Poor requirement: The system should be user-friendly.

That describes a quality. How do you test user-friendliness?

Better requirement: Patients must complete an appointment booking within three minutes using no more than five clicks.

That is observable and testable. You can measure whether patients can complete the task in three minutes.

Poor requirement: The system should support scheduling.

That describes a category of functionality. What does support mean?

Better requirement: The system shall display available appointment slots for the selected doctor at fifteen-minute intervals.

That is specific and verifiable.

Good requirements share several characteristics.

They are observable. You can see whether the system does this.

They are testable. You can write a test case that passes or fails.

They are free of implementation details. They describe what must happen, not how it happens.

They mention specific measurable values. Not "timely" but "within five minutes." Not "many" but "at least twenty."

## Capturing requirements

Requirements come from many sources.

Product owners understand user needs. Business analysts understand organisational constraints. Domain experts understand business rules. Stakeholders understand strategic goals.

The conversation that produces requirements is crucial. Questions surface assumptions. Disagreements reveal misunderstandings.

A typical requirements workshop might look like this.

**Facilitator:** What needs to happen for a patient to book an appointment?

**Domain Expert:** They need to see when the doctor is available.

**Product Owner:** But only during the hours the clinic is open. We close at 5 PM.

**Business Analyst:** Actually, we want to allow booking 24/7, but only for future dates. And only up to three months ahead. If someone tries to book beyond three months, we reject it.

**Domain Expert:** Why three months?

**Business Analyst:** Because the doctors' schedules are only confirmed three months out. Beyond that, we don't know availability.

**Product Owner:** What about patients who want to book further in advance?

**Domain Expert:** They call. That's a small number. Not worth optimising for now.

**Facilitator:** So the requirement is: Patients may book appointments online up to three months in advance, during any day and time, but only for appointments within the clinic's open hours.

This conversation surfaces decisions that would otherwise be invisible in code.

## Documenting requirements

Requirements should be captured in writing. They should be centralized. They should be maintained.

Many organisations use Jira, Confluence, or similar tools.

Martinelli's approach is compatible with any documentation system.

What matters is that:

Requirements are explicit, not implied.

Requirements are accessible to the team.

Requirements are updated when business needs change.

A typical requirements document might look like:

### Appointment booking

**Requirement:** Patients may book appointments online up to three months in advance.

**Requirement:** Appointment slots are displayed at fifteen-minute intervals.

**Requirement:** Patients may not book outside clinic business hours (8 AM - 5 PM, Monday-Friday).

**Requirement:** If a patient tries to book an already-reserved slot, the system displays the next available alternative.

**Requirement:** Booking confirmation is sent via email within one minute.

**Requirement:** Patients must provide name, contact number, and reason for visit.

Notice that each requirement is singular. Each is testable. Each describes observable behaviour.

## System use cases

Requirements describe individual behaviours.

Use cases describe complete interactions.

A requirement might be: "The system displays available appointment slots."

A use case might be: "Patient books an appointment," which includes:

Patient selects doctor.

System displays available slots.

Patient selects a time.

System confirms availability.

System creates the appointment.

System sends confirmation email.

Use cases are more powerful than requirements for AI-assisted development.

Use cases are complete. They describe an entire user goal from start to finish.

Use cases are structured. They have a predictable format: actors, preconditions, main flow, alternatives, postconditions.

Use cases are testable. Every step becomes a test case.

## The use case structure

Simon Martinelli recommends use cases as the primary specification format.

A use case contains:

**Title.** The goal being accomplished. Usually a verb phrase.

**Actor.** Who is performing this use case? A patient? A receptionist? A system?

**Preconditions.** What must be true before this use case begins?

**Main Success Scenario.** The happy path. What happens when everything works correctly?

**Alternative Flows.** What happens when something doesn't work as expected?

**Postconditions.** What is true after the use case completes successfully?

**Business Rules.** Any constraints or decisions that apply.

## An example use case

Here is a complete use case for clinic scheduling.

### Use case: Schedule Appointment

**Title:** Schedule Appointment

**Actor:** Clinic Patient

**Preconditions:**
- Patient is registered in the system
- Patient is logged in
- Doctor is available for bookings
- Clinic booking window is open (8 AM - 5 PM)

**Main Success Scenario:**

1. Patient selects desired doctor from list
2. System displays available appointment slots for the selected doctor
3. Patient reviews available times
4. Patient selects an appointment time
5. System checks availability again (to handle race conditions)
6. System reserves the appointment slot
7. Patient confirms the booking
8. System sends confirmation email with appointment details
9. System displays appointment summary to patient
10. Appointment is now visible in patient's dashboard

**Alternative Flows:**

**Alternative A: No Appointments Available**
- At step 2: If no appointments are available for selected doctor within booking window
- System displays message: "No appointments available with this doctor. Please try another doctor or date range."
- Patient may select different doctor or cancel

**Alternative B: Appointment Already Booked**
- At step 6: If appointment slot was booked by another patient after step 5
- System notifies patient: "That slot is no longer available"
- System redisplays available times
- Patient selects new time

**Alternative C: Patient Cancels**
- At any step: Patient clicks "Cancel"
- System returns to doctor selection screen
- No appointment is created

**Postconditions:**
- Appointment is created in system
- Patient has received confirmation email
- Doctor's schedule shows appointment
- Appointment is visible in patient's dashboard

**Business Rules:**
- Appointments may only be booked up to 90 days in advance
- Appointment slots are fifteen-minute intervals
- Appointments cannot be scheduled outside clinic hours (8 AM - 5 PM)
- Appointments cannot be scheduled on weekends
- Patient cancellations must occur at least twenty-four hours before appointment
- Doctor availability must be manually configured by staff

## Why use cases trump requirements

Use cases and requirements describe the same system behaviour, but from different angles.

Requirements focus on individual needs: "The system must validate email addresses."

Use cases focus on complete interactions: "A patient books an appointment, which requires their email address to be valid."

For AI implementation, use cases are superior because:

They are complete. The AI understands the entire interaction, not isolated fragments.

They provide context. The AI sees how steps relate. It understands causality.

They naturally produce test cases. Each step becomes an assertion.

They are testable at the use case level, not just at the requirement level.

They are closer to how humans think about systems. "I want to book an appointment" is a use case, not a requirement.

## Use cases and user stories

Many organisations use user stories instead of use cases.

A user story is typically: "As a [role], I want to [action], so that [benefit]."

For example: "As a patient, I want to book an appointment online, so that I don't have to call."

User stories are valuable for product management and prioritisation.

But for implementation, user stories lack the detail that use cases provide.

A single user story often contains multiple use cases. "Book an appointment" includes viewing availability, selecting a time, confirming, and receiving confirmation.

Martinelli's recommendation is to use stories for planning, but implement from use cases.

The workflow looks like:

User story identifies a capability.

Use cases break down that capability into precise interactions.

AI implements from use cases.

## Completeness and consistency

One critical principle: use cases should be complete and internally consistent.

Incomplete use cases generate incomplete implementations.

If a use case describes "send confirmation email" but never specifies what goes in the email, the AI must guess.

Inconsistent use cases confuse implementation. If one use case says "appointments cannot be booked on weekends" but another allows it, the AI cannot determine the correct behaviour.

Before passing use cases to AI, the team should review:

Are all steps included? If something important is missing, add it.

Are all alternatives covered? If there are cases not described, add them.

Are business rules explicit? If a rule is implied but not stated, state it.

Are terms consistent? If an entity is called "Doctor" in one use case and "Physician" in another, standardise.

## Multiple use cases per feature

Large features often contain multiple use cases.

An appointment system might include:

Schedule Appointment

Cancel Appointment

Reschedule Appointment

View My Appointments

Manage Doctor Availability

Send Appointment Reminder

Each is a separate use case. Each describes a complete interaction.

When all use cases for a feature are written, the feature is fully specified.

## Use cases and change

Use cases are a living specification.

When business requirements change, use cases are updated.

When a new edge case is discovered, an alternative flow is added.

When a business rule changes, it is updated in the business rules section.

Because code is generated from use cases, updating the use case means the implementation can be regenerated.

This differs from hand-written code, where requirements changes mean manual editing.

## From use cases to implementation

Once use cases are written and reviewed, they become the specification that guides implementation.

The AI receives the use case. It understands the complete interaction. It generates code that implements every step.

But before the AI begins, there is one more critical piece: the domain model.

The domain model identifies the business objects that appear in use cases.

In the clinic example, the domain model includes Patient, Doctor, Appointment, and Clinic.

Understanding these entities, their attributes, and their relationships, is essential for correct implementation.

That is the subject of the next chapter.
