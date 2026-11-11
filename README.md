# Awesome Claude Code Hooks [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of hooks, guides, tools, and examples for [Claude Code](https://docs.claude.com/en/docs/claude-code) hooks — the shell-command lifecycle events that let you intercept, block, log, or augment what your coding agent does.

Claude Code hooks fire on events like `PreToolUse`, `PostToolUse`, `SessionStart`, `SessionEnd`, `Notification`, `Stop`, and `UserPromptSubmit`, running arbitrary shell commands with structured JSON in/out. This list collects the best real-world implementations, so you don't have to write your security guardrail or notification hook from scratch.

Contributions welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

## Contents

- [Official Docs](#official-docs)
- [Getting Started / Guides](#getting-started--guides)
- [Security & Guardrail Hooks](#security--guardrail-hooks)
- [Notification Hooks](#notification-hooks)
- [Observability & Logging Hooks](#observability--logging-hooks)
- [Git & Commit Hooks](#git--commit-hooks)
- [Formatting / Linting / Testing Gates](#formatting--linting--testing-gates)
- [Voice / TTS Hooks](#voice--tts-hooks)
- [Session Memory & Context Hooks](#session-memory--context-hooks)
- [Frameworks & Toolkits (bundle many hooks)](#frameworks--toolkits-bundle-many-hooks)
- [Multi-Agent / Cross-Tool Hooks](#multi-agent--cross-tool-hooks)

## Official Docs

- [Claude Code Hooks Reference](https://docs.claude.com/en/docs/claude-code/hooks) — official event list, JSON schema, exit code semantics.
- [Claude Code Hooks Guide](https://docs.claude.com/en/docs/claude-code/hooks-guide) — official walkthrough with examples.

## Getting Started / Guides

- [ChrisWiles/claude-code-showcase](https://github.com/ChrisWiles/claude-code-showcase) — full project config example wiring hooks, skills, agents, and commands together.
- [diet103/claude-code-infrastructure-showcase](https://github.com/diet103/claude-code-infrastructure-showcase) — skill auto-activation + hooks + agents infrastructure example.
- [disler/claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery) — the most complete hands-on reference for every hook event, with working examples for each.
- [FlorianBruniaux/claude-code-ultimate-guide](https://github.com/FlorianBruniaux/claude-code-ultimate-guide) — 430K+ line guide covering hooks alongside skills, agents, and MCP.
- [wesammustafa/Claude-Code-Everything-You-Need-to-Know](https://github.com/wesammustafa/Claude-Code-Everything-You-Need-to-Know) — a practical guide that covers hooks alongside skills, agents, and MCP servers with copy-paste examples.

## Security & Guardrail Hooks

Hooks that block destructive commands, exfiltration attempts, or unsafe file access before they execute.

- [DataFog/datafog-python](https://github.com/DataFog/datafog-python) — `datafog-hook` gates tool calls (shell commands, web requests, file writes, MCP tools) and blocks PII from leaving the machine, entirely offline in ~70-90ms.
- [Dicklesworthstone/destructive_command_guard](https://github.com/Dicklesworthstone/destructive_command_guard) — Rust `PreToolUse` hook that blocks destructive git, filesystem, database, Kubernetes, cloud, and Terraform commands (including ones hidden in heredocs and inline scripts) via 50+ rule packs, with explain mode and a CI scan mode; installs into Claude Code, Codex, Gemini CLI, Copilot, Cursor, and more.
- [dwarvesf/claude-guardrails](https://github.com/dwarvesf/claude-guardrails) — hardened Claude Code security config with permission deny rules, shell hooks, and prompt-injection defense in full and lite variants.
- [hahahahahahahahah6/agent-guard](https://github.com/hahahahahahahahah6/agent-guard) — dependency-free guard stack that blocks the "green by editing the test" cheat (snapshots test/source hashes, blocks `Stop` until a changed test is proven to fail without the fix), plus an outbound-action denylist for pushes, publishes, deploys, and mass-send channels, with mutation-testing and comment-slop checks on top.
- [hahahahahahahahah6/edit-guard](https://github.com/hahahahahahahahah6/edit-guard) — stops one agent session from overwriting a file another session changed underneath it: watches Read/Edit/Write and blocks the stale write, telling the agent to re-read first; Python stdlib only.
- [hanlulong/overleaf-sync-now](https://github.com/hanlulong/overleaf-sync-now) — `PreToolUse` hook that pulls fresh Overleaf web edits before every `.tex`/`.bib` read or write, stopping the agent from silently overwriting them with a stale local Dropbox copy.
- [JeongJaeSoon/agent-guard](https://github.com/JeongJaeSoon/agent-guard) — `PreToolUse` guardrail that blocks an agent from reading `.env` files or writing secret-like values, using gitleaks for detection, with matching Git hook and CI backstops.
- [kaboumou/agent-run-guard](https://github.com/kaboumou/agent-run-guard) — dependency-free hook CLI for repeat-call and call-budget limits, with a documented Claude Code adapter (simulated hook tests; fails open on internal errors).
- [kenryu42/cc-safety-net](https://github.com/kenryu42/cc-safety-net) — `PreToolUse` guardrail hook blocking destructive git/filesystem commands and secret file access; also supports Codex, Cursor, Gemini CLI, and other agent runtimes.
- [kornysietsma/tool-gate-hook](https://github.com/kornysietsma/tool-gate-hook) — `PreToolUse` hook for Claude Code and GitHub Copilot CLI that auto-allows, auto-denies, or forces a prompt on tool calls via TOML rules, and logs every decision (payload, matched rules, outcome) to a JSONL audit trail. Rename/rework of the old `claude-code-permissions-hook`.
- [li-zhixin/claude-ignore](https://github.com/li-zhixin/claude-ignore) — `PreToolUse` hook that blocks Claude from reading files matching `.claudeignore` patterns, mirroring `.gitignore` semantics.
- [liberzon/claude-hooks](https://github.com/liberzon/claude-hooks) — `PreToolUse` hook that decomposes compound bash commands and checks each sub-command individually against allow/deny permission patterns.
- [MaxwellCalkin/sentinel-ai](https://github.com/MaxwellCalkin/sentinel-ai) — safety guardrails that use fast scanners to detect prompt injection, PII, and code vulnerabilities.
- [Pantheon-Security/medusa](https://github.com/Pantheon-Security/medusa) — scans `.claude/` hooks, permissions, and skills for compromise before you clone/run a repo; 40,000+ attack-signature patterns.
- [sangrokjung/claude-forge](https://github.com/sangrokjung/claude-forge) — 6-layer security hook stack bundled into a full Claude Code plugin framework.
- [tillmeier/claude-code-guardrails](https://github.com/tillmeier/claude-code-guardrails) — guardrail hooks derived from real incidents, paired with a plan→implement→verify→crosscheck loop, backed by 35 bats tests and measured hook overhead.
- [ulukaya/pawl](https://github.com/ulukaya/pawl) — deterministic `PreToolUse`/`Stop` gates for Claude Code, Codex and Antigravity that refuse home/root deletions (following scripts, Makefiles and `npm run`), ask before destructive git and credential reads, block token egress, and auto-approve provably read-only commands; stdlib Python, no network.
- [wangbooth/Claude-Code-Guardrails](https://github.com/wangbooth/Claude-Code-Guardrails) — protective hooks preventing accidental code loss via branch protection, automatic checkpointing, and safe commit squashing.
- [randommonicle/claude-skills](https://github.com/randommonicle/claude-skills) — a four-layer architecture of guardrail hooks and norms distilled from real shipped defects across four production codebases.
- [yurukusa/cc-safe-setup](https://github.com/yurukusa/cc-safe-setup) — interactive installer for `PreToolUse`/`PostToolUse`/`SessionStart`/`Stop`/`SubagentStop` hooks that block destructive commands (`rm -rf`, force-push, `git reset --hard`, secret writes) at the tool boundary, with plugin variants for git protection, credential guarding, and token budgets.

## Notification Hooks

Send a ping to Slack, Telegram, desktop notification center, etc. when Claude needs input or finishes a task.

- [disler/claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery) — includes `Notification` and `Stop` hook examples with TTS + desktop notification dispatch.
- [shanraisshan/claude-code-hooks](https://github.com/shanraisshan/claude-code-hooks) — adds a distinct voice announcement per hook event so you know what Claude is doing without watching the terminal.

## Observability & Logging Hooks

- [coleam00/claude-memory-compiler](https://github.com/coleam00/claude-memory-compiler) — hooks capture full sessions, an LLM compiler distills them into a structured, cross-referenced project knowledge base.
- [disler/claude-code-hooks-multi-agent-observability](https://github.com/disler/claude-code-hooks-multi-agent-observability) — real-time dashboard for monitoring multiple Claude Code agents via hook event tracking.
- [hansipie/ecotokens](https://github.com/hansipie/ecotokens) — `PreToolUse`/`PostToolUse` hooks filter and compress shell output, file reads, and grep results before they hit the model, with a TUI dashboard tracking token savings per project.

## Git & Commit Hooks

- [blader/taskmaster](https://github.com/blader/taskmaster) — `Stop` hook that keeps the agent working until all plan items and user requests are fully complete, rather than stopping early.
- [malaysherasia-ai/claude-never-again](https://github.com/malaysherasia-ai/claude-never-again) — turns each bug you fix into a `PreToolUse` hook on `git commit` that blocks the mistake (warn first, then deny after five correct fires), also run from git’s own pre-commit; the rest become one capped line in LESSONS.md.
- [parcadei/Continuous-Claude-v3](https://github.com/parcadei/Continuous-Claude-v3) — hooks maintain ledgers/handoffs for context continuity across sessions and commits.

## Formatting / Linting / Testing Gates

- [carlrannaberg/claudekit](https://github.com/carlrannaberg/claudekit) — toolkit of custom hooks/commands including lint/format/test gate hooks.
- [ckorhonen/jev-lint](https://github.com/ckorhonen/jev-lint) — fuzzy linting hook that checks Claude Code and Codex edits against team standards and test-hygiene rules, returning findings to the agent.
- [severity1/claude-code-prompt-improver](https://github.com/severity1/claude-code-prompt-improver) — `UserPromptSubmit` hook that rewrites loose prompts into precise ones before Claude sees them.

## Voice / TTS Hooks

- [disler/claude-code-hooks-mastery](https://github.com/disler/claude-code-hooks-mastery) — TTS-on-completion example.
- [shanraisshan/claude-code-hooks](https://github.com/shanraisshan/claude-code-hooks) — per-event voice announcements.

## Session Memory & Context Hooks

- [coleam00/claude-memory-compiler](https://github.com/coleam00/claude-memory-compiler) — auto-captures sessions and compiles a persistent, evolving knowledge base.
- [vshulcz/deja-vu](https://github.com/vshulcz/deja-vu) — single Go binary that indexes session history already on disk across Claude Code, Codex, Cursor, and 35+ other agents, surfacing matching past fixes via local search, MCP, and hooks with no LLM in the loop.
- [entireio/cli](https://github.com/entireio/cli) — installs `PreToolUse`/`PostToolUse` hooks that capture full agent sessions (prompts, files touched, tool calls) into a separate git branch, indexed and searchable alongside your commit history.
- [mksglu/context-mode](https://github.com/mksglu/context-mode) — hooks that compress tool output to save context window space and persist session memory.
- [parcadei/Continuous-Claude-v3](https://github.com/parcadei/Continuous-Claude-v3) — ledger/handoff hooks for context management across long sessions.
- [SethGammon/Citadel](https://github.com/SethGammon/Citadel) — persistent project memory, intent routing, safety hooks, and cost telemetry as one operating layer.
- [shimo4228/harness-scope](https://github.com/shimo4228/harness-scope) — a mod whose `prompt.context`, `prompt.attachment`, `agent.offer` and `tool.call` hooks hide global skills, agents, rules files and tools per repo through named profiles, so each repo's context carries only what it uses.

## Frameworks & Toolkits (bundle many hooks)

- [CloudAI-X/claude-workflow-v2](https://github.com/CloudAI-X/claude-workflow-v2) — plugin bundling 14 hooks (formatting, security, metrics, notifications) with 7 agents, 26 commands, and 14 skills in one marketplace install.
- [composio-community/awesome-claude-plugins](https://github.com/composio-community/awesome-claude-plugins) — curated Claude Code plugins that bundle hooks with commands/agents/MCP servers.
- [davepoon/buildwithclaude](https://github.com/davepoon/buildwithclaude) — hub for finding hooks alongside skills, agents, commands, and marketplace plugins.
- [fcakyon/claude-codex-settings](https://github.com/fcakyon/claude-codex-settings) — battle-tested hook configs across Claude Code, Codex, and Cursor.
- [ITW-Creative-Works/workkit](https://github.com/ITW-Creative-Works/workkit) — issue-pipeline plugin with 28 hooks in four groups (safety, docs, manager, workflow) that gate commits on Conventional Commits and test proof, guard vendor files, and keep GitHub issue labels in step with the work.
- [kyu1204/oh-my-harness](https://github.com/kyu1204/oh-my-harness) — generates a catalog of enforcement hooks (TDD guard, branch guard, command guard, commit-test gate, auto-lint, auto-PR) from a plain-English project description, with `omh sync --check` as a CI drift gate.
- [rohitg00/awesome-claude-code-toolkit](https://github.com/rohitg00/awesome-claude-code-toolkit) — 20+ hooks bundled with agents, skills, commands, and rules.
- [vibeeval/vibecosystem](https://github.com/vibeeval/vibecosystem) — 73 hooks as part of a larger self-learning multi-agent swarm setup.
- [yotamleo-org/Himmel](https://github.com/yotamleo-org/Himmel) — an orchestrated harness for running Claude Code that includes guardrail hooks, a Jira CLI, and a cross-session handover system.

## Multi-Agent / Cross-Tool Hooks

Hooks designed to work across Claude Code, Codex, Cursor, Gemini CLI, and other agent runtimes.

- [first-fluke/oh-my-agent](https://github.com/first-fluke/oh-my-agent) — stop-hook gates and independent judges verifying agent work by artifacts, across multiple agent runtimes.
- [JakeSelby/model-citizen](https://github.com/JakeSelby/model-citizen) — a control plane that projects your hooks, guardrails, and telemetry rules into Claude Code and Codex.
- [kenryu42/cc-safety-net](https://github.com/kenryu42/cc-safety-net) — cross-runtime guardrail hook (Claude Code, Codex, Cursor, Gemini CLI, Hermes Agent, and more).
- [Kruhlikau/subagent-tuner](https://github.com/Kruhlikau/subagent-tuner) — a `tool.call` hook on the Agent tool that sets the model and reasoning effort of each Claude Code subagent: asks first, recommends by task kind, or applies a saved default over what the agent requested.
- [publicmain/codex-delegation-guard](https://github.com/publicmain/codex-delegation-guard) — PreToolUse/SessionStart hooks that make Claude Code hand large code changes to Codex (or record why it keeps them), with local delegation stats.

## Contributing

New hooks, guides, and tools are added regularly — see [CONTRIBUTING.md](CONTRIBUTING.md) for the submission criteria. This list is updated frequently to track newly published hook implementations.

## License

[CC0](LICENSE) — public domain, per [awesome list convention](https://github.com/sindresorhus/awesome/blob/main/awesome.md).
