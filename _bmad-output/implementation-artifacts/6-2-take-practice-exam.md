# Story 6.2: Take Practice Exam

Status: ready-for-dev

## Story

As a Learner,
I want to take a timed JLPT practice exam with proper sections (Vocab, Grammar, Reading, Listening),
so that I can simulate the real test environment.

## Acceptance Criteria

1. **Test Interface**:
   - Display current question and options (Radio buttons).
   - Sidebar/Bottom sheet navigation (Question 1, 2, ... 50).
   - Flag/Mark for review functionality.
   
2. **Timer**:
   - Countdown timer based on section limit.
   - Auto-submit on zero.

3. **Listening Section**:
   - Audio player for listening questions.
   - Prevent pausing/scrubbing if simulating real exam (strict mode), or allow (practice mode). Default: Allow control for MVP.

4. **Progress Saving**:
   - Auto-save answers every X seconds or on change (to prevent data loss, NFR17).

## Tasks / Subtasks

- [ ] Implement Take Exam API
  - [ ] POST `/api/v1/exams/:id/start` -> returns Session ID.
  - [ ] PUT `/api/v1/exams/sessions/:sessionId/answers` -> save progress.
  - [ ] POST `/api/v1/exams/sessions/:sessionId/submit` -> finish.
- [ ] Build Exam Runner UI
  - [ ] Validated Single Choice Input.
  - [ ] Timer Widget.
  - [ ] Audio Player integration.

## Dev Notes

### Technical Requirements
- **State Management**: Complex local state (answers map). Sync frequently.
- **Security**: Prevent accessing answers from browser inspection (Questions shouldn't include `isCorrect` flag in payload).

### References
- Epic 6, FR9.
