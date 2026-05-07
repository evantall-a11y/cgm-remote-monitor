---
itemId: TC-002
itemType: Test Case
itemTests:
  - SRS-002
---
# TC-002 — Urgent low blood glucose alarm verification

**Preconditions:**
- A user profile is configured with the urgent-low alarm enabled and a known urgent-low threshold value.
- The system has been running for at least one alarm evaluation cycle and the in-memory data context is initialized.
- No alarm is currently active and no snooze is currently in effect for the default group.

**Steps:**
1. Inject a blood glucose entry whose value is one unit above the configured urgent-low threshold and whose timestamp is the current evaluation time.
2. Trigger an alarm evaluation cycle and observe whether an URGENT alarm is emitted on the WebSocket alarm channel.
3. Inject a second blood glucose entry whose value is one unit below the configured urgent-low threshold and whose timestamp is the current evaluation time.
4. Trigger an alarm evaluation cycle and observe whether an URGENT alarm is emitted on the WebSocket alarm channel.

**Expected Result:**
- After step 2, no URGENT alarm is emitted.
- After step 4, exactly one URGENT alarm is emitted on the WebSocket alarm channel within one evaluation cycle, with the originating plugin identifier indicating the threshold evaluator.
