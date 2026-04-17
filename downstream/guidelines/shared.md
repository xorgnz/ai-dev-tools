# Shared Downstream Guidelines

This file is the shared base for downstream agent guidelines.

At deployment time, combine this file with exactly one agent-specific file from `downstream/guidelines/` and exactly one environment-specific file from `downstream/environments/`.

When needed, you may also append one or more technology-specific overlays from `downstream/toolsets/`.

## Project Workflow

- Do not apply root repository rules (e.g., `ai-rules/rule-*`) in downstream projects; use only the downstream rules and overlays provided here.
<include src="../../shared-snippets/explicit-request-before-implementation.md" />
<include src="../../shared-snippets/clarification-line.md" />
- Work step-by-step and avoid combining unrelated changes in a single pass.
- Prefer repo-aware tools and minimal, traceable edits over broad rewrites.
- You may refer to repository files directly with `@` file references when the UI supports them.
- For rule-driven work, prefer short requests such as `Rule: @ai-rules/5-create-tasks.md` and `Feature: 01-some-feature`.
- If the user says `rule 1`, `rule 2`, `rule 3`, and so on, treat that as an instruction to run the corresponding downstream rule rather than merely describing it.
- Any time the user asks you to execute a rule, look through the relevant instructions in `ai-rules/` before proceeding.
- After recognizing a numbered rule invocation, parse the remaining tokens against that rule's documented arguments before applying generic feature, task, branch, or free-form inference.
- If a token matches both a reserved rule argument and a possible feature alias, branch name, task label, or free-form description, prefer the reserved rule argument unless the user explicitly identifies the other target, for example with `feature <tag>`.
- Shortcut workflow phrases documented in `ai-rules/` may also be used directly. For example, `Run the 6-7-8 subtask flow for task 3` refers to the workflow defined in `@ai-rules/00-subtask-flow-6-7-8.md`.
- Branch-sensitive rules should use `/ai-work/00-workflow-config.md` as the source of truth for whether branch-based feature workflow is `required` or `optional`.
- If a branch-sensitive rule needs that config and it is missing, ask the user which mode to use, write the answer to `/ai-work/00-workflow-config.md`, and then continue.
- In `branch_mode: optional`, branch operations are advisory unless the user explicitly asks for them or a specific rule says otherwise.

## Approval Style

<include src="../../shared-snippets/approval-style-question.md" />

## Scope Discipline

<include src="../../shared-snippets/scope-discipline.md" />

## Tone

<include src="../../shared-snippets/tone-baseline.md" />

## Environment-Agnostic Defaults

<include src="../../shared-snippets/environment-agnostic-defaults.md" />

## Execution Constraints

<include src="../../shared-snippets/execution-constraints.md" />

## Editing Expectations

<include src="../../shared-snippets/editing-expectations.md" />
