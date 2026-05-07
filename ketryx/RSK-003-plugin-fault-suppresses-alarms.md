---
itemId: RSK-003
itemType: Risk
itemIsRiskControlledBy: SRS-006
---
# RSK-003 — Faulting plugin suppresses dispatch of unrelated blood glucose alarms

**Hazard / Hazard Type:** Software hazard — unintended halting of safety-critical evaluation pipeline.

**Hazardous Situation:** A user is relying on the alarm subsystem to evaluate every active alarm source while one alarm-generating plugin is in a faulted state during the evaluation cycle.

**Sequence of Events:**
- The system loads multiple alarm-generating plugins, including blood glucose threshold and forecast evaluators.
- During an evaluation cycle, one plugin encounters an unhandled exception caused by malformed input, a configuration error, or an upstream change.
- Without isolation, the exception would propagate and prevent later plugins in the cycle from running.
- A blood glucose threshold or forecast plugin scheduled later in the same cycle does not run.
- The user's blood glucose is out of range, but no alarm is generated for that cycle.

**Harm:** Missed or delayed detection of an excursion event, leading to untreated hypoglycemia or hyperglycemia and potential physical injury.

**Risk Control:** Plugin error isolation (SRS-006).

**Risk Controls Description:** Per SRS-006, the alarm pipeline catches unhandled exceptions raised by an individual plugin, logs the failure, and continues invoking the remaining plugins so that a single faulting plugin cannot suppress alarms produced by other plugins in the same evaluation cycle.
