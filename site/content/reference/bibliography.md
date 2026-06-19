---
title: "Bibliography"
linkTitle: "Bibliography"
weight: 10
toc: false
---

Works referenced in the design notes.

---

**I Heart Logs: Event Data, Stream Processing, and Data Integration**
Jay Kreps, O'Reilly Media, 2014.
[Local copy](/docs/20170922-EB-I_Heart_Logs.pdf)

The short book that articulates the log as a universal data structure:
append-only, ordered, multiply readable with independent offsets. The PBEM
event stream is an application of this model. Kreps's treatment of state as a
projection from a log, and of snapshots as compaction checkpoints, underpins
the design described in
[Snapshots and the Event Pointer](../explanation/snapshots-and-the-event-pointer.md).
