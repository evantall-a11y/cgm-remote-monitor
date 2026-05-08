---
itemId: SDS-001
itemType: Software Item Spec
itemFulfills:
  - SRS-001
  - SRS-002
---
# SDS-001 — Blood-glucose classifier with freshness window

The blood-glucose alarm classification responsibility is implemented in the simple-alarms notification plugin, which is registered as one of the server's default notification plugins and is invoked by the plugin runner on each notification-evaluation cycle.

On each cycle the classifier reads the most recent sensor reading from the runtime sandbox, scales it to the user's display units, and evaluates the following pipeline:

1. **Validity gate.** The reading must have a numeric value greater than 39 milligrams per decilitre. Values at or below this threshold are reserved for CGM error codes and are handed off to the error-codes plugin instead of the threshold classifier.
2. **Freshness gate.** The reading's timestamp is compared to the current sandbox evaluation time. If the difference exceeds 10 minutes, the classifier returns without producing any alarm request. This implements SRS-002.
3. **Severity classification.** The scaled reading is compared in turn against the configured urgent-high, warning-high, urgent-low, and warning-low thresholds. Each comparison is gated by the corresponding per-category enable flag in the user's settings (urgent-high, high, low, urgent-low). The first matching comparison produces an alarm request whose severity is Urgent or Warning accordingly. This implements SRS-001.
4. **Notification request.** Matching readings produce a notification request submitted to the notifications module with severity, title, message, plugin identity, and an optional Pushover sound name.

Threshold values and unit scaling are derived from the merged user/server settings module, which normalises mmol-format thresholds to milligrams per decilitre at load time and clamps degenerate target ranges so that target-bottom is always strictly less than target-top.

The classifier is deterministic with respect to its inputs and produces at most one alarm request per evaluation cycle.
