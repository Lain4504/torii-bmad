# Story 12.5: Push Notifications (Mobile)

Status: ready-for-dev

## Story

As a Mobile Learner,
I want to receive push notifications for important events like class reminders and daily goals,
so that I stay engaged with my learning.

## Acceptance Criteria

1. **Functionality**:
   - Receive notification when app is backgrounded or terminated.
   - Tap notification opens relevant screen (Deep linking).
2. **Triggers**:
   - "Live Class starting in 15 mins".
   - "Keep your streak alive! Practice now." (Daily at 8 PM if not studied).
   - "Your assignment was graded."
3. **Settings**:
   - User can toggle notifications On/Off per category.

## Tasks / Subtasks

- [ ] Setup Firebase Cloud Messaging (FCM).
  - [ ] Configure Flutter client.
  - [ ] Configure Backend sender (Notification Service).
- [ ] Implement Device Token management.
  - [ ] Store FCM tokens for `User`.
- [ ] Implement Scheduler/Trigger system.

## Dev Notes

### Technical Requirements
- **Flutter**: `firebase_messaging`.
- **Backend**: `firebase-admin` SDK.

### References
- Epic 12, FR63.
