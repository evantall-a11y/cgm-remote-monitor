---
itemId: SDS-001
itemType: Software Item Spec
itemFulfills:
  - SRS-001
  - SRS-002
  - SRS-003
---
# SDS-001 — Threshold and freshness evaluation module

A simple-alarms evaluation module participates in each alarm evaluation cycle as one of several alarm-generating plugins. On each invocation, it reads the most recent blood glucose entry from the in-memory data context, applies the user's display unit conversion (mg/dL or mmol/L), and reads the configured high, low, urgent-high, and urgent-low thresholds from the user profile.

The module first checks freshness: if the most recent entry's timestamp is older than ten minutes relative to the current evaluation time, it produces no alarm request from this evaluator. A separate timeago evaluator emits the WARN-level stale-data notification specified by SRS-003 once the configured stale-data interval (default thirty minutes) has elapsed.

If the most recent entry is fresh, the module compares its value against each enabled threshold in priority order — urgent-low, urgent-high, warn-low, warn-high — and emits at most one alarm request per cycle, populating the alarm structure with severity level (URGENT or WARN), the originating plugin name, a localized title and message, and the alarm group. Alarm requests are submitted to the central notifications coordinator, which selects the highest-severity request per group for dispatch.
