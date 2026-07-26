# Chapter 8: From Specification to Software

The AI-Native Development Workflow

> When specifications become the primary artefact, software development stops being a coding process and becomes a knowledge process.

## The moment everything changes

Imagine two software teams receiving exactly the same request.

The request is simple.

"Allow customers to schedule appointments online."

### Team One

The developers immediately open their IDEs.

One begins designing a database. Another creates REST endpoints. A third builds a React page.

Questions emerge almost immediately.

Can appointments overlap? Can customers cancel them? How far into the future may they book? Who sends reminders? Are weekends allowed?

The team schedules meetings. Emails circulate. Slack conversations multiply.

Some assumptions are documented. Most are not.

Eventually the software works.

Months later nobody remembers why certain decisions were made.

### Team Two

Nobody writes code.

Not yet.

Instead they ask: What does "schedule an appointment" actually mean?

The discussion produces a use case. A domain model is refined. Business rules are clarified.

The architecture already exists. Implementation skills already exist.

The AI receives the specification.

Minutes later, the feature exists.

The implementation is reviewed rather than invented.

The difference between these teams is preparation, not AI.

## The knowledge pipeline

Traditional development centres on implementation.

AI-native development centres on knowledge.

The workflow becomes a pipeline.

```
Business Vision
    ↓
Requirements
    ↓
Use Cases
    ↓
Domain Model
    ↓
Architecture
    ↓
Skills
    ↓
AI Implementation
    ↓
Testing
    ↓
Review
    ↓
Deployment
```

Each stage reduces uncertainty.

Each stage removes decisions the AI would otherwise have to invent.

## Stage 1: Understanding the problem

Every feature begins with a business problem.

Notice that we deliberately avoid beginning with a solution.

**Poor requirement:** Add another button.

**Better requirement:** Customers cannot book appointments outside office hours.

The second describes a problem. Solutions remain open.

Good software engineering begins with understanding, before any code gets written.

## Stage 2: Capturing requirements

Requirements should describe observable business behaviour.

Consider this example.

### Business requirement

- Patients should be able to schedule appointments without calling the clinic.
- Receptionists should still be able to schedule appointments on behalf of patients.
- Appointments must not overlap.
- Doctors may define unavailable periods.

Already we know far more than: Build appointment booking.

The requirement is becoming precise.

## Stage 3: Writing the use case

Now the behaviour becomes explicit.

### Use case: Schedule Appointment

**Primary Actor:** Patient

**Preconditions:**
- Patient is registered
- Doctor accepts appointments

**Main Success Scenario:**
1. Patient selects doctor
2. System displays available times
3. Patient selects a time
4. System validates availability
5. System creates appointment
6. System confirms booking

**Alternative:**
- Selected time no longer available
- System requests another selection

**Postconditions:**
- Appointment exists
- Confirmation sent

The AI now understands the interaction.

## Stage 4: Refining the domain

Next we identify the business concepts.

**Patient**

- Name
- Contact Details
- Medical Record Number

**Doctor**

- Speciality
- Working Hours

**Appointment**

- Date
- Time
- Duration
- Status

**Clinic, Availability, Room**

Each entity receives attributes. Notice how naturally the business language emerges.

## Stage 5: Applying architecture

Now architecture provides constraints.

Suppose the organisation has already defined:

- Modular Monolith
- Spring Boot
- PostgreSQL
- REST
- Feature Packages
- Integration Tests

These decisions are already made.

The feature should not revisit them.

One of the hidden costs of traditional development is repeatedly solving problems that were solved years ago.

Architecture prevents this.

## Stage 6: Applying skills

Next the AI receives implementation knowledge.

For example:

**Repositories:** Spring Data

**Validation:** Jakarta Validation

**Testing:** JUnit

**Logging:** Structured logging

**Events:** Domain events only

None of these belong inside the use case.

They belong inside reusable skills.

## Stage 7: Implementation

Only now does implementation begin, and the prompt becomes almost trivial.

Instead of writing pages of instructions, the developer simply asks:

Implement the Schedule Appointment use case.

Everything else already exists.

The AI is no longer inventing software. It translates specifications into code, which changes what implementation means.

## Stage 8: Testing

Traditional projects often treat testing as something that happens after implementation.

AI-native development encourages a different perspective.

Testing validates the specification, not merely the code.

Consider our use case. Every numbered step naturally becomes a test.

