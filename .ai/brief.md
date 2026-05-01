# Brief

## Goal

Create a model-agnostic context transfer system that works across Claude, Codex, OpenCode, Gemini CLI, and future AI coding tools.

## Principles

- Durable context lives in files, not chat memory.
- Per-turn updates are append-only and compact.
- Handoff state is maintained proactively before context limits are reached.
- Full transcript details are stored separately from the main session log.
- Token metrics track context capture cost and transfer savings when available.
- Tool-specific files are thin adapters that point to `.ai/protocol.md`.
- The repository state remains the source of truth.

## Non-Goals

- Do not create a heavy framework.
- Do not depend on one AI vendor or one CLI.
- Do not require rewriting all context files after every message.
