---
itemId: SRS-002
itemType: Requirement
itemHasParent: SUB-001
---
# SRS-002 — Blood-glucose alarm classification freshness gate
The system shall not produce a blood-glucose threshold alarm request when the timestamp of the most recent continuous-glucose-monitor reading is more than 10 minutes older than the current evaluation time.

**Pass/fail criterion:** When the most recent reading's timestamp is older than 10 minutes relative to the current evaluation time, no Warning or Urgent blood-glucose threshold alarm request shall be produced.
