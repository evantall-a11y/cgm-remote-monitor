---
itemId: TC-002
itemType: Test Case
itemTests: SRS-002
---
# TC-002 — Stale data alert at urgent staleness threshold

**Preconditions:**
- A test instance of the monitoring server is running with the alarm subsystem enabled.
- User settings have `alarmTimeagoUrgent` enabled and `alarmTimeagoUrgentMins` set to 30.
- A subscribed alarm-socket client is connected and authorized.
- The most recent glucose entry was received exactly 31 minutes before the current evaluation time.

**Steps:**
1. Advance the evaluation clock to a value 31 minutes after the most recent glucose entry's timestamp.
2. Trigger one notification evaluation cycle.
3. Capture the events emitted on the alarm-socket default namespace during the cycle.

**Expected Result:**
Exactly one `urgent_alarm` event is emitted in the Time Ago alarm group, and its payload identifies severity URGENT. **Pass / fail:** pass if the URGENT stale-data event is emitted in the Time Ago group on this cycle; fail if no event is emitted, if a WARN-only event is emitted, or if the event appears in a different alarm group.
