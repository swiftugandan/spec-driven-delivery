# Essay: RFCs as the Template for Specification-Driven Development

## The model that built the internet

Before everything else, before implementation, before optimization, before any code was written, the internet was built on a simple idea.

Write down what you want the protocol to do. Make it clear. Make it precise. Make it durable.

Then everyone implements it. In whatever language they want. On whatever platform they want. Using whatever technology suits them.

That idea is the RFC.

Request for Comments.

It sounds modest. The name itself suggests tentativeness. Yet RFCs have become the foundation upon which billions of devices communicate. TCP/IP works because of RFC 791. HTTP works because of RFC 7230. SMTP works because of RFC 5321.

Not because everyone used the same language, framework, or architectural choices, but because everyone agreed on the specification.

## What RFCs actually are

An RFC is a published memorandum describing a proposed Internet standard or best practice.

It specifies:

**Exact behaviour.** What should happen in every case? What are the edge cases?

**Protocol details.** How do actors communicate? What are the message formats?

**State machines.** What transitions are allowed? What states can be occupied?

**Error handling.** What happens when things go wrong?

**Constraints and assumptions.** What must be true for this to work?

**Examples.** Concrete illustrations of the protocol in action.

An RFC is a specification, not an implementation, code, or product design document, and it has proven to be one of humanity's most successful coordination mechanisms.

## Why RFCs work

RFCs work for a deceptively simple reason.

They separate what from how.

An RFC specifies *what the protocol does*.

Implementations decide *how to achieve it*.

Consider HTTP, defined in RFC 7230.

The RFC says: "A server must respond to a GET request with a status line, headers, and optional body."

The RFC does not say to use Java with Spring Boot, store state in PostgreSQL, or deploy on Kubernetes.

Every HTTP server implementation decides those things independently.

A web server written in Go in 2024 communicates flawlessly with a server written in C in 1995, not because they share implementation details, but because they share a specification.

## The interoperability miracle

This separation is the root of the internet's greatest achievement.

Interoperability.

Different systems, built by different teams, in different decades, using different technologies, can communicate smoothly.

A smartphone running iOS talks to a server running Linux running an old Java application talking to a mainframe running COBOL. None of them know what technology the others use. They don't need to.

They agree on the specification.

It's achieved purely through disciplined specification, not through technological unity.

## Translating RFCs to internal development

Now apply this to an organisation building internal software.

An organisation's domain knowledge is like the internet's protocols. It is durable. It should outlive technologies.

A bank's loan approval process should survive multiple technology transitions. A hospital's patient management workflow should work whether implemented in Java or Go or Rust. An e-commerce system's order processing should be implementable in any framework.

Most organisations do not treat domain knowledge this way. They entangle it with implementation. They lose it when technology changes. They rediscover it when new developers arrive.

What if organisations adopted the RFC model?

## The specification as RFC

Imagine treating a specification like an RFC.

The domain model becomes the "protocol." It defines what entities exist and how they relate: the "message format" of the business.

Use cases become the "state machine." They define what sequences of events are valid: the "protocol flow."

Business rules become the "constraints." They define what must be true: the "error handling" of the specification.

Architecture becomes the "assumptions." It defines structural boundaries that all implementations must respect.

Then implementations are like HTTP servers: they can use any language, framework, database, or deployment platform.

As long as they conform to the specification, they work.

## What gets invented vs. what gets preserved

RFCs achieve their power through ruthless discipline about what must be preserved and what can vary.

What must be preserved:

- Protocol behaviour
- Message formats
- State transitions
- Error responses

What can vary:

- Implementation language
- Data structures
- Performance optimisations
- Deployment approach

This distinction is crucial. If an RFC tried to preserve implementation details, it would fail. Immediately.

An RFC that said "all HTTP servers must use Java and PostgreSQL" would be useless. The moment a faster implementation in Go appeared, everyone would abandon it.

Yet organisations often do exactly this in reverse. They preserve implementation details (the technology stack) but let specifications dissolve into code comments.

## Regenerating from RFCs

RFCs enable something remarkable: regeneration.

If a new protocol version emerges, implementations don't require hand-editing. They can be regenerated from the new specification.

Consider the history of TLS. TLS 1.0 → 1.1 → 1.2 → 1.3.

No HTTP server implementation needed to be hand-edited.

