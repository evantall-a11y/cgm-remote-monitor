---
itemId: RSK-002
itemType: Risk
itemIsRiskControlledBy: SRS-005
---
# RSK-002 — Indefinite suppression of subsequent alarms after a single acknowledgment

**Hazard / Hazard Type:** Software hazard — unintended suppression of safety notifications.

**Hazardous Situation:** A user has acknowledged a prior blood glucose alarm and is relying on the system to re-alert them if a new excursion occurs, while the alarm subsystem holds an active silence state.

**Sequence of Events:**
- The user acknowledges an active alarm.
- The system records an acknowledgment and suppresses re-emission of the alarm.
- The user's blood glucose returns to range, then drifts out of range again or develops a new excursion.
- The silence state is still active and applies to the new excursion.
- The user is not notified of the new excursion.

**Harm:** Untreated subsequent excursion event leading to hypoglycemia or hyperglycemia and associated physical injury.

**Risk Control:** Bounded default silence interval on acknowledgment (SRS-005).

**Risk Controls Description:** Per SRS-005, when an acknowledgment does not specify an explicit silence duration, the system applies a fixed 30-minute upper bound on suppression, after which alarms are permitted to re-emit if the triggering condition remains satisfied. This guarantees that any silence state expires within a known interval and that subsequent qualifying excursions can re-notify the user.
