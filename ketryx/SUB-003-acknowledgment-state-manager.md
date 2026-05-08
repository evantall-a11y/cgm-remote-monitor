---
itemId: SUB-003
itemType: Requirement
requirementType: INTERFACES
itemHasParent: SYS-003
---
# SUB-003 — Acknowledgment state manager subsystem
The acknowledgment state manager subsystem shall record, per alarm group and per severity level, the time of the most recent user acknowledgment and the user-selected silence duration, and shall expose this state to the notification dispatcher so that suppressed alerts are not redistributed during the silence interval.
