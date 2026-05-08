---
itemId: SRS-001
itemType: Requirement
itemHasParent: SUB-001
---
# SRS-001 — Urgent-high classification of glucose readings
The system shall classify the most recent continuous-glucose-monitor reading as an Urgent High alarm when the reading is strictly greater than the configured urgent-high blood-glucose threshold and the urgent-high alarm category is enabled in the user's settings.

**Pass/fail criterion:** When the most recent reading exceeds the urgent-high threshold and the urgent-high alarm category is enabled, the subsystem shall produce exactly one alarm request of severity Urgent.
