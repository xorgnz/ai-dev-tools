# Root Meta-Project Guidance

## Purpose

This file is the single shared source of truth for root-level instructions in this repository.

It governs how AI agents should work while maintaining this repository itself.

It does not define the reusable guidance stored under `downstream/` for downstream projects.

## Terminology

- "Root rules" means the rules intended to be applied in this project while working in this repository.
- "Downstream rules" means the rules authored in this project for use elsewhere.
- In this repository, downstream artifacts live under `downstream/`.
- The shared downstream rules live in `downstream/ai-rules/`.
- The shared downstream guideline base and agent-specific guideline overlays live in `downstream/guidelines/`.
- Deployment-specific downstream agent files are not stored as source artifacts unless explicitly added later.

## Repository Role

This repository has two distinct layers:

1. The meta-project layer at the root, where agents help author and maintain repository structure and shared guidance.
2. The reusable artifact layer inside `downstream/`, where shared downstream rules and agent-specific downstream guidelines are prepared for use in other projects.

Agents must preserve the distinction between those two layers, which is also the distinction between root rules and downstream rules.

## Root-Level Scope

Root-level governance files exist only to guide work performed in this repository.

They are not templates for downstream development projects unless a file explicitly says so.

If a rule is meant to be copied into other repositories, it is a downstream rule and belongs under `downstream/`, not in the root governance layer.

## Downstream Layout

- `downstream/ai-rules/` contains the shared downstream rules.
- `downstream/guidelines/` contains the shared downstream guideline base and agent-specific guideline overlays.
- Deployment-specific downstream agent files can be assembled later from these shared sources when needed.

When editing files under `downstream/`, treat them as downstream rules and reusable artifacts rather than root operating instructions.

Agents working in this repository should not execute downstream rules as if this repository were a downstream project.

In this repository, downstream rules should only be consulted when the task is to review, edit, reorganize, or otherwise work on those downstream rules themselves.

## Commit Rule For This Repository Only

This commit rule applies only to commits made while maintaining this repository.

It does not apply to guidance being developed inside `downstream/` unless that guidance explicitly defines a similar rule for downstream use.

When asked to commit changes in this repository:

1. Review the changes since the last commit.
2. Propose a commit message that starts with the prefix `ai`.
3. Wait for explicit user approval.
4. Create the commit only after approval is given.

Do not commit automatically without explicit user approval.

## Writing Guidance In This Repository

- Use clear language that another agent can follow without hidden context.
- State whether new guidance is a root rule or a downstream rule.
- Do not mix root rules into downstream rules by accident.
- Keep cross-agent root guidance aligned by editing this shared file instead of duplicating the same rule in multiple places.
- If an agent notices that a root agent-specific guidance file differs from this shared file in substance, it should alert the user immediately so the mismatch can be resolved.

## Default Decision Rule

If it is unclear where a rule belongs, resolve it by asking:

1. Is this for maintaining this repository? If yes, it is a root rule and belongs in the root governance layer.
2. Is this for governing agent behavior in downstream development projects? If yes, it is a downstream rule and belongs in the relevant agent-specific subfolder.
