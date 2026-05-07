---
itemId: TC-004
itemType: Test Case
itemTests:
  - SRS-004
---
# TC-004 — Predicted blood glucose excursion alarm verification

**Preconditions:**
- A user profile is configured with target range bottom and target range top set to known values.
- The forecast evaluator is enabled and at least six recent blood glucose entries spaced at five-minute intervals are present in the data context.
- No alarm is currently active and no snooze is currently in effect for the default group.

**Steps:**
1. Inject a sequence of recent blood glucose entries whose trajectory, when projected forward thirty minutes by the forecast model, remains inside the configured target range.
2. Trigger an alarm evaluation cycle and observe whether a predicted-excursion alarm is emitted on the WebSocket alarm channel.
3. Inject a sequence of recent blood glucose entries whose trajectory, when projected forward thirty minutes by the forecast model, falls outside the configured target range.
4. Trigger an alarm evaluation cycle and observe whether a predicted-excursion alarm is emitted on the WebSocket alarm channel.

**Expected Result:**
- After step 2, no predicted-excursion alarm is emitted.
- After step 4, exactly one WARN-level alarm is emitted on the WebSocket alarm channel, with the originating plugin identifier indicating the forecast evaluator.
