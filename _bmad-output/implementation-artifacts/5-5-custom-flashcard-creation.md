# Story 5.5: Custom Flashcard Creation

Status: ready-for-dev

## Story

As a Learner,
I want to create my own flashcard decks and cards,
so that I can study specific vocabulary not covered in the official courses.

## Acceptance Criteria

1. **Create Deck**:
   - Name, description, tags.
2. **Add Card**:
   - Fields: Front (Kanji/Word), Back (Meaning), Reading (Kana), Example Sentence (optional).
   - Support image upload (optional).
3. **Edit/Delete**:
   - Manage own decks and cards.
4. **Visibility**:
   - Private by default. Warning if sharing (User Generated Content policy).

## Tasks / Subtasks

- [ ] Implement CRUD API
  - [ ] POST/PUT/DELETE `/api/v1/flashcards/decks`
  - [ ] POST/PUT/DELETE `/api/v1/flashcards/cards`
- [ ] Build UI
  - [ ] Form for Deck creation.
  - [ ] Form for Card creation (Web & Mobile).

## Dev Notes

### Technical Requirements
- Standard CRUD.
- Input validation (Zod).

### References
- Epic 5.
