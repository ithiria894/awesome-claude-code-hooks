# Awesome Claude Code Hooks [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Curated collection of Claude Code hooks — event-driven automations that trigger before or after Claude Code actions.

Hooks are shell commands that run automatically when Claude Code performs specific actions. They're defined in `settings.json` and trigger on events like `PreToolUse`, `PostToolUse`, `Notification`, `Stop`, and more.

Looking for complete workflow recipes? See [awesome-claude-code-workflows](https://github.com/ithiria894/awesome-claude-code-workflows). Looking for tools and skills? See [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code).

## Contents

- [Security and Prompt Injection](#security-and-prompt-injection)
- [Safety and Protection](#safety-and-protection)
- [Monitoring and Observability](#monitoring-and-observability)
- [Code Quality Gates](#code-quality-gates)
- [Context and Memory](#context-and-memory)
- [Model Routing and Cost](#model-routing-and-cost)
- [Session Management](#session-management)
- [File Organization](#file-organization)
- [Notification and Alerts](#notification-and-alerts)
- [Voice and Sound](#voice-and-sound)
- [Git Integration](#git-integration)
- [Hook SDKs and Frameworks](#hook-sdks-and-frameworks)
- [Hook Collections](#hook-collections)
- [Creative and Utility](#creative-and-utility)
- [Learning Resources](#learning-resources)

---

## Security and Prompt Injection

Hooks that detect and block prompt injection attacks in tool outputs.

- [Lasso Claude-Hooks](https://github.com/lasso-security/claude-hooks) - Scans tool outputs for 50+ prompt injection patterns including instruction overrides, role-playing jailbreaks, encoded payloads, and data exfiltration commands. Injects warnings into Claude's context. Triggers on: `PostToolUse`.
- [dwarvesf/claude-guardrails](https://github.com/dwarvesf/claude-guardrails) - Hardened security config with deny rules, destructive command blocking, pipe-to-shell blocking, data exfiltration prevention, and prompt injection scanning. Lite (3 hooks) and Full (5 hooks + scanner) modes. Install via `npx claude-guardrails install`. Triggers on: `PreToolUse`, `PostToolUse`.
- [CloneGuard](https://github.com/prodnull/cloneguard) - 4-layer defense: pre-execution repo scan, InstructionsLoaded hook, PostToolUse output scanning, PreToolUse write/build gating. Uses ONNX embedding classifier (non-promptable) instead of LLM for detection. Works with Claude Code, Gemini CLI, Cursor. Triggers on: `PreToolUse`, `PostToolUse`, `InstructionsLoaded`.
- [claude-injection-guard](https://github.com/michaelhannecke/claude-injection-guard) - Two-stage prompt injection guard: Stage 1 is regex (zero deps, sub-ms), Stage 2 escalates to local LLM (Ollama/LM Studio). Zero data leaves your machine. Triggers on: `PostToolUse` (WebFetch).
- [rulebricks/claude-code-guardrails](https://github.com/rulebricks/claude-code-guardrails) - Real-time guardrails for Claude Code tool calls. 61 stars. Triggers on: `PreToolUse`, `PostToolUse`.

## Safety and Protection

Hooks that prevent Claude Code from making unwanted changes.

- [wangbooth/Claude-Code-Guardrails](https://github.com/wangbooth/Claude-Code-Guardrails) - Protective hooks that prevent accidental code loss through branch protection, automatic checkpointing, and safe commit squashing. 51 stars. Triggers on: `PreToolUse`, `PostToolUse`.
- [gstack freeze/guard](https://github.com/garrytan/gstack) - Lock critical files from modification. Uses `PreToolUse` hook definitions in SKILL.md frontmatter (not hooks.json) with real shell scripts (`freeze/bin/check-freeze.sh`). Note: only enforced in Claude Code — generated Codex skill docs are advisory prose only. Found in `freeze/SKILL.md.tmpl` and `guard/SKILL.md.tmpl`. Triggers on: `PreToolUse` (Write/Edit).
- [Everything Claude Code hook profiles](https://github.com/nicholasareed/everything-claude-code) - Three preset safety levels: minimal (fast, fewer checks), standard (balanced), strict (maximum safety, slower). Switch profiles per session. Found in `hooks/hooks.json`. Triggers on: `PreToolUse`, `PostToolUse`.
- [Pre-commit hook guard](https://github.com/anthropics/claude-code/tree/main/hooks) - Official example: block commits that skip pre-commit hooks (prevents `--no-verify`). Triggers on: `PreToolUse` (Bash).

## Monitoring and Observability

Hooks that track and visualize Claude Code activity in real-time.

- [Multi-Agent Observability Dashboard](https://github.com/disler/claude-code-hooks-multi-agent-observability) - Real-time monitoring dashboard for Claude Code agents through hook event tracking. Streams tool usage events to a web UI. 1,289 stars. Triggers on: all hook events.
- [MadameClaude](https://github.com/williamkapke/MadameClaude) - Monitoring system that captures and streams tool usage events to a web interface in real-time. 21 stars. Triggers on: `PreToolUse`, `PostToolUse`.
- [ccproxy](https://github.com/starbaser/ccproxy) - Proxy that hooks into Claude Code requests for intelligent model routing, request/response modification, and LangFuse tracking. 189 stars. Triggers on: request-level proxy hooks.

## Code Quality Gates

Hooks that enforce code quality standards automatically.

- [Auto-lint on save](https://github.com/nicholasareed/everything-claude-code) - Run linter after every file write. Reject changes that introduce lint errors. Found in `hooks/hooks.json`. Triggers on: `PostToolUse` (Write/Edit).
- [Claude Organize](https://github.com/ramakay/claude-organizer) - AI-powered file organization hook that automatically sorts temporary scripts from permanent docs. Understands content, not just patterns. 61 stars. Triggers on: `PostToolUse` (Write/Edit).

## Context and Memory

Hooks that manage what Claude knows across sessions and compactions.

- [post_compact_reminder](https://github.com/Dicklesworthstone/post_compact_reminder) - Detects context compaction and injects a reminder to re-read AGENTS.md, preventing post-compaction rule amnesia in long sessions. 34 stars. Triggers on: `PostCompact`.
- [Continuous Claude v3](https://github.com/parcadei/Continuous-Claude-v3) - Context management via hooks that maintain state through ledgers and handoffs. MCP execution without context pollution. Agent orchestration with isolated context windows. 3,619 stars. Triggers on: multiple lifecycle hooks.
- [Memory injection hook](https://github.com/nicholasareed/everything-claude-code) - Inject alerts, briefings, and relevant memories before each message. Scans memory files and surfaces the most relevant context. Found in `hooks/hooks.json`. Triggers on: pre-message.
- [Founder OS institutional memory](https://github.com/danielraffel/founder-os) - Accumulates learnings from task completions into `.claude/learnings/`. Future sessions automatically reference past lessons. Triggers on: task completion.

## Model Routing and Cost

Hooks that optimize model selection and track spending.

- [claude-model-router-hook](https://github.com/tzachbon/claude-model-router-hook) - Auto-switches model tier based on task complexity (e.g., Haiku for simple reads, Opus for complex reasoning). 25 stars. Triggers on: `PreToolUse`.
- [Cost tracker hook](https://github.com/karanb192/claude-code-hooks) - Tracks token usage and estimated cost per session. Part of a 10-hook collection. Triggers on: `PostToolUse`.

## Session Management

Hooks that manage Claude Code session state.

- [Everything Claude Code session persistence](https://github.com/nicholasareed/everything-claude-code) - Save and restore session context across restarts. Auto-dumps important state on session end, reloads on next start. Triggers on: `Stop`, session start.
- [Superpowers session-start](https://github.com/jasonm/superpowers) - Auto-load project context and active tasks when starting a new session. Found in `hooks/hooks.json`. Triggers on: session start.

## File Organization

Hooks that keep your project directory clean.

- [Claude Organize](https://github.com/ramakay/claude-organizer) - Automatically moves files Claude creates in the wrong place. Scripts go to `scripts/`, docs go to `docs/`, test results go to `docs/testing/`. 10 script subcategories. 61 stars. Triggers on: `PostToolUse` (Write).

## Notification and Alerts

Hooks that notify you about Claude Code activity.

- [claude-code-toast](https://github.com/eyalzh/claude-code-toast) - macOS toast notification when Claude Code is waiting for user response. 16 stars. Triggers on: `Notification`.
- [aily](https://github.com/jiunbae/aily) - Discord notifications with per-tmux-session threads. Each Claude session gets its own Discord thread. 6 stars. Triggers on: `Notification`, `Stop`.
- [Desktop notification on complete](https://github.com/anthropics/claude-code/tree/main/hooks) - Official example: send system notification when a long-running task completes. Triggers on: `Stop`.
- [Solopreneur decision logger](https://github.com/codeislaw1993/solopreneur-plugin) - Auto-logs every user decision with reasoning when Claude asks a question. Creates an observer protocol for future reference. Triggers on: `PostToolUse` (AskUserQuestion).

## Voice and Sound

Hooks that add audio feedback to Claude Code events.

- [Voice output hooks](https://github.com/shanraisshan/claude-code-hooks) - Adds text-to-speech voice output to Claude Code responses and notifications. 187 stars. Triggers on: `Notification`, `Stop`.
- [SCV Sounds](https://github.com/htjun/claude-code-hooks-scv-sounds) - StarCraft SCV sound effects for hook events (tool use, completion, errors). 38 stars. Triggers on: `PreToolUse`, `PostToolUse`, `Stop`, `Notification`.

## Git Integration

Hooks that connect Claude Code actions to git operations.

- [GitButler Claude Code hooks](https://docs.gitbutler.com/features/ai-integration/claude-code-hooks) - Official GitButler integration: PreToolUse creates session-specific git index, PostToolUse stages files, Stop commits to per-session branch under `refs/heads/claude/`. Enables parallel sessions with isolated branches. By Scott Chacon. Triggers on: `PreToolUse`, `PostToolUse`, `Stop`.
- [Auto-checkpoint on skill completion](https://github.com/codeislaw1993/solopreneur-plugin) - Automatically creates a git commit after every skill finishes running. Ensures you can always roll back. Triggers on: skill completion.
- [Branch-per-task pattern](https://github.com/danielraffel/founder-os) - Auto-create a new branch when starting a task from the queue. Isolates work for clean PR creation. Triggers on: task start.

## Hook SDKs and Frameworks

Tools for building and managing hooks in different languages.

- [cchooks (Python)](https://github.com/GowayLee/cchooks) - Python SDK for building Claude Code hooks. Abstracts stdin/stdout JSON handling, exit codes, and event matching. 123 stars.
- [cc-hooks-ts (TypeScript)](https://github.com/sushichan044/cc-hooks-ts) - TypeScript SDK with full type safety for defining hooks. 35 stars.
- [claude-hooks-sdk (PHP)](https://github.com/beyondcode/claude-hooks-sdk) - PHP SDK for building Claude Code hooks. 62 stars.
- [claude_hooks (Ruby)](https://github.com/gabriel-dehan/claude_hooks) - Ruby DSL for creating Claude Code hooks. 36 stars.
- [claude-hooks CLI manager](https://github.com/webdevtodayjason/claude-hooks) - CLI manager for hooks — add, remove, list, toggle hooks without editing JSON. 73 stars.
- [Hookify plugin](https://paddo.dev/blog/claude-code-hooks-guardrails/) - Zero-JSON hook creation via natural language. `/hookify Block rm -rf commands` creates the hook without editing settings.json.

## Hook Collections

Repos that bundle multiple hooks together.

- [karanb192/claude-code-hooks](https://github.com/karanb192/claude-code-hooks) - 10-hook collection: cost-tracker, rate-limiter, branch-guard, protect-tests, context-snapshot, ntfy-notify, discord-notify, tts-alerts, rules-injector, session-summary. Copy-paste ready. 298 stars.

## Creative and Utility

Unique and experimental hooks.

- [cc-dice](https://github.com/pro-vi/cc-dice) - Probabilistic dice triggers — adds randomness to hook execution (e.g., only run expensive checks 20% of the time). Wraps any hook event. 21 stars.

## Learning Resources

Guides and tutorials for writing hooks.

- [Claude Code Hooks Mastery](https://github.com/disler/claude-code-hooks-mastery) - Complete reference implementation of all 13 hook lifecycle events with JSON payloads captured. Includes TTS, Ruff linting, transcript extraction, sub-agent hooks, and team-based validation. 3,379 stars.
- [95-hook production infrastructure](https://blakecrosley.com/blog/claude-code-hooks) - Blog documenting 95 production hooks across 4 layers: Prevention (PreToolUse), Context (UserPromptSubmit), Validation (PostToolUse), Quality (Stop). Includes recursion-guard, circuit-breaker, and pride-check.
- [Claude Code official hooks docs](https://docs.anthropic.com/en/docs/claude-code/hooks) - Official documentation covering all hook events, configuration, and best practices.
- [gstack hooks patterns](https://github.com/garrytan/gstack) - Production hooks for file protection (freeze/guard) used by a YC partner.

---

## Related Awesome Lists

- [awesome-claude-code-workflows](https://github.com/ithiria894/awesome-claude-code-workflows) - Workflow recipes that combine hooks with skills, MCP servers, and agents.
- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) - Comprehensive catalog of Claude Code tools, skills, hooks, agents, and plugins.
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) - The definitive list of MCP servers.
- [awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) - Claude Code skills collection.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines. We curate, not collect — not every submission will be accepted.
