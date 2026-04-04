# AI Dev Tools Repository Guidance

## Purpose

This repository centralizes the rules, conventions, and working strategies used across multiple AI-assisted development toolsets.

It serves two distinct roles:

1. It is a meta-project where AI agents help author, refine, and organize guidance files.
2. It is a source repository for agent-specific guidance that may later be copied into other software projects.

Agents working in this repository must preserve that distinction.

## Repository Structure Intent

The repository is organized around three AI toolsets:

- `codex/`
- `claude/`
- `junie/`

Each of those subfolders is intended to contain the guidance, rules, templates, and related files that belong to that specific agent ecosystem and are meant to be reused in downstream development projects.

In addition to those agent-specific folders, this repository also contains root-level governance files for work performed inside this repository itself. Those root-level files are not the same thing as the files stored in the agent-specific subfolders.

## Root-Level Governance Files

The root of this repository is reserved for meta-project instructions that govern how agents should work while editing and maintaining this repository.

These root-level files include:

- `AGENTS.md` for Codex-oriented guidance in this repository
- `CLAUDE.md` for Claude-oriented guidance in this repository
- `.junie/guidelines.md` for Junie-oriented guidance in this repository

These files exist so that each agent can be guided appropriately while helping build or maintain the repository itself.

They should be written for use in this meta-project, not as generic downstream project instructions unless explicitly intended.

## Root-Only Commit Rule

This rule applies only to commits made in this repository while maintaining the meta-project.

It does not define or imply any commit policy for files stored in `codex/`, `claude/`, or `junie/` as reusable downstream guidance. If similar commit guidance is needed for downstream projects, it should be defined separately in the appropriate agent-specific location.

When asked to commit changes in this repository:

1. Review the changes since the last commit.
2. Propose a commit message that starts with the prefix `ai`.
3. Wait for user approval.
4. Create the commit only after approval is given.

Do not commit automatically without explicit approval from the user.

## Agent-Specific Subfolders

The agent-specific subfolders are the place for files that will be copied or adapted into other projects.

Examples:

- `codex/` should contain Codex-facing rules intended for use in real development repositories
- `claude/` should contain Claude-facing rules intended for use in real development repositories
- `junie/` should contain Junie-facing rules intended for use in real development repositories

When editing files in those folders, assume they are productized guidance artifacts for future reuse, not instructions for operating inside this meta-repository unless a file explicitly says otherwise.

## Working Rules For Agents In This Repository

- Preserve the distinction between root-level meta-project governance and reusable downstream guidance stored in subfolders.
- Prefer clear, explicit language that another agent can interpret without relying on unstated context.
- When adding new guidance, state whether it is meant for this repository or for downstream projects.
- Do not casually merge meta-project instructions into reusable copied templates.
- If a rule applies only to one agent, keep it in that agent's root-level governance file or agent-specific folder as appropriate.
- If a convention applies across the repository, document it in the appropriate root-level file and keep wording consistent across agent ecosystems where practical.

## Authoring Intent

This repository is being built incrementally. The first phase is to establish the meta-governance files that let each agent help define its own downstream guidance safely and consistently.

Because multiple AI systems may read these files later, instructions should be:

- unambiguous
- scoped to the correct layer of the repository
- easy to maintain over time
- explicit about whether they govern this repository or copied artifacts

## Default Interpretation

Unless a file clearly states otherwise:

- root-level governance files apply to work performed in this repository
- files inside `codex/`, `claude/`, and `junie/` are intended as reusable agent-specific guidance for other projects

If there is ambiguity about where a rule belongs, agents should resolve it by asking whether the rule is for:

1. maintaining this repository, or
2. governing AI behavior in downstream development projects
