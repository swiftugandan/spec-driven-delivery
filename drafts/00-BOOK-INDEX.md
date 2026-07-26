# Specification-Driven Development with AI

## A Complete Guide to Simon Martinelli's Methodology

---

## Quick navigation

### Front matter
- [Foreword](./00-FOREWORD.md) — The RFC model as historical precedent
- [Case Studies](./01-CASE-STUDIES.md) — Five real-world implementations

### Core book: 11 chapters + afterword

**Part 1: Foundation** — Building the case and establishing what needs to be built
- [Chapter 1: The Promise and Peril](./chapter-01-introduction.md) — Why AI produces bad code without context
- [Chapter 2: Vision and Purpose](./chapter-02-vision-purpose.md) — Understanding why a system exists
- [Chapter 3: Requirements and Use Cases](./chapter-03-requirements-use-cases.md) — Specifying what the system does
- [Chapter 4: Domain Modeling](./chapter-04-domain-modeling.md) — Understanding business objects and relationships
- [Chapter 5: Bringing It Together](./chapter-05-bringing-together.md) — How all layers work in concert

**Part 2: Framework** — How to build systems with AI
- [Chapter 6: Architecture as Context](./chapter-06-architecture-as-context.md) — Constraints guide AI behavior
- [Chapter 7: Skills, Rules, and Context Engineering](./chapter-07-skills-rules-context.md) — Reusable implementation knowledge
- [Chapter 8: From Specification to Software](./chapter-08-specification-to-software.md) — The complete workflow

**Part 3: Practice and Implications** — Real-world application and the future
- [Chapter 9: Brownfield Development](./chapter-09-brownfield-development.md) — Modernizing legacy systems
- [Chapter 10: The Future Software Engineer](./chapter-10-future-engineer.md) — How roles evolve
- [Chapter 11: The Specification Economy](./chapter-11-specification-economy.md) — Long-term shifts in software value

[Afterword](./afterword.md) — Final reflection on knowledge as the durable asset

---

### Supplementary materials

**Historical Precedent**
- [Essay: RFCs as Template for Specification-Driven Development](./essay-rfcs-as-precedent.md) — How internet protocols validate the methodology at massive scale

**Practical Application**
- [Guide: Organisational RFCs in Practice](./guide-organisational-rfcs.md) — Concrete example of how to structure domain specifications

---

## Key concepts at a glance

### The core thesis

> The future of software engineering belongs to organisations that treat **specifications, not source code, as their primary intellectual asset**.

### The specification stack

Each layer answers different questions and has different rates of change:

| Layer | Answers | Changes |
|-------|---------|---------|
| **Vision** | Why does this system exist? | Rarely |
| **Requirements** | What observable behaviour is needed? | Frequently |
| **Use Cases** | What is the complete user interaction? | Frequently |
| **Domain Model** | What business entities and relationships exist? | Occasionally |
| **Architecture** | What structural constraints guide implementation? | Rarely |
| **Skills** | How does this organisation implement things? | Occasionally |
| **Implementation** | What code expresses all of the above? | Constantly |

### The knowledge pipeline

```
Vision
    ↓
Requirements
    ↓
Use Cases
    ↓
Domain Model
    ↓
Architecture + Skills
    ↓
AI Implementation
    ↓
Testing
    ↓
Review
    ↓
Deployment
```

Each stage reduces uncertainty. Each stage removes decisions the AI must invent.

### Why specifications matter more than code

- **Code is transient.** Technology changes, frameworks are replaced, languages evolve.
- **Specifications are durable.** The knowledge they encode persists across technological transitions.
- **Code is an implementation detail.** One possible expression of a specification.
- **Specifications enable regeneration.** Change the spec, regenerate the code. Don't hand-edit implementations.
- **Specifications enable interoperability.** Different implementations can coexist if they follow the same spec.

### The RFC connection

The methodology is essentially applying the RFC (Request for Comments) model, which has powered the internet for 50 years, to internal software development.

Just as:
- HTTP implementations in Go, Python, Java all communicate because they conform to RFC 7230
- Different storage technologies work together because they follow SMTP (RFC 5321)
- The entire internet's interoperability rests on specifications, not technology uniformity

So too can internal systems:
- Different implementations of the same business process can coexist
- Technology can be replaced without breaking the system
- Knowledge survives framework and language changes
- Specifications become the source of truth

---

## Three problem statements and solutions

### Problem 1: speed paradox
**The Problem:** AI can generate code faster than humans can read it, yet experienced developers reject the code as unsuitable.

**The Root Cause:** The code "belongs in a different project" because it was written without organisational context.

**The Solution:** Provide explicit context through specifications before asking AI to implement.

---

### Problem 2: knowledge loss
**The Problem:** Organisations repeatedly lose institutional knowledge when employees leave, projects finish, or technology changes.

**The Root Cause:** Knowledge is embedded in code, not in explicit specifications. Code is fragile and transient.

**The Solution:** Make knowledge explicit through specifications that persist independent of implementation.

---

