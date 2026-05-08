---
itemId: SRS-003
itemType: Requirement
itemHasParent: SUB-002
---
# SRS-003 — Acknowledged-alarm redelivery suppression
The system shall suppress emission of a subsequent alarm whose severity and group match a previously acknowledged alarm until the silence duration recorded in that acknowledgement has elapsed since the acknowledgement was received.

**Pass/fail criterion:** When an acknowledgement records a silence duration of T milliseconds at time T0 for severity S and group G, no alarm of severity S and group G shall be emitted at any time strictly less than T0 + T.
