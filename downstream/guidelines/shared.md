# Header

This file is the shared base used to build downstream guidelines.

Any agent working in this repository may read or edit it.

This `Header` section is source-only metadata and must not be copied into downstream export files.

# Content

## Project Workflow

<include src="../../shared-snippets/explicit-instruction-required.md" />
<include src="../../shared-snippets/clarification-line.md" />
- Work step-by-step and avoid combining unrelated changes in a single pass.
- Prefer repo-aware tools and minimal, traceable edits over broad rewrites.
- You may refer to repository files directly with `@` file references when the UI supports them.
- For rule-driven work, prefer short requests such as `Rule: @ai-rules/05-create-tasks.md` and `Feature: 01-some-feature`.
- If the user says `rule 1`, `rule 2`, `rule 3`, and so on, treat that as an instruction to run the corresponding rule rather than merely describing it.
- Any time the user asks you to execute a rule, look through the relevant instructions in `ai-rules/` before proceeding.
- After recognizing a numbered rule invocation, parse the remaining tokens against that rule's documented arguments before applying generic feature, task, or free-form inference.
- If a token matches both a reserved rule argument and a possible feature alias, task label, or free-form description, prefer the reserved rule argument unless the user explicitly identifies the other target, for example with `feature <tag>`.
- Shortcut workflow phrases documented in `ai-rules/` may also be used directly. For example, `Run the 6-7-8 subtask flow for task 3` refers to the workflow defined in `@ai-rules/00-subtask-flow-6-7-8.md`.

## Approval Style

<include src="../../shared-snippets/approval-style-question.md" />
<include src="../../shared-snippets/approval-policy.md" />

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
