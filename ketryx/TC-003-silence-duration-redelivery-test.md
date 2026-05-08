---
itemId: TC-003
itemType: Test Case
itemTests:
  - SRS-003
---
# TC-003 — Acknowledged alarm is not re-emitted within its silence duration

**Preconditions:**
- The notification subsystem is running with default plugin registration.
- User settings have urgent-high enabled at 200 milligrams per decilitre.
- The system internal event bus is observed by a recording listener that captures every emitted notification.
- No prior alarm has been acknowledged for the test group.

**Steps:**
1. Submit a sensor reading of 220 milligrams per decilitre with a timestamp equal to the current evaluation time.
2. Trigger one notification-evaluation cycle and confirm that exactly one Urgent notification is emitted on the internal event bus and recorded by the listener.
3. Submit an acknowledgement for severity Urgent, default group, with a silence duration of 600 000 milliseconds (10 minutes).
4. Without advancing simulated time beyond 9 minutes from the acknowledgement, submit a second sensor reading of 230 milligrams per decilitre with a fresh timestamp.
5. Trigger a second notification-evaluation cycle.

**Expected result:**
- After step 2, the recording listener contains exactly one Urgent notification.
- After step 5, the recording listener still contains exactly one Urgent notification (the second cycle does not emit a new Urgent notification, because the alarm is within its 10-minute silence window).
