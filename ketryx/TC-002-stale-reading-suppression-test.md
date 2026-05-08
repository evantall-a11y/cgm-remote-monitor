---
itemId: TC-002
itemType: Test Case
itemTests:
  - SRS-002
---
# TC-002 — Stale reading is not classified as a threshold alarm

**Preconditions:**
- The notification subsystem is running with default plugin registration.
- User settings declare an urgent-low threshold of 55 and a warning-low threshold of 75 milligrams per decilitre, both alarm categories enabled.
- No prior alarm has been acknowledged for the relevant group.

**Steps:**
1. Submit a sensor reading of 50 milligrams per decilitre with a timestamp set to 11 minutes prior to the current evaluation time.
2. Trigger one notification-evaluation cycle.
3. Inspect the resulting notification requests captured by the notifications module.

**Expected result:**
- No alarm request of severity Warning or Urgent is captured for the threshold-excursion classifier.
- The classifier returns without raising any blood-glucose threshold alarm, despite the value being below the urgent-low threshold.
