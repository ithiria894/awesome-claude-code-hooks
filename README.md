# Awesome Claude Code Hooks [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Curated collection of Claude Code hooks — event-driven automations that trigger before or after Claude Code actions.

Hooks are shell commands that run automatically when Claude Code performs specific actions. They're defined in `settings.json` and trigger on events like `PreToolUse`, `PostToolUse`, `Notification`, and `Stop`.

Looking for complete workflow recipes? See [awesome-claude-code-workflows](https://github.com/ithiria894/awesome-claude-code-workflows). Looking for tools and skills? See [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code).

## Contents

- [Safety and Protection](#safety-and-protection)
- [Code Quality Gates](#code-quality-gates)
- [Session Management](#session-management)
- [File Organization](#file-organization)
- [Notification and Monitoring](#notification-and-monitoring)
- [Context and Memory](#context-and-memory)
- [Git Integration](#git-integration)
- [Security](#security)
- [Hook Frameworks](#hook-frameworks)
- [Learning Resources](#learning-resources)

---

## Safety and Protection

Hooks that prevent Claude Code from making unwanted changes.

- [gstack freeze/guard](https://github.com/garrytan/gstack) - Lock critical files from modification. `/freeze` marks files, hook blocks any write attempts during session. Triggers on: `PreToolUse` (Write/Edit).
- [Everything Claude Code hook profiles](https://github.com/nicholasareed/everything-claude-code) - Three preset safety levels: minimal (fast, fewer checks), standard (balanced), strict (maximum safety, slower). Switch profiles per session. Found in `hooks/hooks.json`.
- [Pre-commit hook guard](https://github.com/anthropics/claude-code/tree/main/hooks) - Official example: block commits that skip pre-commit hooks (prevents `--no-verify`). Triggers on: `PreToolUse` (Bash).

## Code Quality Gates

Hooks that enforce code quality standards automatically.

- [Auto-lint on save](https://github.com/nicholasareed/everything-claude-code) - Run linter after every file write. Reject changes that introduce lint errors. Triggers on: `PostToolUse` (Write/Edit).
- [Type-check guardian](https://github.com/nicholasareed/everything-claude-code) - Run TypeScript compiler after code changes, block if type errors introduced. Triggers on: `PostToolUse` (Write/Edit).
- [Claude Organize](https://github.com/ramakay/claude-organizer) - AI-powered file organization hook that automatically sorts temporary scripts from permanent docs. Understands content, not just patterns. 61 stars. Triggers on: `PostToolUse` (Write/Edit).

## Session Management

Hooks that manage Claude Code session state.

- [Everything Claude Code session persistence](https://github.com/nicholasareed/everything-claude-code) - Save and restore session context across restarts. Auto-dumps important state on session end, reloads on next start. Triggers on: `Stop` and session start.
- [Superpowers session-start](https://github.com/jasonm/superpowers) - Auto-load project context and active tasks when starting a new session. Found in `hooks/hooks.json`. Triggers on: session start.

## File Organization

Hooks that keep your project directory clean.

- [Claude Organize](https://github.com/ramakay/claude-organizer) - Automatically moves files Claude creates in the wrong place. Scripts go to `scripts/`, docs go to `docs/`, test results go to `docs/testing/`. 10 script subcategories. 61 stars. Triggers on: `PostToolUse` (Write).
- [Auto-cleanup temp files](https://github.com/nicholasareed/everything-claude-code) - Remove temporary test files and debug scripts after session ends. Triggers on: `Stop`.

## Notification and Monitoring

Hooks that notify you about Claude Code activity.

- [Desktop notification on complete](https://github.com/anthropics/claude-code/tree/main/hooks) - Official example: send system notification when a long-running task completes. Triggers on: `Stop`.
- [Solopreneur decision logger](https://github.com/codeislaw1993/solopreneur-plugin) - Auto-logs every user decision with reasoning when Claude asks a question. Creates an "observer protocol" for future reference. Triggers on: `PostToolUse` (AskUserQuestion).

## Context and Memory

Hooks that manage what Claude knows across sessions.

- [Memory injection hook](https://github.com/nicholasareed/everything-claude-code) - Inject alerts, briefings, and relevant memories before each message. Scans memory files and surfaces the most relevant context. Triggers on: pre-message.
- [Founder OS institutional memory](https://github.com/danielraffel/founder-os) - Accumulates learnings from task completions into `.claude/learnings/`. Future sessions automatically reference past lessons. Triggers on: task completion.

## Git Integration

Hooks that connect Claude Code actions to git operations.

- [Auto-checkpoint on skill completion](https://github.com/codeislaw1993/solopreneur-plugin) - Automatically creates a git commit after every skill finishes running. Ensures you can always roll back. Triggers on: skill completion.
- [Branch-per-task pattern](https://github.com/danielraffel/founder-os) - Auto-create a new branch when starting a task from the queue. Isolates work for clean PR creation. Triggers on: task start.

## Security

Hooks that enforce security policies.

- [Secret scanner](https://github.com/nicholasareed/everything-claude-code) - Scan for API keys, passwords, and secrets before any commit. Block if secrets detected. AgentShield integration. Triggers on: `PreToolUse` (Bash with git commit).
- [Command allowlist](https://github.com/anthropics/claude-code/tree/main/hooks) - Official example: only allow specific bash commands, block everything else. Triggers on: `PreToolUse` (Bash).

## Hook Frameworks

Tools for building and managing hooks.

- [Everything Claude Code hook system](https://github.com/nicholasareed/everything-claude-code) - Complete hook management system with profiles, pre/post-tool hooks, and session lifecycle hooks. The most comprehensive reference implementation.
- [Claude Code official hooks docs](https://docs.anthropic.com/en/docs/claude-code/hooks) - Official documentation for the hooks system. Event types, configuration format, and examples.

## Learning Resources

Guides and tutorials for writing hooks.

- [Claude Code Hooks Guide](https://docs.anthropic.com/en/docs/claude-code/hooks) - Official documentation covering all hook events, configuration, and best practices.
- [Everything Claude Code hooks examples](https://github.com/nicholasareed/everything-claude-code/tree/main/hooks) - Real-world hooks configuration with three safety profiles.
- [gstack hooks patterns](https://github.com/garrytan/gstack) - Production hooks for file protection (freeze/guard) used by a YC partner.

---

## Related Awesome Lists

- [awesome-claude-code-workflows](https://github.com/ithiria894/awesome-claude-code-workflows) - Workflow recipes that combine hooks with skills, MCP servers, and agents.
- [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) - Comprehensive catalog of Claude Code tools, skills, hooks, agents, and plugins.
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) - The definitive list of MCP servers.
- [awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) - Claude Code skills collection.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.
