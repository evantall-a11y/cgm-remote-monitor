---
itemId: SUB-003
itemType: Requirement
itemHasParent: SYS-003
---
# SUB-003 — Alarm dispatch and acknowledgment subsystem

The alarm dispatch and acknowledgment subsystem shall be responsible for receiving alarm requests from evaluation subsystems, broadcasting alarm and clear events to subscribed client sessions, accepting acknowledgment messages from clients, and maintaining a per-group, per-severity silence state that suppresses repeat dispatch during the configured silence interval.
