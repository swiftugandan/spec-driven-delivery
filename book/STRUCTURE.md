# Specification-Driven Development

## Working subtitle

How to make AI implementation reliable by treating specifications, not code, as the asset that lasts

## Promise

After this book, you can write a specification (vision, requirements, use cases, a domain model, architecture constraints, and reusable implementation skills) precise enough that an AI assistant implements a feature correctly on the first pass instead of guessing, and you can apply the same discipline in reverse to recover a working specification from a legacy system that never had one.

## Audience

- Software engineers and tech leads who use AI coding assistants daily and are tired of rewriting what they generate
- Software architects responsible for keeping many AI-assisted teams consistent with each other
- Engineering managers deciding how their team should adopt AI-assisted development

**Not the audience:** readers who want a business case for AI adoption without technical detail, or a prompt-engineering cookbook. Point them to the Foreword and Appendix A (case studies) only, or elsewhere.

## Reading paths

**Practitioner:** Chapters 1–11 in order
The complete methodology, front to back, for someone about to apply it to their own feature or team.

**Architect:** Foreword, Chapters 2, 4, 6, 7, 11, Appendix C
Vision through architecture and skills, plus the fully worked specification template, for a reader who owns consistency across teams rather than a single feature. Chapters 3 and 9 supply evidence this path depends on: Chapter 4 and Appendix C both work from Chapter 3's Schedule Appointment use case and booking rules, and Chapter 11 argues from the ledger recovered in Chapter 9. The printed reading-paths page tells this reader to take those two chapters first if either is unfamiliar.

**Manager:** Foreword, Chapter 1, Appendix A, Chapter 8, Chapter 10, Afterword
The case for the change and its effect on team structure and roles, without the specification-writing detail.

## Running examples

### Primary: Riverside Clinics appointment scheduling

A multi-location clinic group needs a way for patients to book appointments online. It starts under-specified, a one-line request to "let patients book appointments," and the book grows it: a vision that names the real barrier to booking, requirements that pin down what "available" means, a use case for the booking flow, a domain model for patients, doctors, and time slots, architecture constraints once a second team joins the project, and a versioned specification a third team can implement independently.

### Variant: a bank's core ledger migration

A retail bank's account-management system has run on the same COBOL codebase since the late 1980s. Nobody currently at the bank designed it, and its rules survive only as behavior. This variant stresses what the clinic example cannot: recovering a specification from code instead of writing one from scratch, and carrying that specification through a technology change the original authors never anticipated.

---

# Part 1: Foundation

## Chapter 1: Why AI needs a specification, not a prompt

**Question:** Why does asking AI to build a feature from a short description produce code a team can't keep?

- A team asks AI to build an order-management feature; the result works, and the team rejects it anyway
- The rejection is about code written for a different project, not broken code
- Developers were never the bottleneck; understanding what to build was, and AI has only made that gap visible
- Two different requests look similar but aren't: "build a feature" asks AI to guess business intent; "implement this use case" asks it to translate a decision already made
- Shifting effort from implementation to specification changes what improves, and by how much

**Field guide:** A two-column test for telling a specification-shaped request from a guessing-shaped one
**Primary example:** The Riverside Clinics booking request arrives as a one-line, under-specified ask

## Chapter 2: Why purpose comes before design

**Question:** Why does skipping the vision step cost more than writing the vision would have?

- A vision answers why a system exists and for whom, not what it does
- A vision statement that only restates the feature request hides the actual problem
- A stakeholder conversation surfaces the real barrier to booking, which the original request never mentioned
- Vision constrains scope, and constrains it before architecture decisions lock anything in
- Vision scales: a feature, a product, and an organization each need one, at different grain

**Field guide:** A vision-document outline (problem, stakeholders, scope, approach, success criteria, constraints)
**Primary example:** Writing the Riverside Clinics booking vision, badly first and then well

## Chapter 3: Specifying what the system must do

**Question:** How do you turn a vision into requirements an AI assistant can't misread?

- A good requirement is observable, testable, and silent on implementation
- A requirements workshop negotiates a concrete rule (a 90-day booking horizon) that the vague version of the request left open
- A use case, not a requirement list, is the unit AI implements best, because it specifies a complete interaction rather than a property
- The standard use-case shape: actor, preconditions, main scenario, alternative flows, postconditions, business rules
- User stories and use cases serve different purposes: one plans work, the other drives implementation

**Field guide:** A use-case template with a worked example filled in
**Primary example:** The "Schedule Appointment" use case for Riverside Clinics, written start to finish

## Chapter 4: Modeling the business objects a system runs on

**Question:** What must AI know about your business objects before it can implement anything correctly?

