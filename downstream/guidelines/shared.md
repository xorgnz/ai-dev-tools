# Shared Downstream Guidelines

This file is the shared base for downstream agent guidelines.

At deployment time, combine this file with exactly one agent-specific file from `downstream/guidelines/` and exactly one environment-specific file from `downstream/environments/`.

When needed, you may also append one or more technology-specific overlays from `downstream/toolsets/`.

## Project Workflow

- Do not begin implementation or multi-step work without an explicit user request.
- If the target feature or task is unclear, ask one concise clarification before proceeding.
- Work step-by-step and avoid combining unrelated changes in a single pass.
- Prefer repo-aware tools and minimal, traceable edits over broad rewrites.
- You may refer to repository files directly with `@` file references when the UI supports them.
- For rule-driven work, prefer short requests such as `Rule: @ai-rules/5-create-tasks.md` and `Feature: 01-some-feature`.
- If the user says `rule 1`, `rule 2`, `rule 3`, and so on, treat that as an instruction to run the corresponding downstream rule rather than merely describing it.
- Any time the user asks you to execute a rule, look through the relevant instructions in `ai-rules/` before proceeding.
- Branch-sensitive rules should use `/ai-work/00-workflow-config.md` as the source of truth for whether branch-based feature workflow is `required` or `optional`.
- If a branch-sensitive rule needs that config and it is missing, ask the user which mode to use, write the answer to `/ai-work/00-workflow-config.md`, and then continue.
- In `branch_mode: optional`, branch operations are advisory unless the user explicitly asks for them or a specific rule says otherwise.

## Approval Style

- When a downstream rule requires user approval, ask for it with this exact question: `Approve this? Y/N.`

## Tone

- Be clear, direct, and technically precise, but do not default to a cold or mechanical tone.
- Prefer a mildly warm, personable style that feels collaborative and human while staying concise.
- Keep that tone lightweight. Do not add fluff, exaggerated enthusiasm, or unnecessary filler.

## Environment-Agnostic Defaults

- Keep commands non-interactive when feasible.
- Consider the consequences of running commands in parallel before attempting to do so.

## Execution Constraints

- Do not start long-running processes in-session, including dev servers, watchers, or persistent background jobs, unless the user explicitly asks.
- If a command may be slow, state the purpose briefly before running it.
- If reproducing an issue depends on a local dev server or another environment-sensitive command that is easier for the user to run directly, prefer asking the user to run it and share the output rather than spending time fighting local shell or process-capture limitations.
- Follow higher-priority system, developer, and tool instructions when they conflict with repository guidance.

## Editing Expectations

- Prefer small, focused changes that match the existing codebase patterns.
- Preserve unrelated user changes in the worktree.
- When practical, validate changes with targeted checks or tests that do not require long-running processes.

## JavaScript Style

- Use 4-space indentation. Do not use tabs for indentation.
- Put opening braces on a new line for functions, methods, conditionals, loops, and classes unless an existing file clearly follows a different local convention.
- Prefer simple functions and methods where practical.
- Favor straightforward control flow and small units of logic over clever or densely abstracted code.
- Add brief comments before each logical block of code to orient the reader.
- Keep comments short and directional. Do not restate obvious code behavior unless an obscure or complex algorithm needs explanation.
- Precede standalone comments with a blank line.
- End-of-line comments are acceptable in short declaration blocks. Align those comments to a consistent visual column so they remain tidy.
