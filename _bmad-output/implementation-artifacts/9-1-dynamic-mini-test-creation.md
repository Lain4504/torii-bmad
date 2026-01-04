# Story 9.1: Dynamic Mini-test Creation

Status: ready-for-dev

## Story

As a Learner,
I want to take a short, dynamically generated quiz based on my recent mistakes or study activity,
so that I can reinforce my learning efficiently.

## Acceptance Criteria

1. **Generation Trigger**:
   - "Practice Weak Areas" button on Dashboard.
   - Auto-generated "Daily Quiz".

2. **Content selection**:
   - Algorithm selects questions tagging user's "weak" concepts (from SRS or past exam errors).
   - If not enough data, random selection from current level.

3. **Format**:
   - Short (5-10 questions).
   - Immediate feedback.

## Tasks / Subtasks

- [ ] Implement Quiz Generator
  - [ ] POST `/api/v1/assessment/generate-mini-test`
  - [ ] Logic: Query `UserMetadata` for weak tags -> Query `QuestionBank`.
- [ ] Build Quiz Runner
  - [ ] Re-use Exam Runner UI (Story 6-2) or simplified version.

## Dev Notes

### Technical Requirements
- Efficient tagging system in Postgres (e.g., `question_tags`, `user_weakness_tags`).

### References
- Epic 9, FR17, FR22.
