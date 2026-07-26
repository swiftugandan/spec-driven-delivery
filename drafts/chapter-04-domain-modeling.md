# Chapter 4: Domain Modeling

Understanding the business objects

> The domain model is the blueprint of business reality.

## Why domain matters

Use cases describe behaviour. They explain what happens and in what sequence.

But use cases assume entities. In our appointment scheduling use case, we assumed Patient, Doctor, Appointment, and Clinic.

These entities are not obvious. They are discovered. They must be named, understood, and related to each other.

This is the domain model.

The domain model is the map of business concepts.

It identifies the entities that exist in the business, describes their attributes, and specifies their relationships.

The domain model is essential for AI implementation.

Without a domain model, the AI has to invent entities, guess attributes, and reverse-engineer relationships from use cases.

Most of the time, these guesses are wrong.

With a clear domain model, the AI knows exactly what entities to create and how to relate them.

## What is a domain model?

A domain model is a structured representation of the business.

It is a map of the business concepts and how they relate, not a technical architecture diagram, a database schema, or code.

For the clinic scheduling system, the domain model might identify:

**Patient**

A person who seeks medical care. Attributes include name, contact details, medical history. A patient may have multiple appointments.

**Doctor**

A medical professional who provides care. Attributes include name, speciality, contact details. A doctor has working hours and availability. A doctor may have multiple appointments.

**Appointment**

A scheduled interaction between a patient and doctor. Attributes include date, time, duration, status, reason for visit. An appointment involves exactly one patient and one doctor.

**Clinic**

The organization providing healthcare. Attributes include business hours, location, policies. A clinic may have multiple doctors and handle multiple appointments.

**Availability**

A time slot when a doctor is available. Attributes include date, time, duration, status. An availability record belongs to one doctor.

**TimeSlot**

A specific fifteen-minute window. Attributes include date, start time, end time. Time slots are used to check and reserve appointments.

Notice that each entity is concrete, with clear attributes and defined relationships.

## Entities and attributes

An entity is a thing the business cares about.

Entities are typically nouns. Patient. Doctor. Appointment.

Each entity has attributes.

**Patient** has: name, email, phone, address, medical record number.

**Doctor** has: name, speciality, contact number, office location, years of experience.

**Appointment** has: patient id, doctor id, date, time, duration, status, reason for visit.

Attributes should be specific. Not "information" but "email address." Not "details" but "phone number."

## Relationships

Entities are not isolated. They relate to each other.

**Patient has many Appointments.**

One patient might have three appointments.

**Doctor has many Appointments.**

One doctor might have fifty appointments.

**Appointment belongs to one Patient and one Doctor.**

Each appointment involves exactly one patient and one doctor.

**Doctor has many Availability entries.**

One doctor might have availability entries for every business day.

**Clinic has many Doctors.**

One clinic might employ twenty doctors.

These relationships constrain how entities interact. They guide implementation.

When the AI knows that "Patient has many Appointments," it knows to create a relationship in the database, a method to retrieve a patient's appointments, and validation rules to ensure appointments reference valid patients.

## Cardinality

Relationships have cardinality. This describes how many entities can relate.

**One-to-Many:** One doctor has many appointments. Many appointments belong to one doctor.

**Many-to-Many:** One doctor may work multiple clinics. One clinic may employ multiple doctors.

**One-to-One:** One appointment record maps to one time slot.

Cardinality is important because it affects database design, validation, and implementation logic.

## Constraints and business rules

The domain model documents constraints that apply to entities.

**Patient constraints:**

- Email must be valid
- Phone must be valid
- Medical record number is unique
- Date of birth must be in the past

**Doctor constraints:**

- Speciality must be from approved list
- Years of experience must be positive
- Office location must exist

**Appointment constraints:**

- Appointment cannot be before current time
- Appointment cannot be before patient's registration date
- Appointment cannot be outside doctor's working hours
- Appointment cannot conflict with another appointment for same doctor
- Appointment cannot be outside clinic business hours

These constraints are business rules, enforced in the domain model to guide how AI implements validation.

## The difference between domain and database

A domain model is not a database schema.

The domain model is the business view. The database is the technical implementation.

Often they are similar. But not always.

A domain model might say: "Patient has an address."

The database might store address in a separate table to avoid duplication.

A domain model might say: "Doctor has availability."

The database might compute availability dynamically from multiple sources rather than storing it.

The domain model describes business concepts.

The database implements storage for those concepts.

This distinction matters because the domain model should not be constrained by technical implementation details.

