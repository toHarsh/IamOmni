# IamOmni Context

IamOmni is a model-agnostic context transfer system for AI coding sessions.

It is meant to help work move cleanly between tools like Claude, Codex, OpenCode, Gemini CLI, and future AI agents without relying on hidden chat memory or one vendor's session format.

## Core Idea

Every AI tool should treat the repository files as the source of truth.

Instead of depending on a long chat history, each tool reads the shared `.ai` files at the start of a session and writes compact updates after each exchange.

This makes the project more resilient when:

- a model hits its context limit
- a session gets interrupted
- work moves from one AI tool to another
- a different model needs to continue from the current state
- teams want to understand how many tokens Omni spends and saves during transfer

## Important Files

- `.ai/protocol.md`: the main shared protocol every AI tool should follow.
- `.ai/brief.md`: the stable goal and principles of the project.
- `.ai/session-log.md`: append-only per-turn log, updated after every exchange.
- `.ai/transcripts/`: transcript archive with fuller details when needed.
- `.ai/handoff.md`: compact current-state summary for switching models or ending a session.
- `.ai/changed-files.md`: append-only index of files created, updated, deleted, or heavily inspected.
- `INSTALL.md`: installation guide for supported AI harnesses.
- `context.md`: human-readable project overview.
- `CLAUDE.md`: Claude-specific adapter that points to the shared protocol.
- `AGENTS.md`: Codex/agent-style adapter that points to the shared protocol.
- `GEMINI.md`: Gemini CLI adapter that points to the shared protocol.
- `opencode.md`: OpenCode adapter that points to the shared protocol.
- `adapters/`: copy-paste startup prompts for each supported tool.

## How To Use It

At the start of any AI session, tell the tool:

```text
Read .ai/protocol.md first and follow it for this session.
Continue from .ai/brief.md, .ai/handoff.md, .ai/session-log.md, and .ai/changed-files.md.
After every response, append the session log and transcript entries required by the protocol.
```

During the session, the AI should:

- append a compact entry to `.ai/session-log.md` after every exchange
- append transcript details to `.ai/transcripts/YYYY-MM-DD-MODEL.md`
- record token metrics for context captured and context-transfer savings
- update `.ai/changed-files.md` when files are touched
- update `.ai/handoff.md` before switching tools, stopping intentionally, or after major changes

## Token Metrics

IamOmni tracks token efficiency as part of the session log:

- `Context capture tokens consumed`: tokens spent recording required Omni context for the exchange.
- `Context transfer tokens saved`: tokens avoided because another AI harness can read compact Omni context instead of raw chat history.
- `Token count source`: whether the values are exact, estimated, or unavailable.

Exact token counts should be used when a harness exposes them. Otherwise, Omni uses reasonable estimates and marks them as estimated.

## Why This Exists

Raw transcripts are useful, but they are noisy and expensive for another model to process.

IamOmni separates context into layers:

- `session-log.md` gives a compact chronological index
- `transcripts/` stores detailed conversation records
- `handoff.md` gives the current working state
- `changed-files.md` shows where work happened
- token metrics show the efficiency gained by compact transfer
- `protocol.md` defines the rules all tools follow

This gives crash-safety without forcing the model to rewrite large summaries after every message.

## Design Rule

Prefer append-only updates.

Do not rewrite old log or transcript entries unless explicitly requested. If something is wrong or outdated, add a new correction entry instead.
