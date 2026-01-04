# Story 8.2: Grammar Correction

Status: ready-for-dev

## Story

As a Learner,
I want to submit Japanese sentences I've written and get corrections/explanations,
so that I can improve my writing skills.

## Acceptance Criteria

1. **Input Interface**:
   - Text area for Japanese writing.
   - "Check Grammar" button.

2. **Output format**:
   - Show original vs corrected text (Diff view).
   - Bullet points explaining specific grammar rules violated.

3. **History**:
   - Save corrections to "My Writing" log (optional MVP).

## Tasks / Subtasks

- [ ] Implement Correction API
  - [ ] POST `/api/v1/cortex/correct`
- [ ] Build Writing UI
  - [ ] Diff visualizer (Green additions, Red deletions).

## Dev Notes

### Technical Requirements
- Use `diff-match-patch` library for visualizing text differences.

### References
- Epic 8, FR15.
