---
itemId: RSK-002
itemType: Risk
itemIsRiskControlledBy: SRS-003
---
# RSK-002 — Repeated duplicate alarms cause user to miss a clinically meaningful event

**Hazard / Hazard Type:** Operational hazard — alarm fatigue from duplicate notifications. Without suppression of redelivery, the same threshold-excursion condition produces a continuous stream of identical alerts that the user learns to dismiss without reading.

**Hazardous Situation:** The patient or caregiver is in an environment where alarm notifications for an active threshold excursion are being delivered repeatedly within seconds of each other, and the user has begun to dismiss notifications reflexively.

**Sequence of Events:**
- A blood-glucose threshold excursion occurs and produces an alarm.
- The condition persists across many consecutive evaluation cycles.
- Each evaluation cycle re-emits the same alarm to the user.
- The user begins dismissing the repeating alarm reflexively without reading its content.
- A subsequent, distinct alarm of equal or higher clinical importance arrives in the same stream and is dismissed in the same reflexive way.

**Harm:** Delayed clinical response to an active glucose excursion or to a subsequent independent alarm because the meaningful notification is dismissed without being read; clinical consequences include delayed correction of the excursion and the downstream injuries that delay enables.

**Risk Control:** Per-alarm silence-duration suppression following acknowledgement.

**Risk Controls Description:** SRS-003 requires that, after a user acknowledges an alarm and supplies a silence duration, the subsystem suppress emission of any alarm of equal or lower severity in the same group until the supplied silence duration has elapsed. This prevents the duplicate-emission stream that causes the dismissive behaviour described above.

**Severity (ISO 14971 default scale):** Serious.
**Probability (ISO 14971 default scale):** Probable in the absence of suppression; Improbable with SRS-003 implemented and verified.
**Residual risk:** Acceptable when SRS-003 is implemented and verified by TC-003.
