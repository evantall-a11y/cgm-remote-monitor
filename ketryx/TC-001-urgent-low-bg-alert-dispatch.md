---
itemId: TC-001
itemType: Test Case
itemTests: SRS-001
---
# TC-001 — Urgent low BG alert dispatch verification

**Preconditions:**
- A test instance of the monitoring server is running with the alarm subsystem enabled.
- User settings have `alarmUrgentLow` enabled and the urgent low threshold (`bgLow`) configured to 55 mg/dL.
- A subscribed alarm-socket client is connected and authorized.
- No prior acknowledgment is active for the default alarm group.

**Steps:**
1. Inject a glucose entry with a value of 50 mg/dL and a timestamp equal to the current evaluation time.
2. Trigger one notification evaluation cycle.
3. Capture the events emitted on the alarm socket's default namespace during the cycle.

**Expected Result:**
Exactly one `urgent_alarm` event is emitted on the alarm-socket default namespace within the same evaluation cycle, and the event payload identifies severity URGENT and an event name corresponding to the low condition. No `alarm` (WARN) event is emitted for the same group in the same cycle. **Pass / fail:** pass if both the presence of the URGENT event and the absence of a WARN event for the same group are observed; fail otherwise.
