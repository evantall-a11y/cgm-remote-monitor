---
itemId: SDS-002
itemType: Software Item Spec
itemFulfills:
  - SRS-003
---
# SDS-002 — Per-alarm silence state and emission gate

The acknowledged-alarm suppression responsibility is implemented in the notifications module. The module maintains an in-memory map of Alarm records keyed by the pair (severity, group). Each Alarm record carries:

- a last-acknowledgement time, expressed as a millisecond epoch,
- a silence duration, expressed in milliseconds, with a default of 30 minutes when no explicit duration is supplied,
- a last-emission time recorded each time a notification for that record is dispatched.

When an acknowledgement arrives through the alarm websocket channel, the notifications module records the current time as the alarm's last-acknowledgement time, sets the alarm's silence duration to the duration supplied in the acknowledgement (or to the 30-minute default when none is supplied), and clears the last-emission time. Acknowledgement of an Urgent alarm additionally cascades to the Warning alarm in the same group so that lower-severity alarms in the same group are also silenced.

Each evaluation cycle, the notifications module selects the highest-severity outstanding alarm request per group and consults the corresponding Alarm record before emitting. Emission is gated as follows:

- If the most recent data-update time is greater than the alarm's last-acknowledgement time plus the alarm's silence duration, the notification is emitted on the internal event bus and the last-emission time is recorded.
- Otherwise the alarm is treated as silenced and the emission is skipped, with a log line recording the remaining silence interval in minutes.

Snooze requests submitted alongside notification requests are matched by group and severity and converted into acknowledgements with the requested silence length, allowing the same gate to handle pre-emptive snoozes.

This design makes the silence state per (severity, group), bounded by the duration recorded at acknowledgement time, which directly implements SRS-003.
