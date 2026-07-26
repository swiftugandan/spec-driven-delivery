# Foreword

## A lesson from the internet

In 1969, a computer scientist named Jon Postel began writing specifications for how computers could talk to each other.

He called them Requests for Comments. RFCs.

The specifications were modest. They defined what should happen. Not how. Not what technology to use. Just what should happen.

By 1983, TCP/IP was standardised as RFC 791 and RFC 793.

Today, fifty-one years later, those specifications have become the foundation of everything.

Your smartphone. Your car. Your bank. Your hospital. Your power grid.

Billions of devices. Trillions of connections. All built on protocols that predate Java, Python, Go, Rust, Docker, Kubernetes, and cloud computing.

Remarkably, the original specifications changed little while the implementations changed constantly.

COBOL computers implementing TCP/IP communicated with mainframes implementing TCP/IP. When Unix systems appeared, they implemented TCP/IP. When PCs arrived, they implemented TCP/IP. When the internet exploded, Windows, Linux, macOS all implemented TCP/IP. When cloud computing emerged, virtualised systems implemented TCP/IP. When containers appeared, containerised systems implemented TCP/IP. When IoT devices proliferated, they implemented TCP/IP.

Different technologies. Different eras. Different industries. Different companies.

All communicating with each other, because they shared something more valuable than code.

They shared a specification.

## The question this book answers

Fifty years after the internet proved that specifications are more durable than implementations, most organisations still build software the opposite way.

They treat source code as the primary artefact. They embed business knowledge in implementations. They lose that knowledge when technology changes. They rediscover it painfully when new people arrive.

Then they ask AI to build features without providing the knowledge AI needs.

The result is fast code that looks like it was written by a stranger.

This book asks a different question.

What if organisations applied the lessons of the internet to their internal software development?

What if they treated specifications as the primary artefact, the way the internet does?

What if they separated what the system should do from how it's implemented, the way RFCs separate protocol from implementation?

What if they understood that knowledge is durable, but technology is transient?

## Why this matters now

The internet's approach worked well for decades before AI.

But it works brilliantly with AI.

When you have a precise specification, an AI can implement it reliably. Different AI systems, different implementations, same behaviour.

When you don't have a specification, you're asking an AI to reverse-engineer intentions from vague requirements.

That's like asking someone to implement TCP/IP by reading a paragraph describing "how the internet should work."

It's nearly impossible.

## What this book offers

This is a guide to Simon Martinelli's methodology for building software in the age of artificial intelligence.

The central claim is simple.

Treat specifications, not source code, as your primary intellectual asset.

Organise knowledge into stable layers. Vision. Requirements. Use cases. Domain models. Architecture. Skills.

Provide all of this to AI. Ask it to implement.

Review the implementation. Deploy it.

When requirements change, update the specification and regenerate.

The code becomes reproducible. The specifications become durable. The knowledge becomes organisational memory.

This is an evolution, not a revolution, of ideas that have proven themselves over seventy years of structured software engineering.

What is new is the timing.

AI makes the economic case overwhelming.

When implementation takes weeks, the time to write specifications is expensive. When implementation takes minutes, that calculation flips.

Suddenly, investing in specifications before implementation becomes obviously rational.

## The historical validation

This book is built on two foundations.

**First:** Decades of software engineering practice. Structured analysis. Use cases. Domain-driven design. Agile. Architecture decision records.

These ideas are not new. They have proven themselves repeatedly.

**Second:** Fifty years of internet history. RFCs have proven that specifications can be more durable than implementations, that different technologies can implement the same protocol, that knowledge can outlive any particular tool or platform.

Rather than propose an untested theory, the book applies a proven model to internal software development at a moment when AI makes that model economically irresistible.

## Who should read this

If you build software, this book is for you.

If you manage people who build software, this book is for you.

If you depend on software, this book explains a better way to build it.

If you use AI to assist with coding, this book explains how to use AI effectively.

If you've ever lost knowledge when a senior engineer left, or watched a technology transition destroy institutional memory, this book offers an alternative.

## What you'll learn

**What specifications are** and why they matter more than code.

**How to capture them** through vision, requirements, use cases, and domain models.

**How to constrain them** through architecture and reusable skills.

**How to implement them** using AI.

**How to maintain them** as living artefacts that evolve with your business.

**How to apply them** to modernising legacy systems.

**How your role changes** as software engineering evolves toward knowledge engineering.

**What the long-term implications are** for organisations, careers, and the software industry itself.

## One warning

This book describes a different way of working.

It will not feel faster initially. Creating specifications takes time.

The speed advantage appears later, in changes, new features, team onboarding, and technology transitions.

This is a long-term bet.

But the payoff is multiplicative.

Organisations that master specification-driven development will, over five years, be five times more productive.

Over twenty years, fifty times more productive.

Not because they write more code, but because they preserve knowledge, avoid rediscovery, and enable technology changes without business disruption.

This is the same advantage the internet gained by standardising on protocols.

It's time for internal organisations to learn what the internet has known for five decades.

## The invitation

The future of software engineering belongs to organisations that understand their business most deeply, not to those that write code fastest.

Code is how you express that understanding. Specifications are how you preserve it.

AI is how you scale it.

This book is an invitation to start that journey.

---

*The methodology presented here builds on decades of software engineering practice and fifty years of internet history. It applies proven principles at a moment when AI makes that application both possible and economically necessary, rather than speculating about a possible future.*

*Everything you need to transform how your organisation builds software is in the chapters that follow.*
