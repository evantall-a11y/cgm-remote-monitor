---
itemId: RSK-001
itemType: Risk
itemIsRiskControlledBy: SRS-002
---
# RSK-001 — Missed hypoglycemic alarm when CGM data is stale

**Hazard / Hazard Type:** Information hazard — alarm omission. The blood-glucose alarm classifier does not consider readings older than 10 minutes, so when the CGM stops reporting fresh values the threshold-excursion alarm path becomes silent for that group.

**Hazardous Situation:** The patient is in or entering a hypoglycemic state while the system is no longer producing threshold-excursion alarms because the most recent reading is older than 10 minutes.

**Sequence of Events:**
- The continuous-glucose-monitor stops uploading new readings (transmitter loss, network outage, or sensor failure).
- The patient's true blood glucose drops into the hypoglycemic range while no fresh reading exists.
- The alarm classifier evaluates and rejects the most recent reading because its timestamp is older than 10 minutes.
- No Warning or Urgent low alarm request is produced for this evaluation cycle.
- The caregiver continues to assume the last seen value reflects current state.

**Harm:** Delayed treatment of hypoglycemia, with the potential clinical consequences of severe hypoglycemia including loss of consciousness, seizure, or injury caused by impaired judgement.

**Risk Control:** Bounded freshness window with explicit handoff.

**Risk Controls Description:** SRS-002 defines an explicit 10-minute freshness window so that stale readings cannot drive false reassurance through a "no alarm" outcome and so that the no-data condition can be unambiguously detected and handed off to a separate stale-data notification path. **Control gap noted:** the stale-data notification path itself is not part of this software requirement set; the gap should be closed by an additional Software Requirement covering generation of a stale-data notification when the freshness window is exceeded, before this risk is considered fully mitigated.

**Severity (ISO 14971 default scale):** Critical.
**Probability (ISO 14971 default scale):** Occasional — depends on CGM reliability and network availability.
**Residual risk:** Until the stale-data notification SRS is added and tested, residual risk remains above acceptable.
