---
itemId: TC-001
itemType: Test Case
itemTests:
  - SRS-001
---
# TC-001 — Urgent-high classification of a fresh reading

**Preconditions:**
- The notification subsystem is running with default plugin registration.
- User settings declare an urgent-high blood-glucose threshold of 200 milligrams per decilitre and the urgent-high alarm category is enabled.
- The warning-high, low, and urgent-low alarm categories are enabled and configured to default thresholds.
- No prior alarm has been acknowledged for the relevant group within the previous 30 minutes.

**Steps:**
1. Submit a sensor reading of 220 milligrams per decilitre with a timestamp equal to the current evaluation time.
2. Trigger one notification-evaluation cycle.
3. Inspect the resulting notification requests captured by the notifications module.

**Expected result:**
- Exactly one alarm request is captured.
- The captured alarm request has severity Urgent and a title that identifies it as the urgent-high category.
- No alarm request of severity Warning is captured for the same reading.
