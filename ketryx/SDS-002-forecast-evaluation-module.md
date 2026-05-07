---
itemId: SDS-002
itemType: Software Item Spec
itemFulfills:
  - SRS-004
---
# SDS-002 — Forecast (AR2) evaluation module

A forecast evaluation module participates in each alarm evaluation cycle. On each invocation, it reads the most recent blood glucose entries from the in-memory data context and applies a fixed second-order autoregressive model with empirically tuned coefficients to project blood glucose forward in five-minute steps over a thirty-minute horizon.

The module computes a confidence metric (mean projection error over the recent observation window) and compares the projected values at fifteen and twenty minutes against the user-configured target range. If the projected values are estimated to fall outside the target range and the confidence metric exceeds the warning threshold, the module emits a WARN-level alarm request. If the metric exceeds the urgent threshold and the projection still indicates an out-of-range value, the module emits an URGENT-level alarm request.

The module gates its output on data freshness using the same ten-minute rule as the threshold evaluator, and submits alarm requests to the central notifications coordinator for dispatch arbitration.
