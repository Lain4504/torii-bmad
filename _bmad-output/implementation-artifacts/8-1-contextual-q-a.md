# Story 8.1: Contextual Q&A (AI Sensei)

Status: ready-for-dev

## Story

As a Learner,
I want to ask the AI Sensei questions about vocabulary or grammar I encounter during lessons,
so that I can get instant clarification without leaving the platform.

## Acceptance Criteria

1. **Chat Widget**:
   - Floating chat button or sidebar in Lesson View.
   - Chat history persistence (per session or permanent).

2. **Context Awareness**:
   - If opened from a Video Lesson: AI knows the current video transcripts/topic.
   - If selected text: AI uses selected text as context.

3. **Response Quality**:
   - Responses should be polite, encouraging, and accurate (Japanese teacher persona).
   - Support Markdown rendering (bolding key terms).

## Tasks / Subtasks

- [ ] Implement Chat API
  - [ ] POST `/api/v1/cortex/chat` { message, context: { contentId, text } }
- [ ] Build Chat UI
  - [ ] Chat bubble component.
  - [ ] Typing indicators.
- [ ] Cortex Service Logic
  - [ ] Integrate LLM (Gemini/OpenAI) via FastMCP or direct.
  - [ ] Prompt Engineering for "Sensei" persona.

## Dev Notes

### Technical Requirements
- **Web**: Re-use `ai-sdk` (Vercel) or custom stream handling.
- **Mobile**: Flutter `dash_chat_2` or custom UI.
- **Stream**: Server-Sent Events (SSE) or simple POST for MVP.

### References
- Epic 8, FR14.
- FastMCP (Story 8-4).