The specification changed. Implementations were updated to match the new spec. Some were rewritten. Some were generated. Some were modified. But all derived from the same source of truth: the RFC.

This is what specification-driven development enables for organisations.

When requirements change, regenerate.

When architecture evolves, regenerate.

When frameworks become outdated, regenerate.

The specification is the source of truth.

## The economics of RFC-based development

RFCs are economically superior because they enable reuse at a level ordinary code cannot.

A single RFC (TCP/IP) has enabled thousands of implementations, billions of devices, and trillions of network connections.

Compare the ROI of that specification against the cost of any single implementation.

The same applies internally. A well-specified domain model, encoded as an organisational "RFC," can generate dozens of implementations, support dozens of teams, evolve across decades.

The investment in the specification pays dividends continuously.

## Why organisations resist this model

If RFCs work so well for the internet, why don't organisations use them internally?

Several reasons stand out.

**Culture.** Software engineering culture values implementation. Building things. Shipping features. RFCs feel like bureaucracy compared to "just coding."

**Immediacy.** Writing an RFC takes time. Building features feels faster. The pressure to ship creates bias toward implementation-first approaches.

**Feedback loops.** The internet's feedback loop for RFCs is decades long. Organisations operate in sprint cycles. The long-term benefits of good specifications are invisible against the short-term pressure to deliver.

**Knowledge.** Most organisations lack experience with specification-based development. They assume it's harder than it is.

**Tooling.** The internet has RFC repositories, standards bodies, and formal processes. Most organisations lack the tools and discipline to maintain living specifications.

## What's required to adopt the RFC model

Adopting this model requires several capabilities.

**Specification discipline.** Treating specifications as primary artefacts. Maintaining them. Versioning them. Reviewing them.

**Architect leadership.** Architects who understand that their job is to preserve knowledge across implementation generations, not to choose technologies.

**Business involvement.** Business stakeholders who understand that specifications are how organisational knowledge is made explicit.

**Tool support.** Systems to version, review, and search specifications. Ways to generate implementations from specifications.

**Cultural shift.** Valuing precision and understanding over speed and features.

**Patience.** Accepting that the first few cycles are slower. The payoff comes later.

## The parallel to microservices architecture

Microservices architecture has rediscovered some of this thinking.

Microservices succeed when:

- Services have well-defined interfaces (specifications)
- Services can be implemented independently
- Services communicate through agreed protocols (RFCs)
- Technology choices vary across services

Microservices struggle when:

- Interfaces are unclear
- Services are tightly coupled to shared implementations
- Protocol details are undocumented
- Services are forced to use identical technology stacks

The successful microservices organisations are essentially applying the RFC model within their system architecture.

## From internet protocols to organisational protocols

The leap is to treat organisational knowledge with the same respect the internet treats protocols.

A bank's loan approval process is a protocol. It should be specified like an RFC. Different implementations should be possible. Future changes should be managed through specification versioning, not code editing.

A hospital's patient workflow is a protocol. It should survive technology transitions. It should be implementable in different systems. It should be testable against a specification.

An e-commerce platform's order processing is a protocol. It should be independent of technology choices. It should be regenerable. It should survive decades of framework evolution.

## The specification economy, reconsidered

This brings us back to the central claim of this book.

Organisations will increasingly value knowledge over code.

RFCs prove this thesis at global scale.

The internet's value does not come from the source code of individual implementations. It comes from the specifications that enable incompatible systems to interoperate.

The same principle applies internally.

The value of an organisation's software does not ultimately reside in the codebase. It resides in the knowledge encoded in specifications.

That knowledge:

- Outlives technologies
- Can be implemented multiple ways
- Can be evolved without destroying existing implementations
- Can be understood by humans and executed by machines
- Creates competitive advantage precisely because it is durable

## A historical validation

This idea has fifty years of history behind it. RFCs have worked this way across billions of devices, thousands of organisations, and infinite implementations.

All grounded in the principle: the specification is the source of truth.

What Martinelli proposes for internal software development applies a model that has already proven itself at the largest possible scale.

The internet is the most successful software system humanity has created, and it succeeded because of the rigour of its specifications, not despite it.

## Conclusion

When you understand RFCs, you understand why specification-driven development works.

When you adopt specification-driven development, you inherit the lessons of fifty years of internet architecture, validated in practice at a scale most individual organisations can barely imagine.

The real question is why we ever stopped treating specifications as the source of truth.
