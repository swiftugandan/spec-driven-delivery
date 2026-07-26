# Chapter 6: Architecture as Context

Teaching AI How Your System Is Built

> A good architect does not tell every developer how to solve every problem. A good architect creates constraints within which good solutions naturally emerge.

## Why good AI produces bad software

Many teams experience a strange contradiction.

They ask an AI to build a feature.

The generated code compiles.

The tests pass.

The feature works.

Yet experienced developers reject the implementation almost immediately.

Why?

Because it doesn't look like the rest of the system.

Perhaps it uses a different naming convention. Perhaps it introduces another persistence layer. Perhaps it bypasses existing services. Perhaps it ignores logging. Perhaps it invents a new architectural pattern.

The AI has written software that belongs in a different project, not incorrect software.

The problem is context, not implementation.

## Every organisation has invisible rules

Walk into any mature software organisation.

Nobody begins by explaining the business. Instead, experienced developers quickly learn rules such as:

"Controllers never access repositories directly."

"Every command is audited."

"Only domain services may publish events."

"Validation belongs in the application layer."

"Never expose database entities through APIs."

None of these rules are obvious. They exist because previous projects taught difficult lessons. Collectively they define the organisation's architecture.

Humans absorb these conventions gradually.

AI needs them explicitly.

## Architecture is more than components

Many developers think architecture means diagrams. Boxes. Arrows. Databases. Message queues. Servers.

Those diagrams are useful. They are not the architecture.

Architecture is the collection of decisions that guide every implementation: layering, dependencies, naming, module boundaries, communication patterns, security, error handling, testing strategy, and deployment model.

Architecture answers a single question: How do we build software here?

## Why AI needs constraints

Human developers often view constraints as limitations. Architects understand them differently: constraints reduce complexity.

Imagine telling an AI: Build an order management system.

Thousands of designs are possible.

Now add a few constraints. Use a modular monolith. REST endpoints only. PostgreSQL persistence. Domain-driven architecture. Repository pattern. Command-query separation. Integration tests for every use case.

The design space shrinks dramatically.

Ironically, limiting freedom often improves creativity. The AI now spends less effort choosing an architecture and more effort implementing the business correctly.

## Architecture reduces hallucination

One of Simon Martinelli's key observations is that AI performs best when architectural guidance is explicit rather than implied.

Without guidance, the model fills gaps using patterns it has seen elsewhere. Sometimes those patterns fit. Sometimes they conflict with your system.

Architecture removes unnecessary choices.

The AI no longer asks itself:

- Should I create another service?
- Should I use dependency injection?
- Should I expose GraphQL?
- Should I create a new repository?

The specification has already answered these questions.

Less guessing means more consistency.

## Architecture as a contract

Traditional architecture documents were often descriptive. They explained the system after it had already been built.

AI changes their purpose.

Architecture becomes prescriptive.

Instead of saying: This is how the system works.

It says: Every implementation must follow these rules.

The document becomes a contract between architects, developers, and AI systems.

## Layers

One of the simplest architectural constraints is layering. Consider a conventional enterprise application:

```
Presentation
    ↓
Application
    ↓
Domain
    ↓
Infrastructure
    ↓
Database
```

Each layer has a responsibility.

**Presentation.** Communicates with users or external systems.

**Application.** Coordinates use cases.

**Domain.** Contains business rules.

**Infrastructure.** Handles persistence and external services.

The AI does not need to invent this structure. It simply follows it.

## Dependency rules

Layers alone are insufficient. Dependencies matter.

For example:

- Presentation may depend upon Application.
- Application may depend upon Domain.
- Infrastructure may depend upon Domain.
- Domain depends upon nothing.

These rules prevent accidental coupling. An AI informed of these constraints naturally produces cleaner software.

## Package structure

Many teams underestimate the importance of directory layout. Consider two alternatives.

**Structure organised by technology:**

```
controllers/
services/
repositories/
entities/
```

**Structure organised by business capability:**

```
customers/
orders/
billing/
shipping/
```

Both compile. Both function. Only one reflects the business.

Architectural decisions like these should not be rediscovered every time the AI generates code. They belong in the architectural context.

## Naming conventions

Naming appears trivial until inconsistency spreads.

Suppose three developers ask AI to implement similar features. One generates: `CustomerManager`. Another: `CustomerService`. Another: `CustomerProcessor`.

All three perform the same role.

Now the project contains three conventions.

Architectural guidance prevents this. For example:

- Application services always end with: `Service`
- Repositories always end with: `Repository`
- Commands begin with: `Create`, `Update`, `Delete`
- Events end with: `Event`
- Queries end with: `Query`

The AI simply follows the convention.

## Error handling

Every system fails.

The question is whether failure is predictable.

Architecture should define the exception strategy, retry policy, logging, user messages, and audit requirements.

Without guidance, AI invents these behaviours. With guidance, every feature behaves consistently.

## Security as architecture

Security should never be left to implementation.

Architectural rules define authentication, authorisation, encryption, secrets management, audit logging, and data classification.

Individual use cases may mention permissions. The architecture defines how permissions work across the entire system.

## Testing strategy

Architecture also includes quality expectations. For example:

Every use case requires:

- Unit tests
- Integration tests
- API tests

Or perhaps:

- Business logic requires unit tests.
- Persistence requires integration tests.
- Critical workflows require end-to-end tests.

These decisions should not appear inside prompts. They belong in reusable architectural guidance.

## The role of arc42

Simon Martinelli recommends documenting architecture using arc42, a widely used template for software architecture documentation.

The specific template matters less than the principle.

Architecture should be explicit, accessible, structured, and maintained.

Whether an organisation uses arc42, C4, Architecture Decision Records (ADRs), or another framework, the important point is that AI has access to architectural intent before implementation begins.

## Architecture is stable

Requirements change frequently.

Architecture changes slowly.

A pricing rule may change every month. A product catalogue may change every week. The decision to use a modular monolith rather than microservices may last a decade.

This stability makes architectural context highly reusable. Instead of repeating the same instructions in every prompt, we define them once. Every future implementation inherits them automatically.

## From prompt engineering to context engineering

Early AI adoption focused heavily on prompts. Developers searched for the perfect wording. Prompt libraries grew. Templates multiplied.

Eventually organisations discovered an uncomfortable truth.

Excellent prompts cannot compensate for missing project knowledge.

Instead of improving prompts, mature AI teams improve context. They provide specifications, domain models, architecture, standards, and examples.

The prompt itself becomes surprisingly small.

Instead of: Build an order management module following all company standards...

The interaction becomes: Implement Use Case UC-17.

Everything the AI needs already exists.

This shift, from prompt engineering to context engineering, is one of the defining characteristics of professional AI-assisted development.

## Architecture is necessary, but not sufficient

By now we have assembled three important pieces of the puzzle: we understand the business through use cases, the business language through the domain model, and the technical environment through the architecture.

Yet one challenge remains.

Different organisations implement the same architecture differently. Two companies may both use Spring Boot. One structures services around commands. Another around aggregates. One prefers constructor injection. Another generates code. One requires mutation testing. Another requires contract tests.

These are organisational practices, not architectural decisions.

Rather than repeating them endlessly in prompts, AI-native development captures them as reusable implementation knowledge.

Simon Martinelli calls these Skills.

They are the final piece that transforms specifications into consistent software.
