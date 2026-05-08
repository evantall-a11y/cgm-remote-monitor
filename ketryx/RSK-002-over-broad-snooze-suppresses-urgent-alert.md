---
itemId: RSK-002
itemType: Risk
itemIsRiskControlledBy: SRS-003
---
# RSK-002 — Over-broad snooze suppresses subsequent urgent alert

**Hazard / Hazard Type:** Software hazard — unintended suppression of a clinically relevant alert.

**Hazardous Situation:** Patient is in a clinically actionable glucose state while a previously requested user acknowledgment of a less severe alert remains active and is preventing distribution of a newly raised same-group alert.

**Sequence of Events:**
- A WARN-level alert is raised and the user acknowledges it, choosing a long silence duration.
- Glucose continues to deteriorate and a new alert condition would normally be raised in the same alarm group.
- The dispatcher consults the acknowledgment state and finds the active acknowledgment covers the new alert's severity.
- The new alert is acknowledged programmatically rather than emitted to subscribed clients.

**Harm:** Delayed recognition of a worsening glucose excursion, leading to delayed corrective therapy and potential physical harm consistent with prolonged hyper- or hypoglycemia.

**Risk Control:** Acknowledgment scope limited to severities at or below the acknowledged level, with snooze duration selected by the user per acknowledgment.

**Risk Controls Description:** The acknowledgment state manager records the acknowledged severity and group, and the dispatcher only suppresses alerts whose severity is at or below the acknowledged severity for the same group. An URGENT-level condition that follows a WARN-level acknowledgment is not suppressed by that acknowledgment. Implemented by SRS-003.

**Severity (ISO 14971 default):** Serious. **Probability (ISO 14971 default):** Occasional without control, Remote with control. **Residual risk:** Acceptable. **Control gap note:** the system does not enforce an upper bound on the user-selectable silence duration; user training and default UI choices govern realistic snooze lengths.
