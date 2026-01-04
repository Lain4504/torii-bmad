# Story 9.5: Smart Exam Generator (Academic Staff)

Status: ready-for-dev

## Story

As an Academic Staff member,
I want to generate a new mock exam from our question bank matching specific criteria using natural language,
so that I can quickly create new content versions.

## Acceptance Criteria

1. **Prompt Interface**:
   - "Create a hard N3 exam focusing on Business Keigo."
2. **Generation Process**:
   - AI queries Question Bank for matching tags/difficulty.
   - Assembles 50 questions fitting the N3 structure.
3. **Review & Edit**:
   - Staff sees the generated list.
   - Can swap out questions manually.
   - Save as "Official Mock Exam V2".

## Tasks / Subtasks

- [ ] Implement Generator Tool (FastMCP).
- [ ] Build Staff Command Interface.

## Dev Notes

### Technical Requirements
- Requires well-tagged Question Bank.
- Cortex Service integration.

### References
- Epic 9, FR21, FR35.
