# Chapter 7: Skills, Rules, and Context Engineering

Why Reusable Knowledge Is Replacing Prompt Libraries

> The goal is not to teach the AI every time you ask a question. The goal is to teach it once and let every future implementation benefit.

## The prompt engineering trap

When generative AI first entered software development, developers naturally focused on prompts.

Books were written about prompt engineering. Courses appeared. People collected elaborate prompt templates. Entire communities emerged around finding the "perfect prompt."

Many looked something like this:

> You are an expert senior software architect with twenty years of experience. Follow Clean Architecture. Write maintainable code. Use SOLID principles. Create comprehensive tests. Follow our naming conventions. Add logging. Use dependency injection. Don't duplicate code. Don't hallucinate...

Eventually these prompts became hundreds of lines long. Some exceeded several thousand words.

At first, this seemed like progress, but it was often a symptom of a deeper problem: the prompt was trying to compensate for missing project knowledge.

## The wrong place for knowledge

Imagine joining a new company.

On your first day, your manager says: "Every morning I'll explain our architecture, coding standards, security rules, naming conventions, testing strategy, logging policy, deployment process, and documentation requirements."

You might ask: "Couldn't you write that down once?"

Of course.

Humans learn organisational knowledge once and reuse it.

AI should work the same way.

Project knowledge belongs in reusable artefacts, not repeated conversations.

## Knowledge has different lifetimes

One of the most useful ways to organise AI context is by asking a simple question: How long will this information remain true?

Some knowledge changes every hour. Some changes every sprint. Some remains stable for years.

These different lifetimes deserve different homes.

For example:

**Permanent Knowledge**

- Architectural principles
- Coding standards
- Security policies
- Naming conventions
- Project structure

**Project Knowledge**

- Domain model
- Use cases
- Business rules
- APIs
- User interface specifications

**Task Knowledge**

- The feature currently being implemented
- Recent design decisions
- Temporary experiments

Early AI workflows mixed all three together.

Modern workflows separate them.

## What is a skill?

Simon Martinelli uses the term Skill to describe reusable implementation knowledge.

A skill is more than a prompt.

It is a structured capability that teaches an AI how a particular organisation builds software.

Instead of saying: "Remember to use constructor injection." every time, the skill already knows.

Instead of repeating: "Repositories belong in the infrastructure layer." the skill already knows.

Instead of describing the preferred testing framework, the skill already knows.

The conversation becomes simpler.

## Skills encode experience

Every experienced developer carries habits.

After twenty years of software engineering, you no longer consciously think about every decision. You instinctively know:

- Where classes belong
- How exceptions are handled
- When to write tests
- How APIs are structured
- Which design patterns fit

Skills attempt to capture this accumulated experience.

They become organisational memory.

## A Spring Boot skill

Imagine a company building Spring Boot applications.

Rather than repeating guidance for every feature, they create a reusable skill. The skill might include:

**Project Structure**

- Modular package layout
- Feature-first organisation

**Dependency Injection**

- Constructor injection only

**Persistence**

- Spring Data repositories

**Validation**

- Jakarta Validation

**Logging**

- Structured logging

**Testing**

- JUnit
- Testcontainers
- Integration tests for persistence

**Error Handling**

- Global exception handlers

**API Design**

- REST
- JSON
- RFC 7807 problem details

None of this relates to a particular feature.

It is reusable organisational knowledge.

## Different technologies need different skills

Now imagine another team.

Instead of Spring Boot, they use Quarkus.

Their skill changes.

Persistence differs. Configuration differs. Testing differs. Native compilation becomes important.

The business specifications remain identical, and only the implementation knowledge changes. That separation matters.

The same use case can generate completely different implementations simply by changing the active skill.

## Skills reduce cognitive load

Suppose you ask: Implement "Create Customer."

Without skills, the AI must decide:

- Should I use DTOs?
- Should I use records?
- Should I use services?
- Should I use repositories?
- Should I validate here?
- Should I create events?
- Should I add integration tests?

With skills, those questions disappear, and the implementation becomes almost mechanical. That consistency is what large organisations need.

## Skills are not architecture

Architecture defines constraints.

Skills define habits.

Consider this architectural rule: Domain objects may not depend on infrastructure.

Now consider a skill: Prefer immutable value objects.

One is a structural constraint. The other is an implementation preference.

Both matter.

