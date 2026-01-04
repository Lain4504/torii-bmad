# Story 8.4: FastMCP Integration

Status: ready-for-dev

## Story

As a Developer,
I want to integrate the FastMCP protocol into the Cortex Service,
so that our AI agents can reliably call system tools and access data context.

## Acceptance Criteria

1. **FastMCP Server**:
   - Cortex service acts as an MCP server or client (depending on architecture - usually Agent is Client, Cortex might expose Tools OR Cortex *is* the Agent host using MCP to talk to other services). 
   - *Correction*: In this architecture, Cortex is the AI Orchestrator. It likely uses MCP to connect to LLMs and Local Tools. Or provides an MCP server for *other* agents.
   - Requirement: "FastMCP integration" usually means implementing the protocol for tool calling.

2. **Tool Definitions**:
   - Define tools: `search_dictionary`, `get_course_content`, `check_grammar_rules`.
   - Expose these tools to the LLM agent via FastMCP.

3. **Connection**:
   - Stable connection between Cortex Service and Tools.

## Tasks / Subtasks

- [ ] Setup FastMCP boilerplate in `apps/cortex`.
- [ ] Implement `DictionaryTool`.
- [ ] Implement `CourseContextTool`.
- [ ] Test Tool Calling with valid prompts.

## Dev Notes

### Technical Requirements
- `fastmcp` TypeScript library (if available) or raw MCP implementation.
- This creates the "Brain" backing Stories 8-1, 8-2, 8-3.

### References
- Epic 8, FR14-25.
