# Root Meta-Project Guidance

## Purpose

This file is the single shared source of truth for root-level instructions in this repository.

It governs how AI agents should work while maintaining this repository itself.

It does not define the reusable guidance stored under `downstream/` for downstream projects.

The specific root rules live alongside this file in `ai-rules/`.

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

## Root Rule Files

- `ai-rules/rule-1-plan-work.md` is the scaffold for planning new root-level work.
- `ai-rules/rule-2-do-work.md` is the scaffold for executing approved root-level work.
- `ai-rules/rule-3-commit.md` defines the root-only commit rule.

When working in this repository, apply this shared guidance together with the relevant root rule files.

## Downstream Layout

- `downstream/ai-rules/` contains the shared downstream rules.
- `downstream/guidelines/` contains the shared downstream guideline base and agent-specific guideline overlays.
- Deployment-specific downstream agent files can be assembled later from these shared sources when needed.

When editing files under `downstream/`, treat them as downstream rules and reusable artifacts rather than root operating instructions.

Agents working in this repository should not execute downstream rules as if this repository were a downstream project.

In this repository, downstream rules should only be consulted when the task is to review, edit, reorganize, or otherwise work on those downstream rules themselves.

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
