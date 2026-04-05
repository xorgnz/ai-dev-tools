# ai-dev-tools

This repository is a home for rules, prompts, workflows, and supporting files used to develop software with multiple AI toolsets.

The goal is to keep those materials organized in one place, separate shared repository governance from reusable downstream artifacts, and make it easier to refine each agent's guidance over time.

In this repository:

- "root rules" means the rules intended to be applied in this project itself
- "downstream rules" means the rules authored here for use in other projects
- the downstream rules are the files stored under `downstream/`

## What This Repository Contains

Human-facing files at the root:

- `README.md`
- `TODO.md`

Agent-facing instructions for working in this repository:

- `AGENTS.md`
- `CLAUDE.md`
- `ai-rules/`

The root entrypoint files stay in place for agent discovery. Shared root guidance and `rule-#-name.md` root rule files live under `ai-rules/`. A Junie root entrypoint may also exist under `.junie/` when needed, but it is part of the same root-instruction layer.

Planning artifacts for agents working in this repository:

- `ai-work/`

Downstream artifacts intended for use in other projects:

- `downstream/ai-rules/` contains the shared downstream rules used by multiple agents.
- `downstream/guidelines/` contains the shared downstream guideline base plus agent-specific guideline overlays.
- downstream deployment files are not stored yet and can be assembled later from the shared rules and guideline sources.

## Current Status

The repository is in an early organization phase.

Current downstream content includes:

- a shared downstream ruleset under `downstream/ai-rules/`
- a shared downstream guideline base plus agent-specific overlays under `downstream/guidelines/`

There is also an `ai-work/` folder containing planning artifacts related to improving and restructuring the rule system.

## Why The Structure Matters

This project separates three different concerns:

- human-facing repository documentation
- root rules for maintaining this meta-project
- downstream rules and guidelines that may later be copied into real development repositories

Keeping those layers separate reduces confusion, makes the guidance easier to maintain, and helps prevent repository-maintenance rules from leaking into downstream project templates.

## Intended Use

This repository is primarily an authoring and organization workspace.

It is meant to be the place where shared downstream rules and agent-specific guidelines are drafted, reviewed, compared, and improved before being assembled and reused elsewhere.
