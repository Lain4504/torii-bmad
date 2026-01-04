# Story 6.3: Auto-grading Results

Status: ready-for-dev

## Story

As a Learner,
I want to see my exam score immediately after submission, broken down by section,
so that I can know if I passed and where I need to improve.

## Acceptance Criteria

1. **Score Calculation**:
   - Calculate total score and sectional scores.
   - Determine "Pass/Fail" based on JLPT rules (Overall cutoff + Sectional cutoffs).

2. **Results Page**:
   - Big Score / Pass/Fail Badge.
   - Radial/Bar chart for Sectional performance (Vocab, Grammar, Reading, Listening).
   - Comparisons to average (optional leaderboards - Epic 12).

3. **Answer Key**:
   - Review each question.
   - Show User Answer vs Correct Answer.
   - Explanations (if available).

## Tasks / Subtasks

- [ ] Implement Grading Logic (Backend)
  - [ ] Assessment Service triggers grading on submit.
  - [ ] Store `ExamResult`.
- [ ] Build Results Details UI
  - [ ] Score visualization (Charts).
  - [ ] Question review verification list.

## Dev Notes

### Technical Requirements
- **Recharts** (Web) or **fl_chart** (Mobile) for graphs.

### References
- Epic 6, FR9.
