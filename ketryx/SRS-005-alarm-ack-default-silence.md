---
itemId: SRS-005
itemType: Requirement
itemHasParent: SUB-003
---
# SRS-005 — Bounded default silence on alarm acknowledgment

When the system receives an alarm acknowledgment from a client that does not specify an explicit silence duration, the system shall apply a default silence interval of 30 minutes after which the suppressed alarm shall be permitted to re-emit if its triggering condition remains met.
