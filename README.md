# AGENTS.md

A single set of rules for AI coding agents (Claude Code, Codex, and others), so they behave the same way in every project.

## What's inside

- `AGENTS.md`: the rules, read by most coding agents.
- `CLAUDE.md`: the same rules, read by Claude Code.

## What the rules cover

- **Think first:** state assumptions, ask when unclear, prefer the simpler approach.
- **Small changes:** touch only what the task needs, match existing style.
- **Safe Git:** read-only commands and `fetch`/`pull` are free; anything else needs explicit permission.
- **Verification:** run the project's own checks and never claim a check passed unless it did.
- **Safety:** no secrets in code, no malicious tooling.
- **Communication:** short, direct, with changed files and verification listed at the end.

## Usage

Copy `CLAUDE.md` to `~/.claude/CLAUDE.md` for all projects, or place `AGENTS.md` / `CLAUDE.md` in a repository root for that project only. Project-level files take precedence over the global one.
