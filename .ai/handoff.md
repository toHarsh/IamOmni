# Handoff

## Current State

IamOmni has been scaffolded as a lightweight AI context protocol project. A root-level `context.md` provides a human-readable overview. Omni token metrics are now part of the protocol: each session-log entry can record context capture tokens consumed, context transfer tokens saved, and whether counts are exact, estimated, or unavailable. `INSTALL.md` now documents installation and startup for Claude Code, Codex CLI, Gemini CLI, and OpenCode. Git was initialized locally and `main` was pushed to `https://github.com/toHarsh/IamOmni.git`.

## Important Files

- `.ai/protocol.md`: shared protocol every AI tool should follow.
- `.ai/session-log.md`: compact append-only per-turn log.
- `.ai/transcripts/`: detailed transcript archive.
- `.ai/changed-files.md`: append-only file operation index.
- `INSTALL.md`: installation guide and startup prompts for supported harnesses.
- `context.md`: human-readable overview, including token metrics.
- `CLAUDE.md`, `AGENTS.md`, `GEMINI.md`, `opencode.md`: thin tool-specific adapters.

## Next Step

Use the universal startup prompt from `.ai/protocol.md` in Claude, Codex, OpenCode, Gemini CLI, or another tool. Current immediate next step is optional: add `INSTALL.md` references to the individual adapter files.

## Verification

Verified by direct file reads and targeted `rg` search. Install commands were checked against official docs before being written. Repository was pushed to GitHub successfully. Not yet verified by installing/running each AI tool locally.