- Without a domain model, AI invents entities, attributes, and relationships, and most of its guesses are wrong
- A domain model describes business meaning, not how anything is stored
- Entities, value objects, and enumerations each capture a different kind of business fact
- The Riverside Clinics domain model: patients, doctors, appointments, and the constraints between them
- A domain model changes as the business changes, and the specification changes with it

**Field guide:** A checklist for telling an entity from a value object
**Primary example:** Modeling patients, doctors, and appointments for Riverside Clinics

## Chapter 5: Bringing the specification together

**Question:** How do the first four layers combine into a specification AI can implement directly?

- Each layer answers a different question, and a complete specification needs all of them
- Walking the Riverside Clinics example through all four layers as one connected document
- The specification, not the generated code, becomes the source of truth going forward
- Maintaining a specification costs time, and that cost is repaid the first time a requirement changes
- A preview of what the next three chapters add: architecture and reusable skills

**Field guide:** A one-page template for assembling the four layers into a single specification
**Primary example:** The complete Riverside Clinics booking specification, vision through domain model

---

# Part 2: Framework

## Chapter 6: Architecture as context

**Question:** How do structural constraints keep AI-generated code consistent with everything around it?

- AI-generated code can be entirely correct and still be wrong for the project, because nobody told it the project's structural rules
- Every codebase has invisible rules; three developers naming the same class three different ways is what happens when nobody wrote them down
- Architecture is the set of decisions, layering, dependency direction, naming, module boundaries, that apply to every feature, not just one
- The dependency rule and layered architecture, applied to the Riverside Clinics codebase
- Documenting architecture with existing tools (arc42, architecture decision records, C4) rather than inventing a new format
- The shift from prompt engineering to context engineering: giving AI the rules once, in writing, instead of re-explaining them every time

**Field guide:** An architecture-documentation outline scaled to a single team
**Primary example:** Naming and dependency rules for Riverside Clinics, made explicit for the first time

## Chapter 7: Skills: reusable implementation knowledge

**Question:** How do you encode a team's implementation conventions once instead of repeating them in every prompt?

- A prompt that tries to specify testing, logging, error handling, and naming all at once is a symptom: the knowledge belongs in the project, not the request
- A skill is reusable implementation knowledge: how this organization writes tests, handles errors, structures a service
- The same use case, implemented against a Spring Boot skill and then a Quarkus skill, produces two different but equally correct results
- Why large, all-purpose instruction files work worse than several small, specific skills
- Skills as versioned, living documents that compound in value as more features are built against them

**Field guide:** A worked skill definition (persistence, validation, logging, testing, error handling) for one stack
**Primary example:** A Spring Boot implementation skill for the Riverside Clinics booking feature

## Chapter 8: From specification to software

**Question:** What does the complete workflow from specification to deployed software look like in practice?

- Two teams building the same feature under the same deadline: one prepared, one improvising with AI
- The difference between them is preparation, not which AI model either one used
- Walking the full ten-stage workflow using the Riverside Clinics booking specification as the running case
- Testing validates that the implementation matches the specification, not just that the code runs
- Review effort should scale with business risk, not with how much code AI produced
- What "done" means changes: a complete specification becomes part of the definition, not an afterthought

**Field guide:** A workflow checklist from specification draft to deployed feature
**Primary example:** Riverside Clinics booking, specification to shipped feature, stage by stage

---

# Part 3: Practice and implications

## Chapter 9: Brownfield development

**Question:** How do you recover a usable specification from a system that never had one written down?

- Most engineers spend their careers maintaining existing systems, not building new ones
- Code is a poor place to store business knowledge: a line like `customer.getStatus() == 7` has lost whatever it once meant
- Treating a legacy system as something to read before it's something to replace
- AI's most useful role here is archaeological: surfacing suspicious complexity for a human to judge, not rewriting on its own authority
- A recovered specification from the bank's core ledger, business rule by business rule, disagreement by disagreement
- Recover, validate, improve, then generate: a different sequence from a straight line-for-line migration

**Field guide:** A specification-recovery checklist for reading an undocumented system
**Primary example:** Recovering a use case from the bank's core ledger migration

## Chapter 10: The future engineer

**Question:** How does the day-to-day work of a software engineer change once implementation is largely automated?

- Every abstraction that removed manual work, compilers, fourth-generation languages, low-code, raised the same fear, and none of them eliminated the engineer
- What moves from scarce to automated is syntax; what stays scarce is judgment about what the system should do
- Domain knowledge becomes a bigger advantage than syntax fluency
- Code review shifts from checking syntax to checking intent against specification
- What AI does not easily replace: negotiation, ethics, leadership, and specific domain expertise
- A specification can be entirely correct and still admit three different valid implementations; choosing between them is still engineering judgment

