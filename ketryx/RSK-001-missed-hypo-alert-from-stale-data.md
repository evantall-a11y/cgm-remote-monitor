---
itemId: RSK-001
itemType: Risk
itemIsRiskControlledBy: SRS-002
---
# RSK-001 — Missed hypoglycemic alert due to stale CGM data

**Hazard / Hazard Type:** Information hazard — absence of glucose information when needed for therapy decisions.

**Hazardous Situation:** Patient is in a hypoglycemic or pre-hypoglycemic state while no current glucose reading is being delivered to the monitoring system, so neither the threshold-based BG alert nor the user is aware that a low-glucose event is in progress.

**Sequence of Events:**
- Patient is wearing an active CGM and relying on remote monitoring for hypoglycemia awareness.
- The CGM uplink (sensor, transmitter, bridging device, or network path) stops delivering new readings.
- The most recently delivered reading remains in range and does not trigger a threshold alert.
- Glucose declines in reality but no new readings arrive to update the system.
- Without a stale-data alert, the user assumes the most recent in-range reading is still representative of the patient's state.

**Harm:** Missed or delayed recognition of a hypoglycemic event, leading to delayed corrective therapy and potential physical harm including loss of consciousness in severe cases.

**Risk Control:** Stale-data alert at user-configured staleness duration.

**Risk Controls Description:** When no glucose reading has been received within the configured urgent staleness duration, the system generates a stale-data alert in a dedicated alarm group, prompting the user to verify the CGM and the patient's actual glucose state. Implemented by SRS-002.

**Severity (ISO 14971 default):** Serious. **Probability (ISO 14971 default):** Occasional without control, Remote with control. **Residual risk:** Acceptable provided the user has the staleness alarm enabled and the reading freshness threshold is configured to a value appropriate for the user's CGM cadence.
