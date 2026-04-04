# ai-dev-tools

This repository is a home for rules, prompts, workflows, and supporting files used to develop software with multiple AI toolsets.

The goal is to keep those materials organized in one place, separate shared repository governance from reusable downstream artifacts, and make it easier to refine each agent's guidance over time.

## What This Repository Contains

The repository is organized by AI toolset:

- `codex/` contains Codex-specific guidance and workflow artifacts intended for reuse in other projects.
- `claude/` is reserved for Claude-specific guidance and is currently a placeholder for future content.
- `junie/` contains Junie-specific guidance and workflow artifacts intended for reuse in other projects.

At the root, the repository also contains a small set of files used to manage this repository itself:

- `AGENTS.md`
- `CLAUDE.md`
- `.junie/guidelines.md`
- `SHARED_GUIDELINES.md`

Those root files are for maintaining this repository and keeping the root-level instructions aligned across agents.

## Current Status

The repository is in an early organization phase.

Current downstream content includes:

- a more developed Codex ruleset under `codex/`
- an existing Junie ruleset under `junie/`
- a Claude area that has been created but not populated yet

There is also an `ai-work/` folder containing planning artifacts related to improving and restructuring the rule system.

## Why The Structure Matters

This project separates two different concerns:

- repository-level governance for maintaining this meta-project
- reusable agent-specific guidance that may later be copied into real development repositories

Keeping those layers separate reduces confusion, makes the guidance easier to maintain, and helps prevent repository-maintenance rules from leaking into downstream project templates.

## Intended Use

This repository is primarily an authoring and organization workspace.

It is meant to be the place where agent-specific development guidance is drafted, reviewed, compared, and improved before being reused elsewhere.
