---
title: Event-Driven PBEM Engine
toc: false
---

Design notes and essays exploring the architecture of an **event-driven
Play-By-Email (PBEM) game engine**.

This is a working design space, not a finished product. The central idea under
exploration: a PBEM engine should be organized around an **event stream** that
transforms player **intent** into **fact** — orders are not actions, the
parser does not resolve turns, and the engine does not parse orders.

The documentation is organized with the [Diataxis](https://diataxis.fr)
framework. Most of what lives here today is **Explanation** — it argues *why*
the design takes the shape it does and weighs the trade-offs.

{{< cards >}}
  {{< card link="explanation/" title="Explanation" subtitle="The reasoning and trade-offs behind the design — start here." >}}
  {{< card link="how-to/" title="How-to guides" subtitle="Goal-oriented recipes (as the engine takes shape)." >}}
  {{< card link="reference/" title="Reference" subtitle="Precise descriptions of records, phases, and APIs." >}}
  {{< card link="tutorials/" title="Tutorials" subtitle="Guided, learning-oriented walkthroughs." >}}
{{< /cards >}}
