# Chapter 2: Vision and Purpose

Understanding why the system exists

> Before building anything, know why you are building it.

## The first question

Every software system exists to solve a problem.

This statement sounds obvious. Yet most organisations never explicitly answer it.

Instead, requirements immediately jump to "build this feature" without answering a more fundamental question: What problem does this feature solve? Who has that problem? Why is it worth solving now?

Specification-driven development begins with these questions.

## Vision before requirements

Traditional projects start like this.

A product manager writes tickets. Developers ask clarifying questions. Requirements spiral outward. Code begins. Months later, nobody remembers what problem was being solved.

Specification-driven development starts differently.

Before any technical work, before any requirements, before any design discussions, the team answers one simple set of questions.

What problem are we solving?

Who has this problem?

Why does it matter?

These answers constitute the system's vision.

## What is vision?

Vision is not a mission statement or corporate prose.

Vision is the explicit articulation of:

The problem the system solves.

The users who have that problem.

The boundaries of the system.

The major capabilities required to solve the problem.

Vision answers: Why does this system exist?

## An example: clinic scheduling

Consider a healthcare organisation deciding to build an online appointment booking system.

Poor vision: Build a scheduling system.

That describes a solution rather than a problem.

Better vision:

Clinic patients currently call to schedule appointments. This requires staff to answer phones during business hours. When staff are busy, wait times exceed thirty minutes. Patients often hang up. Patients who do connect can only book during office hours, so working patients must call during their lunch break or before work. This creates a bad experience and wastes staff time.

We want to let patients book appointments online, anytime, from their phone or computer. This reduces staff time spent on phones and improves patient experience.

The clinic may also want the ability to manually schedule on behalf of patients, because not all patients are comfortable with online booking.

Notice what this vision includes:

The problem: Patients waste time calling. Staff waste time answering phones.

The users: Clinic patients. Clinic staff.

The boundaries: Scheduling appointments. Not billing. Not medical records. Not diagnostics.

The capabilities: Online booking. Manual booking by staff. Availability display.

This vision takes a paragraph. Yet it contains everything a team needs to know to start building correctly.

## Why vision matters

Vision accomplishes several things.

First, it aligns the team. Everyone understands why they are building. Disagreements about features can be resolved by asking: Does this solve the problem we identified?

Second, it prevents scope creep. The vision explicitly declares what the system is not responsible for. Requests to add billing integration can be evaluated: This is outside our scope.

Third, it enables good architecture decisions. Architectural decisions flow from the problem being solved. A system designed to handle high volume and low latency needs different architecture than a system optimised for simplicity and ease of change.

Fourth, it gives AI context. When implementation begins, the AI knows not just what to build, but why it is being built. This context helps the AI make reasonable choices about trade-offs.

## Vision and requirements are different

Many organisations conflate vision and requirements.

They are not the same.

Vision explains why the system exists.

Requirements describe specific observable behaviours the system must have.

Vision is stable. It may not change for years.

Requirements change frequently. They are refined continuously based on learning.

Vision is written in business language.

Requirements are written in operational language.

A vision might be: "Patients need to book appointments without calling."

A requirement might be: "The system must accept appointment requests up to three months in advance."

The vision explains the problem. The requirement describes a constraint on the solution.

## Starting the conversation

Writing vision should involve everyone who understands the business problem.

This typically includes:

Product managers, who understand user needs.

Business analysts, who understand organisational constraints.

Domain experts, who understand the specific problem deeply.

Sometimes, developers who have experience solving similar problems.

The goal is clarity, not consensus.

The conversation might go like this:

**Product Manager:** Patients cannot book appointments online. They have to call.

**Business Analyst:** Receptionists spend forty percent of their time answering appointment calls.

**Domain Expert:** Some patients also won't call because they are embarrassed about their condition. They would prefer to book online anonymously.

**Developer:** Could we integrate with the clinic's existing calendar system?

**Business Analyst:** Yes. That's in scope. But only for staff scheduling. Patients can only book available slots, not directly modify the doctor's calendar.

These conversations clarify thinking, surface assumptions, and reveal constraints.

They produce vision.

## Documenting vision

Vision should be written down. Explicitly. In a place the team can reference.

The format matters less than the completeness.

Some organisations use a one-page vision document. Others use a slide in a presentation. Some use a section in a README.

The format is less important than consistency and accessibility. Every team member should know where to find the system's vision.

A typical vision document might include:

**The Problem.** What situation exists today that is unsatisfactory?

**The Stakeholders.** Who experiences this problem? Who benefits from solving it?

**The Scope.** What is this system responsible for? What is explicitly out of scope?

**The Approach.** What general approach will solve this problem?

**The Success Criteria.** How will we know we have solved the problem?

**Constraints.** What must remain true? What decisions have already been made?

## Vision and scale

Vision scales across systems and organisations.

A small feature has a vision.

A product has a vision.

An entire organisation has a vision.

At each level, vision answers the same question: Why does this exist?

The clinic scheduling system has a vision.

Within that system, the online booking feature has a vision.

Within online booking, the payment collection step has a vision.

Each vision is complete within its scope. Each vision guides the layer below it.

This creates a hierarchy of purposes.

## What comes next

Once vision is clear, the team can begin capturing requirements.

Requirements flow naturally from vision. They answer: What specific capabilities do we need to solve this problem?

But before jumping to requirements, the team should validate that vision is clear.

Test this: Can you ask any team member why the system is being built? Can they explain it in one or two sentences? Do all team members give roughly the same answer?

If not, vision is not yet clear.

Clarify vision before proceeding.

This costs a few hours. It saves weeks of building the wrong thing.

## The economics of vision

It is tempting to skip vision because it feels like overhead.

But it is the highest-leverage work in software development.

When vision is clear, requirements become obvious. Specifications become crisp. Implementation becomes straightforward.

When vision is unclear, everything that follows is expensive and painful.

Spend the time to get vision right.

The payoff is multiplicative.

## A living vision

Vision is not written once and forgotten.

Organisations change, markets shift, and technology evolves.

But vision should remain stable. If vision is changing every quarter, either the system is solving the wrong problem, or the vision was not clear to begin with.

Still, vision should be revisited annually. Does it still reflect why this system exists? Is anything in the original problem statement no longer true?

This review ensures vision remains alive and relevant.

## Next

With vision established, we move to requirements.

Requirements are the translation of vision into specific observable needs.

If vision answers "why," requirements answer "what."

The team is now ready to describe what the system actually needs to do.
