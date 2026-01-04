# Story 8.3: Auto-generate Flashcards

Status: ready-for-dev

## Story

As a Learner,
I want the system to automatically generate flashcards from a text or lesson I'm studying,
so that I can quickly build my vocabulary deck without manual entry.

## Acceptance Criteria

1. **Extraction**:
   - Select text or supply a URL/Topic.
   - AI identifies key vocabulary/grammar points.

2. **Preview & Edit**:
   - Show generated cards (Front/Back) in a list.
   - Allow user to uncheck/edit before adding.

3. **Add to Deck**:
   - "Add selected to Deck [X]" action.

## Tasks / Subtasks

- [ ] Implement Generation API
  - [ ] POST `/api/v1/cortex/generate-cards`
- [ ] Build Generation Modal
  - [ ] Bulk editor UI.

## Dev Notes

### Technical Requirements
- Structured Output from LLM (JSON) is critical here. Using `zod` schema with AI SDK.

### References
- Epic 8, FR16.