They simply belong at different levels.

## The evolution of project knowledge

Many organisations progress through predictable stages.

**Stage 1.** Every developer writes their own prompts. Results vary wildly.

**Stage 2.** The team shares prompt templates. Consistency improves.

**Stage 3.** The organisation creates project instructions. Knowledge becomes reusable.

**Stage 4.** Skills emerge. The AI behaves like an experienced team member.

**Stage 5.** Skills become versioned organisational assets. New projects begin with years of accumulated implementation knowledge.

This is where AI-native organisations gain a lasting advantage.

## Small instructions, large knowledge

Simon Martinelli makes an important recommendation that initially seems counterintuitive.

Keep your global instructions small.

Many organisations continuously add new rules to a single instruction file until it grows to thousands of lines, loaded in full on every interaction.

This creates problems.

Large instruction files:

- Increase context usage
- Become difficult to maintain
- Contain contradictory guidance
- Encourage outdated rules to survive indefinitely

More importantly, they mix unrelated knowledge together.

A feature about appointments does not need payment gateway rules. A reporting module does not need authentication implementation details.

Knowledge should be modular.

## Modular knowledge

Imagine organisational knowledge as a library rather than a single book.

Instead of this:

```
GIANT_PROJECT_RULES.md
```

You have:

```
Architecture
Security
Testing
Spring Boot
React
Accessibility
Logging
Payments
Reporting
```

The AI retrieves only what is relevant to the current task.

This is both faster and more accurate.

## Context engineering

Prompt engineering asks: "How should I phrase my request?"

Context engineering asks: "What knowledge should the AI already possess before I ask?"

The difference matters.

The quality of AI output depends far less on clever wording than on complete, relevant context.

A weak prompt with excellent context often outperforms an excellent prompt with poor context.

## Retrieval instead of repetition

Modern AI systems increasingly retrieve knowledge when needed rather than carrying everything into every conversation.

Simon Martinelli points to the Model Context Protocol (MCP) as an example of this approach.

Instead of embedding thousands of lines of documentation into prompts, an AI can retrieve architectural guides, internal framework documentation, coding standards, or API references at the moment they are needed. This keeps the working context smaller while giving the model access to richer information.

Think of the difference.

A junior developer memorises documentation.

A senior developer knows where to find it.

AI is becoming more like the latter.

## Skills are living assets

A skill is not static.

Suppose your organisation adopts a new logging framework. You update one skill. Every future implementation immediately follows the new standard.

Suppose security requirements change. Update the security skill. Every generated feature benefits.

Instead of correcting hundreds of prompts, you improve one reusable asset.

The return on investment grows over time.

## Building an organisational memory

The most significant contribution of skills is that they preserve experience.

Every organisation has unwritten knowledge. Senior developers know it. New developers slowly discover it. Sometimes they never do.

When a senior engineer leaves, much of that knowledge leaves as well.

Skills transform tacit knowledge into explicit organisational assets.

They become a living memory of how the company builds software.

This is valuable for humans as well as AI.

## The complete context stack

At this point, we can see the complete hierarchy of information that drives AI-native development.

| Layer | Purpose | Changes |
|-------|---------|---------|
| Vision | Why the system exists | Rarely |
| Requirements | Business needs | Frequently |
| Use Cases | Behaviour | Frequently |
| Domain Model | Business concepts | Occasionally |
| Architecture | Structural constraints | Rarely |
| Skills | Implementation knowledge | Occasionally |
| Task | Current feature | Constantly |

Notice how each layer has a different rate of change.

This separation is deliberate.

Stable knowledge should stay untouched for long stretches, while changing knowledge belongs somewhere separate from permanent documentation.

## The end of prompt libraries

Prompt libraries solved an early problem.

They gave developers a repeatable starting point.

Skills solve a larger problem.

They capture how an organisation builds software.

The conversation with the AI becomes short.

Instead of describing everything repeatedly, the developer simply says:

Implement Use Case UC-12.

The AI already understands the business language, the architecture, the coding standards, the testing strategy, and the implementation conventions.

That is the promise of context engineering.

## Looking ahead

We now have nearly everything required to generate software: a clear business vision, well-defined requirements, structured system use cases, a shared domain model, architectural constraints, and reusable implementation skills.

The next step is to put these pieces together into a complete development workflow, from idea to running software, and see how specifications become executable.
