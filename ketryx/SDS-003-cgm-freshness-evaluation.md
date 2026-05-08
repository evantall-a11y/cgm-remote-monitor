---
itemId: SDS-003
itemType: Software Item Spec
itemFulfills: SRS-002
---
# SDS-003 — CGM freshness evaluation and stale-data alert request
The Time Ago plugin module computes the elapsed time between the timestamp of the most recent glucose entry and the current evaluation time. The module compares this elapsed time against the user-configured warning and urgent staleness thresholds (default 15 minutes warning and 30 minutes urgent) and produces a status of current, warning, or urgent. When the status is warning or urgent and the corresponding alarm enable setting is true, the module constructs a notification request whose alarm group is the dedicated Time Ago group and submits it to the notifications subsystem. The Time Ago plugin also detects and rejects evaluation cycles that occur immediately after a host-side hibernation event by comparing wall-clock deltas across check invocations and skipping alert generation for a short post-resume interval, so that a brief alarm-socket gap due to host suspend does not produce a spurious stale-data alert.
