# Story 5.2: SRS Flashcard Practice

Status: ready-for-dev

## Story

As a Learner,
I want to practice flashcards using a Spaced Repetition System (SRS),
so that I can efficiently memorize vocabulary.

## Acceptance Criteria

1. **Study Session Interface**:
   - Show Front of card (Kanji/Word).
   - Tap to flip -> Show Back (Meaning, Reading, Audio).
   - Rate recall: "Again", "Hard", "Good", "Easy".
   
2. **SRS Algorithm**:
   - Backend (or local logic) schedules next review based on rating (e.g., FSRS or SM-2).
   - "Again" -> Shows again in < 1 min.
   - "Easy" -> Pushes due date far into future.

3. **Audio Playback**:
   - Auto-play audio on flip (optional setting).
   - Button to replay audio.

4. **Session Summary**:
   - End of session screen showing cards studied, accuracy.

## Tasks / Subtasks

- [ ] Implement Study Logic
  - [ ] Fetch "Due" cards: GET `/api/v1/flashcards/study?deckId=...`
  - [ ] Queue management (Frontend).
- [ ] Build Flashcard UI component
  - [ ] Flip animation (CSS transform / Flutter `AnimationController`).
  - [ ] Action buttons (Rating) - keyboard shortcuts on Web (1, 2, 3, 4).
- [ ] Submit Results
  - [ ] POST `/api/v1/flashcards/review` (Batch or per card).
  - [ ] Update local state immediately.

## Dev Notes

### Technical Requirements
- **Mobile**: Heavy interaction. Performance is key. Use `Drift` to store review logs immediately, sync later (Story 5-4) or send API if online.
- **Web**: React Spring or similar for flip animation.

### Architecture Compliance
- SRS Algorithm ideally shared logic or defined consistently.

### References
- PRD FR12.
