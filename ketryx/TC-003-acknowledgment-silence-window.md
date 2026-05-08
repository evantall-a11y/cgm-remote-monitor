---
itemId: TC-003
itemType: Test Case
itemTests: SRS-003
---
# TC-003 — Acknowledgment silence window verification

**Preconditions:**
- A test instance of the monitoring server is running with the alarm subsystem enabled.
- User settings have `alarmUrgentLow` enabled and the urgent low threshold configured to 55 mg/dL.
- A subscribed alarm-socket client is connected and authorized to acknowledge.
- No prior acknowledgment is active for the default alarm group.

**Steps:**
1. Inject a glucose entry of 50 mg/dL with a current timestamp and run an evaluation cycle; verify an `urgent_alarm` is emitted.
2. Send an acknowledgment from the connected client for severity URGENT, default group, with a silence duration of 30 minutes.
3. Inject a second glucose entry of 50 mg/dL with a timestamp 5 minutes after the first and run a second evaluation cycle.
4. Capture the events emitted on the alarm-socket default namespace during the second cycle.

**Expected Result:**
No `urgent_alarm` and no `alarm` event is emitted on the alarm-socket default namespace during the second cycle for the default group, while the underlying condition remains active. **Pass / fail:** pass if the second cycle emits no URGENT or WARN event in the default group; fail if any URGENT or WARN event for the default group is observed in that cycle.
