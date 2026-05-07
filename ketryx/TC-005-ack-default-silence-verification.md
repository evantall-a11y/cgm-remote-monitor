---
itemId: TC-005
itemType: Test Case
itemTests:
  - SRS-005
---
# TC-005 — Default silence interval after acknowledgment verification

**Preconditions:**
- A user profile is configured with the urgent-low alarm enabled and a known urgent-low threshold value.
- The system has been running for at least one alarm evaluation cycle.
- No alarm is currently active and no snooze is currently in effect for the default group.

**Steps:**
1. Inject a blood glucose entry whose value is below the urgent-low threshold and whose timestamp is the current evaluation time.
2. Trigger an alarm evaluation cycle and confirm an URGENT alarm is emitted on the WebSocket alarm channel.
3. Send an acknowledgment for the URGENT alarm in the default group, omitting an explicit silence-duration field.
4. Inject a second blood glucose entry whose value is below the urgent-low threshold and whose timestamp is twenty-nine minutes after the acknowledgment.
5. Trigger an alarm evaluation cycle and observe whether an URGENT alarm is emitted on the WebSocket alarm channel.
6. Inject a third blood glucose entry whose value is below the urgent-low threshold and whose timestamp is thirty-one minutes after the acknowledgment.
7. Trigger an alarm evaluation cycle and observe whether an URGENT alarm is emitted on the WebSocket alarm channel.

**Expected Result:**
- After step 5, no URGENT alarm is emitted, because the silence window is still active.
- After step 7, exactly one URGENT alarm is emitted on the WebSocket alarm channel, because the default thirty-minute silence window has elapsed and the triggering condition is still met.