### Problem 3: change management
**The Problem:** Updating hand-written code to reflect requirement changes is expensive and error-prone.

**The Root Cause:** Code and specifications are disconnected. Changing one doesn't automatically update the other.

**The Solution:** Treat specifications as the source of truth. Regenerate implementations from updated specifications rather than hand-editing code.

---

## How to read this book

### For software engineers
Start with **Chapter 1** (why this matters), then **Chapters 6-8** (how to build with AI). Later, read **Chapter 10** to understand how your role evolves.

### For architects
Start with **Chapter 2** (vision), then **Chapters 6-7** (architecture and skills). These are your primary concerns. **Chapter 11** shows how architecture becomes more strategic.

### For business stakeholders
Start with **Chapter 2** (vision and requirements), then **Chapter 3** (use cases). These directly impact your domain. Skip the technical chapters unless curious.

### For managers
Read **Chapter 1** (the case for change), **Chapter 8** (the workflow), and **Chapter 10** (team implications). Understand how work reorganises around specifications.

### For everyone
Read the **Essay on RFCs** (supplementary). It validates the entire approach using a proven model most people haven't considered.

---

## The methodology in ten steps

When implementing specification-driven development:

1. **Define Vision** — Why does this system exist?
2. **Capture Requirements** — What observable behaviours are needed?
3. **Write Use Cases** — What are the complete user interactions?
4. **Model Domain** — What business entities and relationships exist?
5. **Establish Architecture** — What structural constraints guide implementation?
6. **Define Skills** — How does this organisation implement things?
7. **Generate Implementation** — Run AI with all the above context
8. **Generate Tests** — Tests validate that implementation matches specification
9. **Human Review** — Validate correctness and business alignment
10. **Deploy** — Use standard processes

When requirements change:
- Update the specification (not the code)
- Regenerate the implementation
- Re-test
- Repeat

---

## Key questions answered

**Q: Won't this create more documentation overhead?**

A: Initially yes. Over time, no. The cost of maintaining specifications is vastly lower than the cost of hand-editing code when requirements change. The ROI compounds over time.

**Q: What if the AI misunderstands the specification?**

A: That's possible. That's why human review remains essential. But if the AI misunderstands, it's easier to clarify the specification than to debug code.

**Q: Does this work for legacy systems?**

A: Yes. Chapter 9 covers brownfield development. Start by reverse-engineering specifications from existing code. Then modernize incrementally.

**Q: What about systems where we don't know the requirements?**

A: Specifications are discovered iteratively. Start with what you know. Build, learn, refine. This is compatible with Agile.

**Q: Will this eliminate software engineering jobs?**

A: No. It will shift them. Less time writing boilerplate, more time understanding problems and improving specifications. More human, not less.

**Q: How do I get started?**

A: Pick a small feature. Write a use case. Write a domain model. Provide architecture context. Ask AI to implement. See what happens. Iterate from there.

---

## For different technology stacks

The methodology is technology-agnostic. All of these approaches work:

- **Spring Boot with React** — Define Spring Boot skills, React skills, generate for both
- **Python with Django** — Define Django architecture, Python conventions, generate
- **Go microservices** — Define architecture as Self-Contained Systems, Go conventions
- **Node.js full-stack** — Define Node architecture, React/Vue skills, generate
- **Legacy Java migration** — Reverse engineer specifications from old code, generate new Java
- **Multi-language systems** — Define shared specifications, generate different implementations

The specification is primary. Technology is secondary.

---

## Measuring success

When you've successfully adopted specification-driven development:

- Specifications are version-controlled alongside code
- Code is treated as generated rather than hand-written
- Changing requirements means updating specs, not editing code
- New developers read specifications to understand the system
- AI generates consistent code without surprises
- Technical debt is measured as knowledge debt, not just code quality
- Architecture decisions are explicit and reusable across projects
- Requirements are never vague because they must be executable

---

## The central economic argument

Traditional software development optimizes for implementation speed.

Specification-driven development optimizes for knowledge durability.

Over a 5-year horizon:
- Specification-driven is slower initially
- But faster on changes, faster on new features, faster on team onboarding

Over a 20-year horizon:
- Specification-driven dominates
- Knowledge is preserved
- Technology can be replaced
- New teams inherit understanding
- The organisation doesn't lose what it learns

---

## Resources provided

This package includes 11 full chapters (12,000+ words), a detailed afterword, an essay connecting the methodology to internet RFCs, a practical guide to organisational RFCs with a concrete example, and this index and navigation guide.

All files are standalone markdown that can be:
- Read in order or by topic
- Published as a web book
- Included in documentation systems
- Referenced by practitioners
- Adapted for your organisation

---

## The invitation

This book is an invitation to think about software as knowledge, not code.

Code expresses knowledge. Specifications preserve it. Architecture enables it. Skills operationalise it. AI implements it.

The organisations that master this will build more, faster, with less waste, and without losing what they've learned. That future starts with treating specifications as the primary artifact. Everything else follows.

---

*For questions, comments, or to share your implementation experience, see the original source material by Simon Martinelli and community discussions around specification-driven development.*
