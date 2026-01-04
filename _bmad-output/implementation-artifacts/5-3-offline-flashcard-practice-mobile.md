# Story 5.3: Offline Flashcard Practice (Mobile)

Status: ready-for-dev

## Story

As a Mobile Learner,
I want to download flashcard decks and practice them without internet connection,
so that I can study during my commute.

## Acceptance Criteria

1. **Download Decks**:
   - "Download for Offline" toggle/button on Deck.
   - Downloads generic cards data (Text, Audio URLs).
   - Caches Audio files locally.

2. **Offline Mode**:
   - App detects offline state.
   - Allows starting a study session from local database (Drift).
   - SRS algorithm runs locally.

3. **Sync Queue**:
   - Store review results (ratings) in a local `ReviewLog` table.
   - Flag as "pending sync".

## Tasks / Subtasks

- [ ] Implement Offline Storage (Drift)
  - [ ] Tables: `LocalDeck`, `LocalCard`, `LocalReview`.
- [ ] Implement Audio Caching
  - [ ] Use `flutter_cache_manager` or custom Dio download to app storage.
- [ ] Implement Local SRS Logic
  - [ ] Replicate backend SRS interval calculation in Dart.

## Dev Notes

### Technical Requirements
- **Flutter**: `drift`, `connectivity_plus`, `dio`.
- **Sync**: See Story 5-4.

### Architecture Compliance
- Mobile Offline-First Architecture (Arch Doc).
- NFR32: 4 hours offline capability.

### References
- PRD FR13, NFR32.
