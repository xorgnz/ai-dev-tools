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
- `ai-rules/rule-4-export.md` defines the downstream export rule for generating agent-specific export bundles.

When working in this repository, apply this shared guidance together with the relevant root rule files.

If the user says `root rule 1`, `root rule 2`, `root rule 3`, or `root rule 4`, treat that as an instruction to run the corresponding root rule rather than merely describing it.

## Downstream Layout

- `downstream/ai-rules/` contains the shared downstream rules.
- `downstream/guidelines/` contains the shared downstream guideline base and agent-specific guideline overlays.
- `downstream/environments/` contains environment-specific downstream guideline overlays that must be included during export.
- `downstream/toolsets/` contains technology-specific downstream guideline overlays that can be included during export.
- `downstream/export/` is the generated export target for one agent-specific downstream bundle at a time.
- Deployment-specific downstream agent files can be assembled later from these shared sources when needed.

When editing files under `downstream/`, treat them as downstream rules and reusable artifacts rather than root operating instructions.

Agents working in this repository should not execute downstream rules as if this repository were a downstream project.

In this repository, downstream rules should only be consulted when the task is to review, edit, reorganize, or otherwise work on those downstream rules themselves.

Environment-specific and toolset-specific guidance should normally be authored in `downstream/environments/` or `downstream/toolsets/`, not embedded into root rules or downstream `ai-rules/`.

If an agent thinks environment-specific or toolset-specific behavior truly belongs in a rule rather than an overlay, it should ask the user before making that change.

## Root Work Tracking Layout

- `ai-work/active/` contains active root-level work plans.
- `ai-work/archive/` contains completed or superseded root-level work plans kept for historical reference.
- `ai-work/work-log.md` records planning and execution updates for root-level work in this repository.

The `ai-work/` planning layer is optional and should be used only when the user explicitly asks to plan work or when the user is already working from an approved active plan.

Small ad hoc root-level requests do not need a plan by default.

Each discrete root-level effort should be represented by one plan document in `ai-work/active/`.

Plan filenames should use the format `yyyy-mm-dd - NN - description - plan.md`, where `NN` is a two-digit sequence number for that date.

Use `01` for the first plan created on a given date and increment the sequence for each additional plan created on that same date.

When a root-level effort is completed or explicitly retired, move its plan document from `ai-work/active/` to `ai-work/archive/` and record that transition in `ai-work/work-log.md`.

## Writing Guidance In This Repository

- Use clear language that another agent can follow without hidden context.
- State whether new guidance is a root rule or a downstream rule.
- Do not mix root rules into downstream rules by accident.
- Do not put environment-specific or toolset-specific guidance into rules when an overlay is the better fit.
- Keep cross-agent root guidance aligned by editing this shared file instead of duplicating the same rule in multiple places.
- If an agent notices that a root agent-specific guidance file differs from this shared file in substance, it should alert the user immediately so the mismatch can be resolved.

## Tone

- Be clear, direct, and technically precise, but do not default to a cold or mechanical tone.
- Prefer a mildly warm, personable style that feels like collaborative human interaction rather than a changelog.
- Keep that tone lightweight. Do not add fluff, exaggerated enthusiasm, or unnecessary filler.

## Approval Style

When a root rule requires user approval, ask for it with a single yes/no question in this exact form:

`Approve this? Y/N.`

Present the proposed plan, task, or commit scope first, then ask that question unchanged.

## Default Decision Rule

If it is unclear where a rule belongs, resolve it by asking:

1. Is this for maintaining this repository? If yes, it is a root rule and belongs in the root governance layer.
2. Is this for governing agent behavior in downstream development projects? If yes, it is a downstream rule and belongs in the relevant agent-specific subfolder.

## Scope Discipline

- Do only what the user explicitly asks.
- Do not propose follow-on work, suggest next steps, or solicit further actions after completing a task.
- Stop after the requested task is complete and wait for the user's next instruction.
