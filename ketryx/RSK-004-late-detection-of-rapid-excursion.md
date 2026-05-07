---
itemId: RSK-004
itemType: Risk
itemIsRiskControlledBy: SRS-004
---
# RSK-004 — Threshold-only alarms detect rapid excursions too late for corrective action

**Hazard / Hazard Type:** Information hazard — late detection of imminent harm.

**Hazardous Situation:** A user is relying on threshold-based alarms while their blood glucose is changing rapidly enough that the threshold crossing leaves insufficient time to take corrective action before harm occurs.

**Sequence of Events:**
- The user has configured threshold-based alarms only and relies on them for awareness of out-of-range values.
- An event such as recent insulin dose, exercise, or carbohydrate consumption causes blood glucose to fall or rise rapidly.
- The blood glucose is still within the configured target range and no threshold alarm fires.
- By the time the value crosses the urgent threshold, the user has insufficient time to ingest carbohydrates or take other corrective action before reaching a clinically harmful level.

**Harm:** Severe hypoglycemia or hyperglycemia with associated physical injury due to delayed corrective action.

**Risk Control:** Predicted blood glucose excursion alarm (SRS-004).

**Risk Controls Description:** Per SRS-004, the system continuously projects blood glucose forward over a 30-minute horizon based on recent readings and generates a WARN-level alarm when the projection crosses the user's target range, providing earlier warning than a threshold crossing alone and allowing the user to act before urgent thresholds are reached.
