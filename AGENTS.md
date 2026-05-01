# Agent Instructions

Read and follow `.ai/protocol.md`.

This repository uses append-only context files so work can move between AI tools without relying on hidden chat memory.

Before working:

- Read `.ai/brief.md`.
- Read `.ai/handoff.md`.
- Read `.ai/session-log.md`.
- Read `.ai/changed-files.md`.

After every user/assistant exchange:

- Append a compact entry to `.ai/session-log.md`.
- Append transcript content to `.ai/transcripts/YYYY-MM-DD-MODEL.md`.
- Update `.ai/changed-files.md` when file operations happen.

Before stopping or handing off:

- Update `.ai/handoff.md`.
