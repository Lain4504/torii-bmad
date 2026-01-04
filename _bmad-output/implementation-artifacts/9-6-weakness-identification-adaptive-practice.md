# Story 9.6: Weakness Identification & Adaptive Practice

Status: ready-for-dev

## Story

As a Learner,
I want the system to identify my weak areas and recommend specific practice,
so that I can study more efficiently.

## Acceptance Criteria

1. **Analysis**:
   - System tracks error rates by Tag (e.g., "Particle-ni", "Kanji-Radicals").
2. **Notification/Highlight**:
   - "You seem to simulate 'Conditional Forms' poorly (40% accuracy)."
3. **Adaptive Action**:
   - "Take a targeted quiz" button (Links to 9-1).
   - "Review these 3 lessons" (Links to Course Connect).

## Tasks / Subtasks

- [ ] Implement Analytics Engine
  - [ ] Track detailed answer logs.
  - [ ] Aggregate stats by tag.
- [ ] Build Recommendation UI
  - [ ] "Focus Area" card on dashboard.

## Dev Notes

### Technical Requirements
- Data-heavy. Ensure DB indexing on tags.

### References
- Epic 9, FR22, FR23.
