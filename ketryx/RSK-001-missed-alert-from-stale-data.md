---
itemId: RSK-001
itemType: Risk
itemIsRiskControlledBy: SRS-003
---
# RSK-001 — Missed hypoglycemic or hyperglycemic alert because CGM data has stopped flowing

**Hazard / Hazard Type:** Information hazard — silent loss of monitoring data.

**Hazardous Situation:** A user is relying on the system for active blood glucose surveillance while no fresh blood glucose readings are being received and the user is unaware that monitoring has lapsed.

**Sequence of Events:**
- The user enables blood glucose alarms and assumes ongoing surveillance.
- The CGM uploader, transmitter, or network link interrupts so no new readings reach the system.
- The most recent reading was last received some minutes earlier and is no longer current.
- The user's blood glucose drifts toward an out-of-range value.
- Threshold-based alarms are gated on data freshness and therefore do not fire.
- The user is unaware that monitoring has stopped.

**Harm:** Missed or delayed detection of an excursion event, leading to untreated hypoglycemia or hyperglycemia and potential physical injury (loss of consciousness, seizure, prolonged ketosis).

**Risk Control:** Stale CGM data notification (SRS-003).

**Risk Controls Description:** Per SRS-003, the system generates a WARN-level notification when the time since the last received blood glucose entry exceeds the user-configured stale-data interval, alerting the user that monitoring has lapsed and prompting them to investigate the data feed.

**Note on adequacy:** The control surfaces the lapse but depends on the user receiving and acting on the WARN notification. If the user has snoozed the WARN level globally, the staleness notification will also be suppressed during the silence window — caregivers should be informed of this dependency.
