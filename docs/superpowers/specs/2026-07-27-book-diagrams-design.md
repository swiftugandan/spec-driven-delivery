# Five diagrams for Specification-Driven Development

Date: 2026-07-27

## Problem

The book argues its case entirely in prose. Five of its claims are about the
*relationship* between things rather than about a sequence of items, and prose
is the wrong instrument for those five. A reader has to hold four documents in
mind at once to see Chapter 5's thesis, and hold ten list items in mind to see
which of them repeat.

## Scope

Five inline SVG diagrams, in Chapters 1, 4, 5, 8 and 9. No other chapter gets
one. Chapter 6 (dependency direction) and Chapter 11 (one specification across
three technology generations) were considered and cut: Chapter 6's stack would
read as a house style applied twice next to Chapter 5's, and Chapter 11's
timeline is a list of three with dates on it.

Prose is not deleted to make room. Each diagram is added alongside the material
it illustrates; where the page has no slack, the page splits and the book grows.
The prose has been through three editorial rounds and a content punch list, and
cutting to fit reopens work that is already settled.

## The five

### Chapter 1 — One Request, Two Paths

Archetype: flow, branching. Page: "Guessing Requests and Specification
Requests".

A single feature-request node splits two ways. The guessing-shaped path reaches
code that runs and then a **dashed** return arrow to rework. The
specification-shaped path reaches code the team keeps. The dashed rework loop
is the chapter's opening scene, and dashing rather than colouring it keeps it
reading as exceptional in greyscale.

### Chapter 4 — Riverside Clinics Domain Model

Archetype: node map. Page: "Worked Example: The Riverside Clinics Domain Model".

Patient, Doctor, Clinic and Appointment are squared entity boxes. TimeSlot is
rounded, because shape is the channel that separates a value object from an
entity once both fills print as the same grey. The status enumeration sits in a
pale band listing its four values. Every line carries a cardinality; the
Doctor–Clinic line carries `stroke-width="2"` and the label *many-to-many*,
because that one relationship is what the chapter's failure story turns on.

### Chapter 5 — One Fact Through Four Layers

Archetype: layered stack with a trace. Page: "Worked Example, Concluded: The
Domain Model".

Four bands — vision, requirements, use case, domain model — with one heavy
trace running down them, carrying the doctor-works-at-many-clinics fact in the
form it takes at each level: a plain-language sentence, then REQ-07's second
condition, then the filter applied before display, then the many-to-many
relationship. This is the book's central claim and it currently exists as a
single paragraph.

### Chapter 8 — Six Written Once, Four Repeated

Archetype: pipeline with a return loop. Page: "The Five-Stage Workflow".

Stages 1 through 6 in a band marked *written once, reused across every use
case*; stages 7 through 10 in a band marked *repeats per use case*, with a
solid return arrow from deployment through a specification-review gate back
into implementation. The flat ten-item list cannot show that split, and the
split is what the page's own principle line asserts.

### Chapter 9 — Recover, Validate, Improve, Generate

Archetype: flow with a dashed dead end. Page: "The Four-Stage Recovery Method".

Recover, then draft with flags, then validate, then generate. Validate branches:
*confirmed* continues solid to generate; *disputed* runs **dashed to a terminal
node** naming a human decision owner, and never reaches generate. The dead end
is the argument. BR-3 is not something more code-reading settles.

## Constraints these are drawn under

- One user unit is one point. Maximum width 410.4 units, the 5.7in text measure
  at the book's 7 × 10in trim with 0.65in margins.
- Every fill and stroke is `var(--token, fallback)`. Inline in a page file the
  token resolves to the book's palette, so a diagram retargets when the book
  does.
- The palette carries three tonal levels, not seven colours. `--accent` against
  `--support` is 1.14:1 in greyscale. A fourth category needs a dash pattern, a
  stroke weight, a shape change, or a label.
- `role="img"` and an `aria-label` on every diagram.
- No `--` inside an XML comment. It parses inline and fails standalone.
- A `ch-figure` wrapper per chapter, page-local and `ch-` prefixed, with no
  compound selector touching an `interior.css` class name. Captions use the
  existing `.caption`, unmodified.

## Verification

`bookkit.diagrams` over `book/`, which runs the declared checks and then
rasterises each diagram to confirm it renders at all. Then paginate, render,
merge and verify over the whole book. The final page count is reported, not
assumed: 148 will not hold once five diagrams land.

## Out of scope

Chapter 8's `<h2>` reads "The Five-Stage Workflow" over a list of ten stages,
while the prose beneath says ten and the *next* page's cycle is the one that is
five. It looks like a stale heading. It is recorded here and left alone.
