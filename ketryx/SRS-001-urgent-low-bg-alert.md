---
itemId: SRS-001
itemType: Requirement
requirementType: SOFTWARE_SYSTEM
itemHasParent: SUB-001
---
# SRS-001 — Urgent low BG alert generation
When the urgent low alarm setting is enabled and the most recent glucose reading is strictly below the configured urgent low threshold, the system shall request a glucose alert at URGENT severity, provided the reading was received no more than 10 minutes before the current evaluation time and the reported glucose value is greater than 39 mg/dL.
