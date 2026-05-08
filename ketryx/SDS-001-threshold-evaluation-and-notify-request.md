---
itemId: SDS-001
itemType: Software Item Spec
itemFulfills: SRS-001
---
# SDS-001 — Threshold evaluation and notify-request submission
The Simple Alarms plugin module evaluates the latest scaled glucose value against the user's configured low, urgent low, high, and urgent high thresholds on each evaluation cycle. The module first guards the evaluation by requiring that the most recent glucose reading be both fresh (its timestamp within 10 minutes of the current evaluation time) and above the implausibly low cutoff of 39 mg/dL. When a threshold crossing is found and the corresponding alarm enable setting is true, the module constructs a notification request containing severity level, display title, message, plugin reference, and Pushover sound hint, then submits the request to the notifications subsystem via the requestNotify entry point. The notifications subsystem accepts the request, records its alarm group, and queues it for the per-cycle dispatch step that selects the highest active severity per group.
