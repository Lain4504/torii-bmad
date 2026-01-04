# Story 9.3: Automated Writing Feedback

Status: ready-for-dev

## Story

As a Learner,
I want to receive instant automated feedback on my writing assignments,
so that I can learn from mistakes immediately before the lecturer reviews it.

## Acceptance Criteria

1. **Submission**:
   - Text input assignment.
   - On submit -> Trigger AI analysis.
2. **Instant Feedback Report**:
   - "Grammar Check" score.
   - "Vocabulary Richness" score.
   - List of mechanical errors (Typos, basic grammar).
3. **Disclaimer**:
   - "This is an automated analysis. Your lecturer will provide final grade."

## Tasks / Subtasks

- [ ] Implement Feedback Engine
  - [ ] Reuse Grammar Correction logic (8-2).
  - [ ] Add Rubric scoring logic.

## Dev Notes

### Technical Requirements
- Async processing if analysis takes > 3s. Use NATS / WebSockets for result delivery if non-blocking UI desired.

### References
- Epic 9, FR19.
