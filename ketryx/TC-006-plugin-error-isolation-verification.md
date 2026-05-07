---
itemId: TC-006
itemType: Test Case
itemTests:
  - SRS-006
---
# TC-006 — Plugin error isolation verification

**Preconditions:**
- The system is configured with at least two alarm-generating plugins registered: a faulty plugin instrumented to raise an unhandled exception during evaluation, and the threshold evaluator.
- A user profile is configured with the urgent-low alarm enabled and a known urgent-low threshold value.
- No alarm is currently active and no snooze is currently in effect for the default group.

**Steps:**
1. Inject a blood glucose entry whose value is below the configured urgent-low threshold and whose timestamp is the current evaluation time.
2. Trigger an alarm evaluation cycle. During this cycle, the faulty plugin is invoked first and raises an unhandled exception; the threshold evaluator is invoked next.
3. Observe the system log and the WebSocket alarm channel.

**Expected Result:**
- The system log contains a record of the faulty plugin's exception with its plugin identifier.
- The system does not crash or terminate the evaluation cycle.
- Exactly one URGENT alarm is emitted on the WebSocket alarm channel from the threshold evaluator, demonstrating that the faulting plugin did not suppress dispatch of the unrelated alarm.
