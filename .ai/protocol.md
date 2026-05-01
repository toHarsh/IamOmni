# AI Context Protocol

This protocol is designed to work across Claude, Codex, OpenCode, Gemini CLI, and other AI coding tools.

## Source Of Truth

The repository state is the source of truth.

Context files are navigation aids. If a context file conflicts with actual code, inspect the code and record the correction in `.ai/session-log.md`.

## Start Of Session

Before doing work, read:

- `.ai/brief.md`
- `.ai/handoff.md`
- `.ai/session-log.md`
- `.ai/changed-files.md`

Read transcript files only when the compact context is ambiguous or incomplete.

## After Every Exchange

After every user/assistant exchange, append a compact entry to `.ai/session-log.md`.

Use this format:

```md
## YYYY-MM-DD HH:mm TZ - MODEL - turn-NNN

User intent:
- ...

Assistant action:
- ...

Files inspected:
- None

Files created:
- None

Files updated:
- None

Files deleted:
- None

Commands run:
- None

Decisions:
- None

Assumptions:
- None

Token metrics:
- Context capture tokens consumed: unavailable
- Context transfer tokens saved: unavailable
- Token count source: unavailable

Next step:
- ...

Transcript:
- .ai/transcripts/YYYY-MM-DD-MODEL.md#turn-NNN
```

Keep each entry compact. Prefer 50-150 words unless the turn changed many files.

## Token Metrics

Omni tracks the token cost and savings of context transfer in each session-log entry.

- `Context capture tokens consumed`: tokens spent writing or updating required Omni context for the exchange.
- `Context transfer tokens saved`: tokens avoided by transferring compact Omni context instead of making the next AI harness read raw chat history or rediscover the same state.
- `Token count source`: `exact`, `estimated`, or `unavailable`.

Use exact token counts when the current AI harness exposes reliable token accounting. Otherwise estimate from the captured and avoided text size, and mark the source as `estimated`. Use `unavailable` only when neither exact counts nor a reasonable estimate are available.

## Omni Token Hook

Use this reusable prompt snippet in AI harnesses that support visible prompt hooks near the input composer:

```text
Track Omni token metrics for this exchange:
- tokens consumed to capture required context
- tokens saved by using compact context transfer instead of raw chat history
Prefer exact harness token counts when available; otherwise estimate and mark as estimated.
```

## Transcript Policy

Append the relevant transcript to:

```text
.ai/transcripts/YYYY-MM-DD-MODEL.md
```

Use this format:

```md
## turn-NNN

### User
Exact user message when possible.

### Assistant
Exact assistant response if short.

For long responses, use a compact summary and preserve:
- file paths
- commands
- decisions
- blockers
- final answer
```

Do not paste huge generated code blocks into transcript files. Reference the changed files instead.

## Changed Files Index

When files are created, updated, deleted, or heavily inspected, update `.ai/changed-files.md`.

Keep it append-only unless the user asks for cleanup.

## Handoff Policy

Update `.ai/handoff.md`:

- after every exchange when the current state changed
- immediately when the AI harness reports 5% or less context remaining
- before switching tools or models
- before ending intentionally
- after major implementation changes
- after major decisions
- after resolving a blocker

The handoff should summarize current state, not the full conversation.

Do not wait until the context limit is reached. If exact remaining-context telemetry is unavailable, treat these as warning signs and refresh `.ai/handoff.md` before continuing:

- the model warns that context is almost full
- the conversation has become long enough that prior details may be truncated
- a large file, transcript, log, build output, or diff was read
- a major decision, blocker, or implementation step just happened

When 5% or less context remains, prioritize this minimal emergency handoff sequence before any other work:

1. Update `.ai/handoff.md` with current state, completed work, blockers, and next step.
2. Append the current exchange to `.ai/session-log.md`.
3. Append or summarize the current exchange in the active transcript file.
4. Update `.ai/changed-files.md` for files touched or heavily inspected.

If there is not enough context left for full bookkeeping, update `.ai/handoff.md` first.

## Safety Rules

- Do not overwrite user changes.
- Do not rewrite old log or transcript entries unless explicitly asked.
- Mark assumptions clearly.
- Mark unverified claims clearly.
- Prefer append-only updates.
- Keep tool-specific behavior out of this protocol where possible.

## Universal Startup Prompt

```text
Read .ai/protocol.md first and follow it for this session.
Continue from .ai/brief.md, .ai/handoff.md, .ai/session-log.md, and .ai/changed-files.md.
After every response, append the session log and transcript entries required by the protocol.
```
