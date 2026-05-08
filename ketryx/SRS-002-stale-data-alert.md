---
itemId: SRS-002
itemType: Requirement
requirementType: SOFTWARE_SYSTEM
itemHasParent: SUB-002
---
# SRS-002 — Stale data alert generation
When the urgent staleness alarm setting is enabled and no glucose reading has been received within the configured urgent staleness duration (default 30 minutes), the system shall request a stale-data alert at URGENT severity in the Time Ago alarm group.
