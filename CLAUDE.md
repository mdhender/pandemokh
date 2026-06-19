# CLAUDE.md

## What this work is

We are exploring the **design of an event-driven PBEM (Play-By-Email) game
engine**. This is design exploration, not implementation. The output is
*essays and design notes*, not (yet) code.

Expect this to be messy. We will run down rabbit holes, take wrong turns, and
abandon ideas. Dead ends are expected and acceptable. The design may end up
looking nothing like where it starts — "event-driven" is the current framing,
not a commitment.

## Scope

- **In scope:** the essays in `docs/essays/`, the design ideas they explore,
  and the documentation site under `site/` that publishes them.
- **Out of scope (ignore unless explicitly asked):** the Go code in `cmd/`,
  the DEM (Digital Elevation Model) terrain-processing tooling, and the
  `.archives/` DEM data. That work is described in `AGENTS.md` and is a
  separate concern from this design exploration.

## Source material

The core thesis so far: a PBEM engine should be organized around an **event
stream** that transforms player **intent** into **fact**, sometimes producing
**derived intent** that later phases resolve. Orders are not actions; the
parser does not resolve turns; the engine does not parse orders.

## Documentation site

The site lives in `site/` and is built with **Hugo** (extended) using the
**Hextra** theme, installed via Hugo Modules.

- Local preview: `cd site && hugo server`
- Build: `cd site && hugo`

### Diataxis

Documentation follows the [Diataxis](https://diataxis.fr) framework — four
types split by two axes (action vs. cognition, acquisition vs. application):

|                 | Action        | Cognition       |
|-----------------|---------------|-----------------|
| **Acquisition** | Tutorials     | **Explanation** |
| **Application** | How-to guides | Reference       |

The content tree under `site/content/` has a section per type. **Our essays
are Explanation** — they discuss *why*, weigh trade-offs, and consider
alternatives rather than instructing or describing. When adding docs, classify
first (use the `diataxis` skill) and don't mix types in one document.

## Working notes

- When an essay's addendum lists a topic as "its own essay," that's a backlog
  item, not something to fold into the current piece. Keep one star per essay.
- Prefer the vocabulary the essays establish — see the
  [glossary](site/content/reference/glossary.md).
