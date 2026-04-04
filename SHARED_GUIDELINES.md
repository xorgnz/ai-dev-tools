# Root Meta-Project Guidance

## Purpose

This file is the single shared source of truth for root-level instructions in this repository.

It governs how AI agents should work while maintaining this repository itself.

It does not define the reusable guidance stored in `codex/`, `claude/`, or `junie/` for downstream projects.

## Repository Role

This repository has two distinct layers:

1. The meta-project layer at the root, where agents help author and maintain repository structure and shared guidance.
2. The reusable artifact layer inside `codex/`, `claude/`, and `junie/`, where agent-specific rules are prepared for use in other projects.

Agents must preserve the distinction between those two layers.

## Root-Level Scope

Root-level governance files exist only to guide work performed in this repository.

They are not templates for downstream development projects unless a file explicitly says so.

If a rule is meant to be copied into other repositories, it belongs in the appropriate agent-specific subfolder, not in the root governance layer.

## Agent-Specific Subfolders

- `codex/` contains reusable Codex-oriented guidance for downstream projects.
- `claude/` contains reusable Claude-oriented guidance for downstream projects.
- `junie/` contains reusable Junie-oriented guidance for downstream projects.

When editing files in those folders, treat them as reusable artifacts rather than root operating instructions.

## Commit Rule For This Repository Only

This commit rule applies only to commits made while maintaining this repository.

It does not apply to guidance being developed inside `codex/`, `claude/`, or `junie/` unless that guidance explicitly defines a similar rule for downstream use.

When asked to commit changes in this repository:

1. Review the changes since the last commit.
2. Propose a commit message that starts with the prefix `ai`.
3. Wait for explicit user approval.
4. Create the commit only after approval is given.

Do not commit automatically without explicit user approval.

## Writing Guidance In This Repository

- Use clear language that another agent can follow without hidden context.
- State whether new guidance is for this repository or for downstream projects.
- Do not mix root meta-project rules into reusable downstream templates by accident.
- Keep cross-agent root guidance aligned by editing this shared file instead of duplicating the same rule in multiple places.
- If an agent notices that a root agent-specific guidance file differs from this shared file in substance, it should alert the user immediately so the mismatch can be resolved.

## Default Decision Rule

If it is unclear where a rule belongs, resolve it by asking:

1. Is this for maintaining this repository? If yes, it belongs in the root governance layer.
2. Is this for governing agent behavior in downstream development projects? If yes, it belongs in the relevant agent-specific subfolder.
