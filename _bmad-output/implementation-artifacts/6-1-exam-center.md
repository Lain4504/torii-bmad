# Story 6.1: Exam Center

Status: ready-for-dev

## Story

As a Learner,
I want to browse available JLPT practice exams and see my history,
so that I can choose a test to take or review my past performance.

## Acceptance Criteria

1. **Exam List**:
   - Filter by N Level (N5-N1).
   - Show "Full Test" vs "Mini Test".
   - Status indicators: "New", "In Progress", "Completed (Score)".
   
2. **History View**:
   - List of past attempts with dates and scores.
   - "Review Results" button.

## Tasks / Subtasks

- [ ] Implement Exam List API
  - [ ] GET `/api/v1/exams`
  - [ ] GET `/api/v1/exams/attempts` (History)
- [ ] Build UI
  - [ ] Exam Catalog page.
  - [ ] Results generic view (entry point).

## Dev Notes

### Technical Requirements
- **Web**: `app/exams/page.tsx`.
- **Mobile**: `ExamTab`.

### References
- Epic 6, FR9.
