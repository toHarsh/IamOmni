# IamOmni

IamOmni is a lightweight, AI-agnostic context transfer protocol for moving work between Claude, Codex, OpenCode, Gemini CLI, and other coding agents.

The core idea is simple:

- Keep durable context in project files.
- Append compact logs after every exchange.
- Store transcript details separately.
- Use thin adapter files for each AI tool.
- Track tokens consumed and saved by context transfer.
- Treat the repository state as the source of truth.

## Structure

```text
.ai/
  protocol.md
  brief.md
  session-log.md
  handoff.md
  changed-files.md
  transcripts/
INSTALL.md
context.md
CLAUDE.md
AGENTS.md
GEMINI.md
opencode.md
adapters/
```

## Installation

See `INSTALL.md` for current installation commands and startup prompts for Claude Code, Codex CLI, Gemini CLI, and OpenCode.

## Start A New AI Session

Use this prompt in any tool:

```text
Read .ai/protocol.md first and follow it for this session.
Continue from .ai/brief.md, .ai/handoff.md, .ai/session-log.md, and .ai/changed-files.md.
After every response, append the session log and transcript entries required by the protocol.
```

## Token Metrics

IamOmni tracks context-transfer efficiency in `.ai/session-log.md`.

Each exchange records tokens consumed to capture required context and tokens saved by transferring compact Omni context across AI harnesses instead of replaying raw chat history. Exact harness token counts are preferred when available; otherwise the values are estimated and marked as estimated.

## Omni Token Hook

Use this snippet in AI tools that support prompt hooks or reusable composer text:

```text
Track Omni token metrics for this exchange:
- tokens consumed to capture required context
- tokens saved by using compact context transfer instead of raw chat history
Prefer exact harness token counts when available; otherwise estimate and mark as estimated.
```

## Context Limit Safety

IamOmni does not rely on a final manual command at the moment a model hits its context limit. Each AI should keep `.ai/handoff.md` current during the session and refresh it immediately when the harness reports 5% or less context remaining.

If exact remaining-context telemetry is unavailable, refresh the handoff after long exchanges, large file reads, major implementation changes, major decisions, or blockers.

Emergency priority when context is almost full:

```text
Update .ai/handoff.md first, then .ai/session-log.md, .ai/changed-files.md, and the current transcript file according to .ai/protocol.md.
```

## Crash-Safe Rule

After every user/assistant exchange, append one compact entry to `.ai/session-log.md` and one transcript entry to `.ai/transcripts/YYYY-MM-DD-MODEL.md`.

Do not rewrite old entries unless explicitly asked.
