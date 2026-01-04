# Story 5.4: Flashcard Progress Sync

Status: ready-for-dev

## Story

As a Learner,
I want my flashcard progress to sync between my mobile device and the web,
so that I can switch devices without losing my study streaks or SRS intervals.

## Acceptance Criteria

1. **Background Sync**:
   - Mobile app syncs with server when internet is available.
   - Pushes local review logs.
   - Pulls updated deck stats/intervals from server.

2. **Conflict Resolution**:
   - Merge strategy: New review logs are appended.
   - SRS Intervals: Latest review timestamp wins, or server recalculates based on merged history.

3. **Optimistic UI**:
   - Show "Synced" status indicator (Last synced: 2 mins ago).

## Tasks / Subtasks

- [ ] Implement Sync Endpoint
  - [ ] POST `/api/v1/flashcards/sync` accepts JSON dump of review logs.
  - [ ] Returns updated card states.
- [ ] Mobile Sync Service
  - [ ] `SyncManager` class in Flutter.
  - [ ] Trigger on connection restore + periodic.

## Dev Notes

### Technical Requirements
- **Protobuf** recommended for efficient sync of large datasets (Arch Doc).
- **Mobile**: `connectivity_plus` to detect network.

### References
- PRD NFR31, NFR33.
