---
itemId: TC-003
itemType: Test Case
itemTests:
  - SRS-003
---
# TC-003 — Stale CGM data notification verification

**Preconditions:**
- A user profile is configured with the stale-data warning interval set to a known value (default thirty minutes).
- The system has been running for at least one alarm evaluation cycle.
- No alarm is currently active and no snooze is currently in effect for the default group.

**Steps:**
1. Inject a blood glucose entry whose value is within the user's target range and whose timestamp is the current evaluation time.
2. Advance simulated time so that no further blood glucose entries are received and the elapsed time since the last entry is one minute less than the configured stale-data warning interval.
3. Trigger an alarm evaluation cycle and observe whether a stale-data notification is emitted on the WebSocket alarm channel.
4. Advance simulated time by two additional minutes so that elapsed time exceeds the configured stale-data warning interval.
5. Trigger an alarm evaluation cycle and observe whether a stale-data notification is emitted on the WebSocket alarm channel.

**Expected Result:**
- After step 3, no stale-data notification is emitted.
- After step 5, exactly one WARN-level stale-data notification is emitted on the WebSocket alarm channel.