**Step 1:** Patient selects doctor.
**Test:** Doctor list appears.

**Step 4:** System validates availability.
**Test:** Conflicting appointments rejected.

**Alternative Flow:** Unavailable slot.
**Test:** Alternative selection requested.

The specification and the tests remain synchronised because they describe the same behaviour.

## Stage 9: Human review

One misconception about AI-native development is that humans disappear. In practice, the human role changes.

Developers spend less time writing code and more time reviewing business correctness, architectural consistency, security, performance, and maintainability.

Simon Martinelli recommends that review effort should be proportional to business risk.

A financial trading system deserves more scrutiny than an internal reporting tool.

AI changes implementation speed.

It does not eliminate engineering judgement.

## Stage 10: Deployment

Deployment becomes almost anticlimactic.

The implementation has already been validated against:

- Specifications
- Architecture
- Organisational standards

The deployment pipeline behaves exactly as it always has.

DevOps, Continuous Integration, and Continuous Delivery all remain essential.

AI complements these disciplines rather than replacing them.

## A living specification

The greatest difference appears months later.

The business changes its mind.

This always happens.

A new requirement appears.

Patients should now receive SMS reminders twenty-four hours before their appointment.

In many projects the first instinct is:

Open the code. Find the scheduling module. Add reminder logic.

In AI-native development, the first instinct is different.

Update the specification.

The use case gains another step. The domain model gains a Reminder entity. Perhaps a Reminder Policy value object.

The implementation regenerates.

The specification remains the source of truth.

This simple discipline prevents one of the oldest problems in software engineering:

Documentation drifting away from implementation.

## The economics of regeneration

Historically, regeneration sounded absurd.

Generating an entire feature again would have been prohibitively expensive.

AI changes the economics.

Suppose implementation takes five minutes.

Regeneration also takes five minutes.

Suddenly, modifying the specification first becomes entirely practical.

Instead of treating generated code as precious, we treat it as reproducible.

This encourages a healthier mindset.

Specifications become investments.

Code becomes an expression of those investments.

## Incremental development

One concern often raised is: Do we have to specify the entire system before generating anything?

Absolutely not.

AI-native development remains iterative.

A project might proceed like this:

**Iteration One:** Register Patient

**Iteration Two:** Schedule Appointment

**Iteration Three:** Cancel Appointment

**Iteration Four:** Billing

**Iteration Five:** Reporting

Each iteration follows the same workflow.

Understanding grows continuously. Specifications evolve continuously. Software evolves continuously.

This is entirely compatible with Agile thinking.

The difference is that the iteration revolves around specifications rather than hand-written code.

## The developer's new role

Notice how the developer's day has changed.

**Less time:**

- Writing boilerplate
- Wiring frameworks
- Creating CRUD operations
- Configuring dependency injection

**More time:**

- Discovering requirements
- Modelling domains
- Improving architecture
- Reviewing implementations
- Refining specifications
- Solving difficult business problems

This elevates software engineering rather than eliminating it. Routine implementation becomes increasingly automated, while judgement becomes increasingly valuable.

## A new definition of done

Traditional teams often define a feature as complete when:

- The code is merged
- The tests pass
- The feature is deployed

An AI-native team adds another criterion.

The specification must also be complete.

A feature is not finished unless someone reading the specification months later can understand:

- Why it exists
- What it does
- What business rules apply
- How it fits into the broader system

In this sense, the specification is the development, not documentation produced after it.

## The workflow in practice

By now, the methodology should feel almost mechanical.

Every feature follows the same sequence.

1. Understand the business problem
2. Capture the requirements
3. Write or refine the use case
4. Update the domain model
5. Apply architectural constraints
6. Apply implementation skills
7. Generate the implementation
8. Execute and extend the tests
9. Review according to business risk
10. Deploy
11. Repeat

Notice what is missing.

There is no phase labelled: Write thousands of lines of code.

Coding has become a consequence of understanding rather than the primary activity.

## Looking ahead

So far, every example in this book has assumed a brand-new system.

Unfortunately, that is not how most organisations work.

Most software engineers spend their careers maintaining systems that already exist.

Some are ten years old. Some are thirty. Some were written before the internet.

How does specification-driven development work when the specifications no longer exist?

How do we modernise a legacy system whose only documentation is its source code?

This is where Simon Martinelli introduces one of the most compelling applications of the methodology:

Reverse engineering software back into specifications before generating its successor.
