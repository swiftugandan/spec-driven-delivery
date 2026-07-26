# Chapter 9: Brownfield Development

Reverse Engineering Legacy Systems into Living Specifications

> The greatest opportunity for AI is not writing the next application. It is helping us finally understand the applications we already have.

## The reality of software engineering

If software engineering conferences reflected reality, every developer would be building greenfield systems.

Microservices. Cloud-native architectures. Event-driven platforms. Perfect domain models.

In reality, most software engineers spend their careers working on something very different.

Existing systems.

Some are five years old. Many are twenty. Some are older than the developers maintaining them.

These systems run banks. Hospitals. Governments. Airlines. Factories. Insurance companies. Utilities.

They are essential rather than exciting, and they often share the same problem: nobody fully understands them anymore.

## The missing specification

Imagine inheriting an application written fifteen years ago.

The original architects have retired. The documentation disappeared years ago. Requirements exist only as outdated Word documents. The UML diagrams no longer match reality.

The only trustworthy artefact is the source code.

When a new feature request arrives, most developers do exactly what their predecessors did: they search.

```
CustomerService
↓
OrderManager
↓
InvoiceProcessor
↓
PaymentHelper
↓
UtilityFactory
```

Hours become days. Days become weeks. Eventually someone discovers where the business rule lives.

Sometimes.

## Code is a poor knowledge repository

Source code tells us how something works.

It rarely tells us why.

Consider this fragment.

```java
if(customer.getStatus() == 7)
```

What does status seven mean?

Gold customer? Suspended? Deleted? Pending verification?

The compiler understands. The business no longer does, and the original meaning has vanished.

This happens often.

Business knowledge slowly dissolves into implementation details.

## Legacy systems are archaeological sites

Maintaining an old system resembles archaeology more than engineering.

Archaeologists uncover fragments. A wall. A road. A tool. Gradually a civilisation emerges.

Software engineers do the same.

A controller. A database table. A configuration file. An integration test. Eventually a business process becomes visible.

This investigative work consumes a large proportion of software maintenance.

## AI as an archaeologist

Many discussions of AI focus on generation.

Generation is only half the story.

AI is equally valuable for understanding.

Given enough context, an AI can identify entities, workflows, duplicated rules, hidden dependencies, architectural patterns, inconsistencies, and undocumented assumptions.

Instead of asking the AI to generate new software, we first ask it to explain the software that already exists. That single change in ordering matters.

## Reverse engineering the domain

Suppose we analyse an old warehouse application.

The AI examines the database schema, REST endpoints, service classes, business logic, validation rules, and integration tests.

Instead of producing code, it produces knowledge.

For example:

**Entities**

- Warehouse
- Product
- Stock Item
- Transfer
- Supplier

Relationships emerge. Business terminology emerges. Rules emerge.

The domain model begins to reappear.

Knowledge that had been buried inside code becomes visible again.

## Recovering use cases

The same applies to behaviour.

A legacy application rarely contains explicit use cases.

Instead, they are scattered across controllers. Services. SQL queries. Message handlers. Background jobs.

AI can synthesise these into coherent workflows.

For example:

### Use case: transfer stock between warehouses

**Primary Actor:** Warehouse Operator

**Main Flow**

1. Select source warehouse
2. Select destination warehouse
3. Choose products
4. Validate stock
5. Reserve inventory
6. Create transfer
7. Notify destination warehouse

No developer explicitly wrote this specification.

It emerged from analysing the implementation.

This is one of AI's most valuable capabilities.

## Why reverse engineering matters

Many organisations believe they cannot adopt specification-driven development because they already possess millions of lines of code.

The assumption is understandable, but it is incorrect. Rather than replacing the software, you begin by recovering its knowledge.

Once the knowledge exists, future development becomes specification-driven.

The transition is evolutionary rather than revolutionary.

## The strangler pattern for knowledge

Martin Fowler's Strangler Fig Pattern is normally applied to software architecture.

We can apply the same idea to specifications.

Instead of replacing an entire legacy application, we gradually surround it with better knowledge.

For one module:

1. Recover the domain model
2. Recover the use cases
3. Validate them with business experts
4. Generate new features from those specifications
5. Repeat

Eventually the specification becomes richer than the original codebase.

The code is no longer the authoritative source.

## Validating with the business

One advantage of recovered specifications is that business stakeholders can finally participate again.

Very few business experts can review Java, and almost none can review SQL.

Most can review this:

- Customer places order
- Credit limit checked
- Inventory reserved
- Invoice generated

The conversation moves back to the language of the business.

This often uncovers decades-old misunderstandings.

Business users frequently say: "That's not how it is supposed to work."

Developers reply: "That's how it has worked for fifteen years."

The recovered specification becomes the basis for deciding whether behaviour is intentional or accidental.

## Identifying accidental complexity

Legacy systems accumulate accidental complexity.

Examples include obsolete validation, duplicated business rules, dead code, redundant workflows, and historical workarounds.

These often survive because nobody remembers why they were introduced.

AI can highlight suspicious areas, but it cannot determine business intent on its own; that judgment remains a human responsibility. The combination works well: AI discovers, humans decide.

## Modernisation begins with understanding

Traditional migration projects often begin with technology.

Move to Kubernetes. Rewrite in Go. Adopt microservices. Upgrade the framework.

These projects frequently fail because they preserve technical behaviour without understanding business behaviour.

AI-native modernisation reverses the order.

First recover:

- Requirements
- Use cases
- Domain model

Then choose the implementation.

Technology becomes the final decision rather than the first.

## Regenerating instead of translating

Consider two approaches to replacing a legacy application.

**Traditional Migration**

```
Legacy Java
    ↓
Translate to C#
    ↓
Fix errors
    ↓
Deploy
```

Every historical mistake survives. Only the programming language changes.

**Specification-Driven Modernisation**

```
Legacy Java
    ↓
Recover Specifications
    ↓
Validate with Business
    ↓
Improve Architecture
    ↓
Generate New Implementation
    ↓
Deploy
```

Notice the difference. The second approach preserves business knowledge while discarding accidental implementation.

This is a much healthier form of evolution.

## AI as a modernisation partner

Simon Martinelli emphasises that AI should not simply rewrite code.

Instead, it should help recover the knowledge embedded within the existing system before generating a modern replacement.

This distinction is subtle, but it matters. Code translation changes the technology, while knowledge recovery changes the understanding, and understanding is what produces better software. Technology alone rarely does.

## The living specification

Once a module has been recovered, the next change no longer begins in code: it begins in the specification. The organisation has escaped one of the oldest traps in software engineering, and knowledge becomes explicit again. Future developers no longer need to perform archaeology; they read the specification instead.

## Legacy systems never disappear overnight

Some readers may hope AI enables complete rewrites.

Occasionally it does, but more often it enables something better: continuous modernisation.

Each sprint:

1. Recover one business capability
2. Validate it
3. Improve it
4. Generate better code
5. Deploy
6. Repeat

After several years the organisation possesses something it may never have had before.

A complete, living specification of its business.

## Beyond individual features

By this point in the book we have assembled a complete methodology.

We know how to:

- Capture requirements
- Write use cases
- Model domains
- Define architecture
- Create reusable skills
- Generate implementations
- Recover specifications from legacy systems

One question remains.

How does this methodology change the people involved?

If AI writes much of the implementation, what becomes of software engineers?

Do architects become more important?

Do business analysts disappear?

What new skills define the next generation of developers?

The final part of this book turns from process to people.

The greatest transformation AI brings is professional, not technical.
