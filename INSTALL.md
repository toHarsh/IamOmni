# Installation Guide

This guide shows how to install the AI harnesses that IamOmni currently supports and how to start each one with the shared context protocol.

Installation commands change over time. When in doubt, prefer the official documentation linked in each section.

## Prerequisites

- A terminal shell: Zsh, Bash, Fish, PowerShell, or WSL.
- Node.js 18+ for npm-based installs.
- Git if the harness needs repository context or Windows Git Bash support.
- Provider account or API access for the harness you plan to use.

## Claude Code

Official docs: https://code.claude.com/docs/en/getting-started

Install with npm:

```sh
npm install -g @anthropic-ai/claude-code
```

Alternative native installer for macOS, Linux, and WSL:

```sh
curl -fsSL https://claude.ai/install.sh | bash
```

Verify:

```sh
claude --version
```

Start in this repository:

```sh
cd /Users/harshkothari/Documents/Projects/IamOmni
claude
```

Startup prompt:

```text
Read CLAUDE.md and follow the shared .ai protocol.
Continue from .ai/handoff.md and .ai/session-log.md.
After every response, update the session log and transcript according to .ai/protocol.md.
```

## Codex CLI

Official docs: https://developers.openai.com/codex/cli

Install with npm:

```sh
npm install -g @openai/codex
```

Authenticate with your OpenAI account or API key according to the current Codex CLI docs.

Verify:

```sh
codex --version
```

Start in this repository:

```sh
cd /Users/harshkothari/Documents/Projects/IamOmni
codex
```

Startup prompt:

```text
Read AGENTS.md and follow the shared .ai protocol.
Continue from .ai/handoff.md and .ai/session-log.md.
After every response, update the session log and transcript according to .ai/protocol.md.
```

## Gemini CLI

Official docs: https://github.com/google-gemini/gemini-cli

Run without installing:

```sh
npx @google/gemini-cli
```

Install with npm:

```sh
npm install -g @google/gemini-cli
```

Alternative Homebrew install for macOS and Linux:

```sh
brew install gemini-cli
```

Verify:

```sh
gemini --version
```

Start in this repository:

```sh
cd /Users/harshkothari/Documents/Projects/IamOmni
gemini
```

Startup prompt:

```text
Read GEMINI.md and follow the shared .ai protocol.
Continue from .ai/handoff.md and .ai/session-log.md.
After every response, update the session log and transcript according to .ai/protocol.md.
```

## OpenCode

Official docs: https://opencode.ai/docs/

Install with the official install script:

```sh
curl -fsSL https://opencode.ai/install | bash
```

Install with npm:

```sh
npm install -g opencode-ai
```

Recommended Homebrew install for macOS and Linux:

```sh
brew install anomalyco/tap/opencode
```

Verify:

```sh
opencode --version
```

Start in this repository:

```sh
cd /Users/harshkothari/Documents/Projects/IamOmni
opencode
```

Startup prompt:

```text
Read opencode.md and follow the shared .ai protocol.
Continue from .ai/handoff.md and .ai/session-log.md.
After every response, update the session log and transcript according to .ai/protocol.md.
```

## Omni Token Hook

For any harness that supports saved prompts, custom instructions, hooks, snippets, or composer templates, add this text:

```text
Track Omni token metrics for this exchange:
- tokens consumed to capture required context
- tokens saved by using compact context transfer instead of raw chat history
Prefer exact harness token counts when available; otherwise estimate and mark as estimated.
```

## Cross-Harness Workflow

1. Install the harness you want to use.
2. Open this repository in the harness.
3. Paste the matching startup prompt.
4. Let the harness read `.ai/protocol.md` and the current `.ai` context files.
5. After each exchange, confirm the harness updates `.ai/session-log.md`, `.ai/transcripts/`, `.ai/changed-files.md`, and token metrics.
6. Before switching to another harness, ask the current harness to update `.ai/handoff.md`.
