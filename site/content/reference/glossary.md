---
title: Glossary
linkTitle: Glossary
weight: 1
toc: true
---

Definitions of the vocabulary used across the design notes. Terms are listed
alphabetically. Where a term is easy to confuse with another, the related term
is noted.

For the reasoning behind these distinctions, see the Explanation essays;
this page only describes the terms.

### Accepted intent

[Intent](#intent) that has been recorded as the players' submission for a
turn. Accepted intent is preserved across a [rewind](#rewind); only
[derived intent](#derived-intent) and [facts](#fact) are discarded and rebuilt.
Distinct from derived intent, which the engine produces during resolution.

### Command

A request that asks the system to do something (for example, `AttackCommand`).
Commands are handled by the [parser](#parser) at order intake. A command is not
yet [intent](#intent): the parser validates a command and, if accepted, emits an
intent record.

### Derived intent

Work created by the simulation during [resolution](#resolution) rather than by a
player's [order](#order) — a new obligation discovered while resolving a turn
(for example, `Retreat`, `PursuitAvailable`, `LootDropped`). Derived intent is
neither a player order nor a completed [fact](#fact); it is consumed by a later
[phase](#phase). It is discarded and rebuilt on [rewind](#rewind).

### Engine

The component that drains the [event stream](#event-stream): it reads the next
unresolved record, resolves it against [working state](#working-state), and
emits new records, repeating until no unresolved work remains. The engine does
not parse [orders](#order), approve results, publish [reports](#report), or open
order entry — those are concerns of the surrounding application.

### Event stream

The ordered, authoritative history of a turn: the sequence of
[intent](#intent), [fact](#fact), and [derived intent](#derived-intent) records.
It is both the engine's work queue and the narrative that explains how
[state](#working-state) came to be what it is. The organizing principle of the
engine.

### Fact

A record describing something that has happened (for example,
`Arrived`, `Defending`, `Wounded`). Facts are past-tense. Some facts alter game
state; some exist only to explain what happened. Facts are rendered into
[reports](#report); they are not invented by reports. Discarded and rebuilt on
[rewind](#rewind).

### Game Master (GM)

The operator of a game. The GM reviews and approves turn results, may
[rewind](#rewind) or replay a turn, and performs administrative operations on
the [event stream](#event-stream). For the GM, a turn is complete when results
have been reviewed and approved — a different sense of "complete" than the
engine's or a player's.

### Intent

A record describing something that should be attempted or resolved (for example,
`Move`, `Attack`, `Defend`). Player-submitted intent is produced by the
[parser](#parser) from [orders](#order); the engine may also produce
[derived intent](#derived-intent). The engine's central job is to transform
intent into [fact](#fact). See also [accepted intent](#accepted-intent).

### Order

The text a player submits, expressing a statement of intent — not an action. An
order such as `MOVE 3,4` asks the game to attempt that move during the
appropriate [phase](#phase); it does not itself change state. Orders are turned
into [intent](#intent) records by the [parser](#parser).

### Parser

The component that accepts [orders](#order) (or [commands](#command)), validates
syntax and performs shallow semantic checks, and emits structured
[intent](#intent) records. The parser does not resolve the turn and does not
decide outcomes. It sits outside the [engine](#engine).

### PBEM

Play-By-Email. A turn-based game in which players submit [orders](#order) for a
turn, the [engine](#engine) resolves them, and [reports](#report) are returned
before the next turn begins.

### Phase

A stage of turn resolution treated as a small [engine](#engine) (for example,
movement, defense, attack, retreat). A phase reads the [stream](#event-stream)
records relevant to it, resolves them against [working state](#working-state),
and emits [facts](#fact) and any [derived intent](#derived-intent). Phases run
in a designed order; the order belongs to the game design.

### Report

A player-specific rendering of resolved [facts](#fact). A report describes what
happened (and, from the stream, why); it does not resolve rules or invent
outcomes. Reports may distinguish facts that are private to one player, visible
to several, or visible only to the [GM](#game-master-gm).

### Resolution

The act of transforming [intent](#intent) (or [derived intent](#derived-intent))
into [fact](#fact) against a stable view of state. The practical model is
`G0 + e -> r`, where `G0` is the working state before the event, `e` is the
record being resolved, `r` is the resolution, and applying `r` mutates `G0` into
`G1`. Inputs to a resolution (such as combat inputs) must be stable for its
duration.

### Rewind

An administrative operation on the [event stream](#event-stream) that returns a
turn to an earlier point. The rule: preserve [accepted intent](#accepted-intent);
discard [derived intent](#derived-intent) and [facts](#fact) after the chosen
point and let the engine resolve again. From the engine's perspective, nothing
special happens — it simply processes the records in front of it.

### Snapshot

A durable summary of the game world, typically written at the end of a turn. A
snapshot is the authoritative current state for the start of the next turn. It
is not a replacement for the [event stream](#event-stream): the stream answers
*why*, the snapshot answers *what now*. Lets the engine start a turn from a known
state rather than replaying from turn zero.

### Turn

The unit of play. A turn accepts [intent](#intent), resolves it, records
[facts](#fact), and sometimes creates [derived intent](#derived-intent), until
nothing remains unresolved. "Complete" means different things to the
[engine](#engine), the [GM](#game-master-gm), and the player.

### Working state

The authoritative mutable game state held in memory while the [engine](#engine)
resolves a turn (also "the in-memory model"). The engine resolves the next
record against working state, applies the result, and continues. Compare the
[event stream](#event-stream) (authoritative history) and the
[snapshot](#snapshot) (authoritative current state between turns).
