---
itemId: SRS-006
itemType: Requirement
itemHasParent: SUB-003
---
# SRS-006 — Alarm plugin error isolation

When an alarm-generating plugin raises an unhandled exception during evaluation, the system shall log the failure and shall continue invoking the remaining alarm-generating plugins so that an unrelated plugin fault does not suppress dispatch of alarms produced by other plugins.
