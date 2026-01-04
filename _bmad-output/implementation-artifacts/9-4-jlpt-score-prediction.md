# Story 9.4: JLPT Score Prediction

Status: ready-for-dev

## Story

As a Learner,
I want to see a prediction of my potential JLPT score and pass probability,
so that I can gauge my readiness for the real exam.

## Acceptance Criteria

1. **Prediction Widget**:
   - "Estimated N[X] Score: 90/180".
   - "Pass Probability: High/Medium/Low".
2. **Five Pillars Visualization**:
   - Radar chart showing balance (Vocab/Grammar/Reading/Listening/Kanji).
   - "Your weakest pillar is Listening". (FR20).
3. **Data Source**:
   - Based on Mock Exams and Practice Quiz performance.

## Tasks / Subtasks

- [ ] Implement Prediction Algorithm
  - [ ] Weighted average of recent performance.
  - [ ] Simple heuristic or Machine Learning model (start simple).
- [ ] Build Analytics Dashboard Widget.
 
## Dev Notes

### Technical Requirements
- Backend calculation job (Nightly or on-demand).

### References
- Epic 9, FR20.
