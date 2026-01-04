# Story 5.1: Flashcard Deck Display

Status: ready-for-dev

## Story

As a Learner,
I want to view my flashcard decks organized by course or topic,
so that I can select what to study.

## Acceptance Criteria

1. **Deck Listing**:
   - List available flashcard decks (system-generated from courses).
   - Indicate "New", "Learning", "Review" card counts for each deck (SRS status).
   - Progress bar or mastery percentage per deck.

2. **Deck Details**:
   - Click/Tap deck to view stats (Total cards, Mastery level).
   - "Start Study" button.

3. **Organization**:
   - Group by Course/Module.

## Tasks / Subtasks

- [ ] Implement Deck List API
  - [ ] GET `/api/v1/flashcards/decks`
- [ ] Build Deck Card UI
  - [ ] Web: Card with progress bar.
  - [ ] Mobile: List tile or card with visual SRS stats.
- [ ] Integrate SRS Stats
  - [ ] Display "Due today" count prominently.

## Dev Notes

### Technical Requirements
- Web: Next.js.
- Mobile: Flutter. Use `Drift` for local caching of deck stats if offline (Story 5-3 covers offline, but data structure should support it).

### Architecture Compliance
- `FlashcardDeck` entity.
- `FlashcardStats` value object.

### References
- PRD FR12.
- Epic 5.