**Field guide:** A self-assessment for where a reader's current skills sit on the syntax-to-judgment shift
**Primary example:** Three engineers, three valid implementations of the same Riverside Clinics use case

## Chapter 11: The specification economy

**Question:** What changes in software economics once specifications, not code, are the asset that persists?

- Every prior shift in computing moved the primary asset: hardware, then software, then platforms
- Stealing a competitor's codebase would not reproduce their business, because the business logic that matters survives in decisions, not syntax
- The bank's ledger specification outlives COBOL, then Java, then whatever replaces Java after that
- A specification becomes something an organization can protect and reuse the way it currently protects code
- What stays speculative here and why: regenerable software and specification-first tooling are not yet common practice
- The competitive advantage shifts toward whoever understands their own business most precisely, not whoever ships code fastest

**Field guide:** A set of questions for identifying where an organization's knowledge currently lives only in code
**Primary example:** The bank's ledger specification, carried across three technology generations

---

# Back matter

## Appendix A: Case studies

- A bank's COBOL-to-Java migration for a 200,000-customer account system
- A healthcare network's appointment system spanning 40 clinics and 500 doctors
- An e-commerce platform's shift from ad hoc AI use to specification-driven features
- An enterprise's replacement of a 150-page standards document with protocol-style specifications
- A government agency's phased recovery of a benefits-processing system last touched in 1995
- Each case is presented as reported by the organizations involved, with names and identifying details changed; treat the specific figures as reported outcomes from a single engagement, not as guaranteed or typical results

## Appendix B: RFCs as precedent

- Why internet protocols separate what a system does from how any one implementation builds it
- Reading RFC 791, RFC 793, and RFC 7230 as specifications that have outlived every implementation written against them
- The direct mapping: domain model to protocol, use case to state machine, business rule to constraint
- Why most organizations have not adopted this discipline internally, and what adopting it actually requires

## Appendix C: A worked organizational specification

- A complete, implementable specification for the Riverside Clinics booking feature, in the same format an internal RFC would use
- Protocol messages, consistency rules, notification behavior, and the enumerations that constrain valid state
- Implementation notes covering persistence, idempotency, clock skew, and testing
- A versioning example showing how the specification changes when new capability (recurring appointments, multi-clinic booking) is added later

## Glossary

Terms defined on first use in the body, collected here: specification, vision, requirement, use case, domain model, value object, architecture, skill, context, protocol, implementation.

## Notes and references

- Attributed reported practice: Simon Martinelli's specification-driven development methodology, cited throughout as the source of the book's core recommendations
- Cited standards: RFC 791 (still STD 5), RFC 793 and RFC 7230 as the historical documents the argument turns on, with their 2022 successors RFC 9293 (STD 7) and RFC 9112 plus RFC 9110 recorded alongside them, RFC 5321, RFC 5322, RFC 3339
- Cited established practice: Eric Evans's domain-driven design, the Agile Manifesto, architecture decision records, arc42, the C4 model, the Model Context Protocol, Martin Fowler's Strangler Fig pattern
- A note on the case studies in Appendix A: presented as reported by the organizations involved; the aggregate percentage ranges that appeared in this book's original packaging material are not carried forward, since they do not trace back to the individual case figures

## Index

- Concepts
- Artifacts and templates
- Examples
- Risks and failure modes

---

# Standard chapter pattern

Each chapter uses this sequence. Beats marked *(where it fits)* may be omitted
when the chapter does not need them; the rest are required.

1. Opening situation
2. Chapter promise and reading time
3. Problem and consequences
4. Core concept in plain language
5. Step-by-step method
6. Primary worked example
7. Variant example *(where it fits)*
8. Failure modes and limitations
9. Reusable field guide
10. What to remember
11. Questions for the reader's team *(where it fits)*
12. One action to take next
13. Transition to the next chapter

# Page budget

- Front matter (cover, title, copyright, table of contents, preface, how to read this book, foreword): 13 pages (estimated 10–14)
- Part 1 (Chapters 1–5): 43 pages (estimated 75–95; the estimate assumed longer chapters than the drafted prose needed)
- Part 2 (Chapters 6–8): 28 pages (estimated 48–60)
- Part 3 (Chapters 9–11): 26 pages (estimated 48–60)
- Back matter (afterword, three appendices, glossary, notes and references, index): 38 pages (estimated 45–60)
- **Actual total: 148 pages** (verified by `bookkit.verify`), against an initial estimate of 226–289. The gap is a planning-estimate miss, not a structural problem: every chapter still covers its full beat list per `chapter-pattern.md`, and `bookkit.verify` raised no page-budget drift as a failure.
