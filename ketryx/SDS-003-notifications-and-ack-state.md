---
itemId: SDS-003
itemType: Software Item Spec
itemFulfills:
  - SRS-005
  - SRS-006
---
# SDS-003 — Notifications coordinator and acknowledgment state

A central notifications coordinator orchestrates the alarm evaluation cycle and maintains per-(group, severity) silence state. At the start of each cycle, the coordinator initializes empty alarm-request and snooze-request collections. It then invokes each registered alarm-generating plugin inside an exception boundary so that an unhandled exception raised by one plugin is logged and isolated, allowing the remaining plugins to run.

After all plugins have been invoked, the coordinator selects the highest-severity alarm request per group and checks whether an active snooze applies. If no snooze applies, it dispatches the request to the internal event bus, which forwards it to the WebSocket broadcaster and to external notification channels.

When an acknowledgment message is received from a client, the coordinator records the acknowledgment time on the matching (group, severity) alarm record and applies a silence interval. If the acknowledgment did not specify an interval, the coordinator applies the default silence interval of thirty minutes. The coordinator suppresses re-emission of an alarm at the same (group, severity) for the duration of the silence window. If the acknowledgment is for an URGENT-level alarm, the coordinator additionally applies the same acknowledgment to the WARN-level alarm in the same group so that a single user gesture clears both severities of the same condition.
