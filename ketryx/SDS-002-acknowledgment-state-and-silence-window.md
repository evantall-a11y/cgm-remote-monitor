---
itemId: SDS-002
itemType: Software Item Spec
itemFulfills: SRS-003
---
# SDS-002 — Acknowledgment state and silence window enforcement
The notifications subsystem maintains an in-memory map of alarm objects keyed by severity level and alarm group. Each alarm object holds the time of its last acknowledgment and the silence duration applied at that acknowledgment. When the dispatcher selects the highest-severity active alert for a group, it compares the freshest data timestamp against the alarm's last-ack-time plus silence-duration; if the silence window is still active, the dispatcher logs the suppression and does not emit the alert. When an acknowledgment arrives via the alarm socket and authorization succeeds, the subsystem records the current wall-clock time as the last-ack-time, records the user-selected silence duration, and clears any in-flight emit marker so that the next out-of-window evaluation can re-emit if the underlying condition still holds. Acknowledging an URGENT-level alert also acknowledges the WARN-level alert in the same group so that a single user action covers both severities. After the silence window expires and the underlying condition has cleared, an automatic acknowledgment with a one-millisecond silence duration is recorded and an All Clear notification is emitted, ensuring future occurrences are not suppressed.
