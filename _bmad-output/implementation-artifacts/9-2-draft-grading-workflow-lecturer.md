# Story 9.2: Draft Grading Workflow (Lecturer)

Status: ready-for-dev

## Story

As a Lecturer,
I want to see AI-generated draft grades and feedback for student assignments,
so that I can grade faster by simply reviewing and approving them.

## Acceptance Criteria

1. **Pending Grades List**:
   - List assignments waiting for review.
   - Indicator: "AI Draft Ready".
2. **Review Interface**:
   - Split screen: Student Work vs Grading Panel.
   - Grading Panel is pre-filled with:
     - Score (based on rubric).
     - Feedback comments.
     - Highlighted corrections.
3. **Action**:
   - "Edit" (Modify score/feedback).
   - "Approve & Publish" (Send to student).

## Tasks / Subtasks

- [ ] Implement Draft Grading API
  - [ ] GET `/api/v1/grading/drafts`
  - [ ] POST `/api/v1/grading/publish`
- [ ] Build Grading UI
  - [ ] Assignment Viewer.
  - [ ] Rubric filling component.

## Dev Notes

### Technical Requirements
- AI Agent (Assessment) runs on submission to generate draft. Stores in `GradingDraft` table.

### References
- Epic 9, FR18, FR29.