## Creating a domain model

Domain modeling is a collaborative process.

It involves:

Domain experts, who understand the business deeply.

Analysts, who understand what decisions need to be captured.

Architects, who understand technical constraints.

Developers, who implement from the model.

The process is iterative.

First pass: List all entities. For clinic scheduling, this might be: Patient, Doctor, Appointment, Clinic, Availability, Schedule, Notification, Review, Feedback.

Second pass: Refine each entity. What attributes does it have? What are the constraints?

Third pass: Define relationships. How do entities relate? What is the cardinality?

Fourth pass: Review consistency. Do all use cases reference entities and relationships in the model? If a use case mentions something not in the model, add it. If the model includes something not used in any use case, remove it.

## Domain model notation

Domain models can be represented in several ways.

**Prose:** Written descriptions of entities and relationships.

Example:
> Patient is a person seeking medical care. A patient has a name, email, phone number, and medical record number. A patient may have zero or more appointments. Each appointment is scheduled with exactly one doctor.

**Diagrams:** Visual representation of entities and relationships.

```
    Patient
      |
      | has many
      |
   Appointment
      |
      | involves one
      |
    Doctor
      |
      | works at
      |
    Clinic
```

**Structured list:** Entities with attributes and relationships listed systematically.

```
Patient
- name (String)
- email (String)
- phone (String)
- medical_record_number (String, unique)
- Relationships:
  - has many Appointments
  - registered at one Clinic

Doctor
- name (String)
- speciality (String)
- office_location (String)
- Relationships:
  - has many Appointments
  - works at many Clinics
  - has many Availability entries
```

The notation matters less than clarity and completeness.

What matters is that the team agrees on what entities exist and how they relate.

## Domain models and use cases

Domain models and use cases reinforce each other.

When writing use cases, you discover entities. You add them to the domain model.

When reviewing the domain model, you check it against use cases. Does every entity mentioned in a use case appear in the model? Does every entity in the model appear in at least one use case?

If an entity appears in use cases but not the model, add it.

If an entity is in the model but appears in no use case, remove it.

This cross-checking ensures the domain model is both complete and necessary.

## Value objects

Not every business concept is an entity.

Some are value objects. Value objects are immutable concepts that have no independent identity.

For example, an Address is a value object.

Addresses have attributes: street, city, state, zip. But an address has no identity of its own. It is meaningful only in the context of a patient or clinic.

Similarly, Money is a value object. It has an amount and currency, but no identity.

Value objects are typically attributes of entities, not entities themselves.

**Patient** has an **Address** (value object).

**Appointment** has a **TimeSlot** (value object).

This distinction affects implementation. Value objects are often immutable and can be shared. Entities are mutable and unique.

## Enumerations

Some attributes have a fixed set of valid values.

These are enumerations.

**Doctor.speciality** might be: Cardiology, Dermatology, Orthopedics, Psychiatry, etc.

**Appointment.status** might be: Scheduled, Completed, Cancelled, NoShow, Rescheduled.

**Patient.gender** might be: Male, Female, Other, Prefer Not To Say.

Enumerations guide validation. If someone tries to create an appointment with status "Invalid," the domain model rejects it.

Enumerations should be documented explicitly. Either in the domain model document or in code.

## The domain model as specification

Here is what makes the domain model essential for AI development.

When the AI reads a use case, it understands the sequence of steps.

When the AI reads the domain model, it understands the entities involved.

Together, they tell the AI everything needed to implement the feature correctly.

The AI knows what database tables to create, what attributes they need, what relationships to define, and what validations to enforce.

This is why a clear domain model is non-negotiable for specification-driven AI development.

## Evolving the domain model

The domain model is not static.

As the business learns more, the model evolves.

Maybe the team discovers that patients need addresses, so Address becomes a value object in the model.

Maybe the business decides to track appointment feedback, so Review becomes a new entity.

Maybe clinic policies change, requiring a new constraint on Doctor availability.

When the domain model changes, the specification is updated, affected use cases are reviewed, and the implementation is regenerated.

This is healthy evolution. The model grows as understanding deepens.

## What comes next

We now have the three foundational pieces of specification-driven development:

**Vision:** Why the system exists.

**Use Cases:** What the system does, step by step.

**Domain Model:** What entities and relationships exist in the business.

Together, these pieces describe what needs to be built.

But specifications alone are insufficient.

The AI also needs to know how to build it.

This is where architecture enters.

Architecture answers the structural question: How should we build this?

That is the beginning of the second half of this book.
