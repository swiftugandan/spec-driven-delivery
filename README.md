# Specification-Driven Development

A book about making AI implementation reliable by treating specifications, not code, as the asset that lasts.

The argument: when an AI agent writes a feature from a one-line request, it has to invent every business decision the request left out, and most of those guesses belong to a different organization. The fix is to move the work earlier. Write down the vision, requirements, use cases, domain model, architecture constraints and implementation conventions, and the agent translates a decision you already made instead of guessing at one. The same discipline runs in reverse on a legacy system whose specification was never written down.

The methodology is Simon Martinelli's; this book is a treatment of it, and credits it throughout.

**Status:** complete draft, 148 pages, ~35,000 words. Author name and ISBN are deliberate placeholders (`[AUTHOR NAME]`, `[ISBN TBD]`).

## Repository layout

```
drafts/     20 files, ~30,000 words. The source manuscript this book was built from.
            Kept as the record of what the book's claims trace back to.

book/       The book itself.
  STRUCTURE.md        The blueprint: promise, audience, reading paths, running
                      examples, per-chapter driving question and beat list, page
                      budget. This is the contract every chapter is written against.
  interior.css        The interior design system. Retarget the whole book by
                      editing the tokens at the top (trim size, margins, ink,
                      paper, accent, type stacks).
  book.order          Assembly order, one filename per line.
  *.html              19 page files: cover, front matter, foreword, 11 chapters,
                      afterword, 3 appendices, glossary/notes/index.
  pdf/                Per-file PDFs, written by the render step.
  book.manifest.json  Page counts and folio offsets, written by the paginate step.
  book.pdf            The assembled book.
```

The 11 chapters run in three parts (Foundation, Framework, Practice and implications). Two examples thread the whole book: a multi-location clinic group building online appointment booking, and a retail bank recovering a specification from a 1980s COBOL ledger.

## Building the book

The build lives in the [`book-writing`](https://github.com/swiftugandan/book-writing-skill) skill, installed at `~/.claude/skills/book-writing`. Pages are hand-paginated as `.page` divs and rendered through Playwright's Chromium.

First-time setup:

```bash
cd ~/.claude/skills/book-writing/scripts
python3 -m venv .venv
.venv/bin/pip install -e '.[dev]'
.venv/bin/playwright install chromium
```

Then, from that same directory:

```bash
SKILL=~/.claude/skills/book-writing
BOOK=/path/to/spec-driven-delivery/book

.venv/bin/python -m bookkit.paginate "$BOOK"   # measure pages, write folio offsets
.venv/bin/python -m bookkit.render   "$BOOK"   # render each file to pdf/
.venv/bin/python -m bookkit.merge    "$BOOK"   # assemble book.pdf
.venv/bin/python -m bookkit.verify   "$BOOK" --css "$SKILL/assets/interior.css"
```

Run all four after any content edit. Editing one chapter changes its page count, which changes every downstream folio.

`verify` should end with `OK: 148 pages verified`. It fails on clipped pages, wrong trim geometry, CSS layering violations, a stale manifest, and folio discontinuity. Every one of those is otherwise silent, which is the whole reason it exists.

## Editing rules worth knowing before you touch a page file

These are the constraints that will bite you, learned the hard way:

- **Overflow is silently clipped.** `.page` has `overflow: hidden`, so text that does not fit simply vanishes off the bottom of the page with no error and no warning. If you add material, run `verify`. If a page grows, move a whole element to the next page or split the page; never compress the type.
- **Never hand-edit a `counter-reset` value.** `paginate` writes those from measured page counts. A hand-assigned offset encodes a guess about chapter length, and a chapter that runs one page over silently renumbers everything after it.
- **Page-local CSS must be prefixed `ch-`** and must never reuse a class name from `interior.css`, including inside a compound selector like `.callout.ch-thing`. The layering check rejects both. A chapter that redefines `.callout` restyles every callout in the book, and the damage shows up in a chapter nobody was editing.
- **Em dashes: at most one per thousand words**, and in practice each file has exactly one, inside its `<title>` tag. The en dashes in the contents rows are deliberate folio placeholders.
- **Evidence standing is load-bearing.** Reported practice is attributed, established practice is cited as existing, the author's interpretation reads as interpretation, and speculation is labelled as speculation. The case figures in Appendix A are single-engagement reported outcomes and must never read as typical or guaranteed. Do not add a statistic, source, date, or entity name the drafts do not support.
- **`appendix-c.html`'s implementation-notes page has roughly 30px of slack**, the tightest in the book. Anything added there will clip. Split the page first.

## How it was written

Built with two Claude Code skills: [`book-writing`](https://github.com/swiftugandan/book-writing-skill) for structure, interior design and the build pipeline, and [`avoid-ai-writing`](https://github.com/conorbronsdon/avoid-ai-writing) for the prose audit.

After drafting, the book went through three editorial rounds plus a content punch list, each round using per-file reviewers, adversarial verifiers that had to try to refute every finding, and five whole-book audits (continuity, terminology, fact consistency, duplication, voice). Fix counts fell from ~200 to 75 to 4 across the rounds.

One finding from that process is worth repeating, because it will apply to anyone editing this book next: **a fix loop introduces defects at roughly the rate it removes them, and always in the same shape.** A correction lands in one passage and its counterpart elsewhere is left contradicting it. It happened five times here, including twice to fixes that were themselves fixing it. Two practical consequences:

- Search for the **problem**, not the patch. Grepping for the string you just corrected cannot find the twin you missed.
- A tool reporting no errors is not evidence the change happened. One round reported zero failures while 23 findings sat unapplied, the highest-severity one among them.

## License and attribution

Please attribute the underlying methodology to Simon Martinelli. The manuscript in `drafts/` carries its own usage terms.
