# Contributing

Thanks for wanting to contribute! This list curates **Claude Code hooks** — event-driven automations that trigger on specific Claude Code actions.

## What belongs here

A hook is a shell command or script that runs automatically when Claude Code performs an action (PreToolUse, PostToolUse, Notification, Stop, etc.).

Each entry should include:
- What the hook does
- Which event it triggers on
- A link to the source (GitHub repo, blog post, or gist)

## How to submit

1. Fork this repo
2. Add your hook to the appropriate section in README.md
3. Follow the format: `- [Name](url) - Description of what the hook does. Triggers on: `Event`.`
4. One hook per PR
5. Submit a PR

## Quality standards

- The hook must be something you have **actually used**
- It must work with current Claude Code (2025+)
- Description must start with capital letter and end with period

## Format

```
- [Hook Name](https://github.com/user/repo) - What it does. Triggers on: `PostToolUse`.
```
