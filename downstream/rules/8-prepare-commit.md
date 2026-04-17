---
version: 1.9.2
timestamp: 2026-04-17 09:25
---
# Rule: Prepare a Commit for Approval

## Overview. 

This rule guides an AI assistant in preparing commits to git. To execute, work through steps 1 through 6 in order.

Use this rule when the user explicitly asks to run rule 8 or otherwise asks to prepare a commit.

## Prerequisites

- `/ai-work/00-workflow-config.md` should exist for commits tied to a tracked feature or task
- `/ai-work/00-feature-status.md` must exist for commits tied to a tracked feature or task
- Main task commits require an `active` tracked feature
- Ad hoc `feat` commits tied to a tracked feature also require an `active` tracked feature
- A task list should exist at `/ai-work/{feature-tag}-tasks.md` when using task-scoped context
- The relevant task should already be implemented when using task-scoped context
- Commits not tied to any tracked feature do not require an active tracked feature or task list
- Follow the shared feature-state contract in `/ai-work/00-feature-status.md`

## Core Principle

The AI must not commit automatically when using this rule unless the user explicitly includes approval in the same request.

Quick definitions:

- `context mode`: what the commit is attached to (`task-scoped`, `tracked-feature-scoped`, or `repo-scoped`)
- `commit prefix`: the literal prefix token (for example `feat`, `fix`, `mgmt`)
- `commit mode`: the behavior class inferred from the commit prefix

## Step 1 - Identify the context mode 

After identifying the commit mode, choose the context mode. Do not let the prefix alone pretend to answer the context question.

Context modes:

- `task-scoped`: the commit is tied to a specific task inside a specific tracked feature
- `tracked-feature-scoped`: the commit is tied to a specific tracked feature but not to a specific task
- `repo-scoped`: the commit is not tied to one specific tracked feature or task

Use this context-selection priority:

- If the user explicitly names a task, use task-scoped context unless the prefix forbids task-scoped use
- If the user explicitly names a tracked feature without a task, use tracked-feature-scoped context
- If the diff strongly matches one task, use task-scoped context when the prefix allows it
- If the diff clearly belongs to one tracked feature but not one task, use tracked-feature-scoped context
- If the diff does not clearly belong to one tracked feature, use repo-scoped context when the prefix allows it

A strong task diff match means one task is clearly favored by the actual changes, such as:

- the user explicitly names the task
- the changed files or modules line up cleanly with one task
- the task wording directly matches the scoped diff
- the current work is an obvious regression fix or follow-up to one task and no competing task is similarly plausible

A clear tracked-feature match means the work belongs to one tracked feature overall even if it does not map cleanly to one task.

Explicit tracked-feature selectors may override the active tracked feature for follow-up commit context. This does not change tracked-feature state, does not switch branches, and does not authorize implementation on that tracked feature by itself.

A `narrow recency fallback` means the assistant may use the most recently completed task as the commit's task context only when all of the following are true:

- the commit mode is `main-task`
- the user did not specify a task
- the diff does not strongly match any task
- the commit is still clearly tied to the active tracked feature
- there is one unambiguous most recently completed task in that tracked feature
- no other task is similarly plausible

Do not use the narrow recency fallback when any of the following are true:

- the commit mode is `ad-hoc-feat`, `follow-up`, or `management`
- the diff plausibly matches multiple tasks
- the work is only tracked-feature-scoped or repo-scoped
- the fallback would create a fake task relationship based only on recency

If two or more tasks remain plausible after applying the rules above, do not infer. Ask the user to choose.

### Step 1 execution checks

- If the user says only `run 8`, assume the active tracked feature
- Read `/ai-work/00-workflow-config.md` and `/ai-work/00-feature-status.md` when task-scoped or tracked-feature-scoped context may apply
- If `/ai-work/00-workflow-config.md` is needed and missing, ask whether `branch_mode` should be `required` or `optional`, write the file, and then continue
- Use the active tracked feature as the default tracked-feature context unless the user explicitly identifies another tracked feature for follow-up commit labeling, or the commit is repo-scoped
- Do not prepare main task commits when no tracked feature is active, even if the repository is still checked out on an old feature branch
- Do not prepare task-scoped or tracked-feature-scoped ad hoc `feat` commits when no tracked feature is active
- If `branch_mode: required`, use the active branch as an additional required source of truth for main task mode and for ad hoc `feat` when the selected context is task-scoped or tracked-feature-scoped
- If `branch_mode: required`, do not prepare main task commits or task-scoped or tracked-feature-scoped ad hoc `feat` commits when the current branch does not match the active tracked-feature branch
- If `branch_mode: optional`, do not reject implementation commit preparation solely because the current branch differs from any recorded tracked-feature branch
- If the user provides a task ID, use task-scoped context unless the commit mode forbids task-scoped use
- If the user provides a tracked-feature selector without a task ID, use tracked-feature-scoped context unless the diff clearly supports repo-scoped context and the user explicitly prefers that
- For `main-task`, if the user does not provide a task ID, identify the task that best matches the current diff before considering the narrow recency fallback
- For `ad-hoc-feat`, if the user does not provide a task ID, prefer task-scoped context when the diff strongly matches one task, otherwise prefer tracked-feature-scoped context when one tracked feature is clear, otherwise use repo-scoped context
- For `follow-up`, prefer task-scoped context when the match is strong, otherwise prefer tracked-feature-scoped context when one tracked feature is clear, otherwise use repo-scoped context
- For `management`, never infer a task; prefer repo-scoped context, and use tracked-feature-scoped context only when the work clearly belongs to one tracked feature
- For `management`, an explicit tracked-feature selector may reference a `planned`, non-active, or completed tracked feature without activating it
- Do not prepare main task commits or task-scoped or tracked-feature-scoped ad hoc `feat` commits for a paused tracked feature until it has been switched back to active
- Do not prepare new main task commits or task-scoped or tracked-feature-scoped ad hoc `feat` commits for completed tracked features unless the user explicitly asks for an exception
- Non-`mgmt` follow-up prefixes may reference a non-active or completed tracked feature as commit context when the rule otherwise permits that scope
- Repo-scoped follow-up commits and repo-scoped ad hoc `feat` commits may be prepared even when no tracked feature is active
- In main task mode only, if no clear task match exists after that and there is one obvious most recently completed task, use that task as the narrow last-resort fallback
- If the selected context is repo-scoped, use the reserved context marker `repo-0+`
- If two or more plausible tracked-feature mappings remain for tracked-feature-scoped context, do not infer
- Present the strongest candidate task or tracked-feature contexts briefly and ask the user to choose before proposing a commit
- If the diff appears to span multiple tasks, multiple tracked features, or unrelated work, surface that clearly and ask the user how to scope the commit

## Step 2 - Select prefix

Choose the commit prefix token before constructing the commit tag or message body.

### Terminology

Use these terms consistently:

- `commit prefix`: the literal prefix token from the command, such as `feat`, `fix`, or `mgmt`; the main task commit has an implicit main `feat` prefix even when the user does not spell it out
- `commit mode`: the behavior class inferred from the commit prefix
- `context mode`: what the commit is attached to: `task-scoped`, `tracked-feature-scoped`, or `repo-scoped`

### Follow-Up Commit Prefixes

The following explicit follow-up prefixes are also allowed when the user is preparing a commit that builds on existing work rather than representing the main task-completion commit:

- `tweak` - small targeted adjustments with no structural change: config values, tuning parameters, threshold adjustments, minor wording fixes
- `fix` - corrects a bug or unintended behavior
- `docs` - changes to purely informational content (READMEs, architecture docs, inline comments) that have no effect on behavior; skill files, CLAUDE.md, and command files are not `docs` - use `feat`, `fix`, or `tweak` depending on the nature of the change
- `style` - formatting, naming, or whitespace with no behavior change
- `tidy` - non-functional codebase cleanup within product/application code: dead code removal, internal reorganization, refactors with no behavior change, and maintenance dependency updates
- `mgmt` - repository/workflow management outside product code: `ai-work/`, rule/guideline files, planning notes, board/status files, `.gitignore`, and repository config

### Prefix-To-Mode Mapping

Do not blur commit prefix, commit mode, and context mode. They are separate decisions.

Use this mapping:

- implicit main `feat` -> `main-task`
- explicit `feat` -> `ad-hoc-feat`
- `fix`, `tidy`, `style`, `docs`, and `tweak` -> `follow-up`
- `mgmt` -> `management`

Map commit mode to allowed context modes like this:

- `main-task`: `task-scoped` only
- `ad-hoc-feat`: `task-scoped`, `tracked-feature-scoped`, or `repo-scoped`
- `follow-up`: `task-scoped`, `tracked-feature-scoped`, or `repo-scoped`
- `management`: `tracked-feature-scoped` or `repo-scoped`; never `task-scoped` unless the rule is explicitly revised later

### Prefix Selection Precedence

Use this precedence to choose or validate the commit prefix:

1. Use the user's explicit prefix when provided, unless it clearly conflicts with the scoped diff intent.
2. Determine primary intent from the full scoped diff and apply the existing prefix definitions in this rule.
3. Use changed-file mix as secondary evidence to confirm the intent decision.
4. If multiple prefixes remain plausible after this check, do not infer; ask the user to choose.

If an explicit prefix conflicts with the strongest scoped intent, present the mismatch and ask the user whether to keep the explicit prefix or switch.

### Invocation Parsing

After recognizing rule 8, parse trailing tokens in this order:

1. reserved rule-8 arguments
2. explicit task identifiers
3. explicit tracked-feature selectors such as `feature <tag>`, plus planned-feature selectors such as `for planned feature <tag>` when the commit mode permits planned tracked-feature context, currently `mgmt`
4. remaining free-form description text

Reserved rule-8 arguments are:

- `tidy`
- `style`
- `fix`
- `docs`
- `mgmt`
- `tweak`
- `feat`
- `approve`
- `approved`

If a token matches both a reserved rule-8 argument and a possible feature alias, treat it as the reserved rule-8 argument unless the user explicitly identifies a feature.

### Step 2 execution checks

- Parse the commit prefix from the user's command
- Map the commit prefix to the commit mode using the prefix-to-mode mapping above
- If the requested prefix conflicts with the strongest scoped diff intent, do not silently remap it; present the mismatch and ask the user whether to keep the requested prefix or switch

## Step 3 - Prepare tag

Prepare the tag segment that follows the prefix using selected context and mode.

Allowed tag shapes:

- `<feature-tag>-<task id>` for main task commits
- `<feature-tag>-<task id>+` for task-scoped follow-up and ad hoc feature commits
- `<feature-tag>-0+` for tracked-feature-scoped follow-up commits
- `repo-0+` for repo-scoped follow-up commits

Use Step 1 context rules and Step 2 prefix/mode rules together when selecting the tag.

The literal `repo` is a reserved context marker meaning the commit is not tied to one specific tracked feature.

Use `0+` only for tracked-feature-scoped or repo-scoped contexts, not for `main-task` commits.

## Step 4 - Commit message

Construct the full message in the required format and ensure the description matches the scoped diff.

### Required Commit Message Formats

```text
feat: <feature-tag>-<task id> - <description>
```

Ad hoc feature commits are also allowed when the user wants to make a focused feature addition without treating it as the main task-completion commit.

Ad hoc feature format:

```text
feat: <feature-tag>-<task id>+ - <description>
```

Repo-scoped ad hoc feature format:

```text
feat: repo-0+ - <description>
```

Follow-up format:

```text
<prefix>: <feature-tag>-<task id>+ - <description>
```

Tracked-feature-scoped follow-up format:

```text
<prefix>: <feature-tag>-0+ - <description>
```

Repo-scoped follow-up format:

```text
<prefix>: repo-0+ - <description>
```

### Step 4 execution checks

- Read `/ai-work/{feature-tag}-tasks.md` only when using task-scoped context
- Use the task wording as the basis for the description when a real task id is being used
- If the selected context is tracked-feature-scoped `0+` or repo-scoped `repo-0+`, base the description on the scoped diff and the user's wording instead of pretending a completed task exists
- For `mgmt`, do not rewrite the description as if the commit were task delivery or bug-fix work tied to one numbered task
- Review the current Git status
- Identify only the files related to the selected task, tracked feature, or repo-scoped support change
- Exclude unrelated or unfinished work
- For follow-up prefixes and ad hoc `feat`, treat the candidate commit message as a summary of the full scoped diff since `HEAD`, not just the most recent user request in the conversation
- If multiple related changes have accumulated since the last commit, make the description reflect the combined result at the chosen scope
- Keep the description concise and specific
- Prefer a narrow, task-aligned commit over a broad convenience commit
- For follow-up prefixes and ad hoc `feat`, summarize all known in-scope changes since the last commit that will be included in the proposed commit
- For `run 8 tidy`, `run 8 style`, `run 8 fix`, `run 8 docs`, `run 8 mgmt`, `run 8 feat`, and `run 8 tweak`, write the description to match the full scoped set of uncommitted changes since the last commit
- Surface unrelated changes clearly instead of silently bundling them
- If there are no changes, do not propose a commit

## Step 5 - Confirm with user

1. Present the proposed message and file list.
2. Ask `Approve this? Y/N.` unless the user already provided preapproval in the same command.
3. The approval question must clearly bind to that exact message and that exact scoped file set.
4. If the user's rule invocation already includes `approve` or `approved`, treat that as approval for the proposed task-scoped, tracked-feature-scoped, or repo-scoped commit.

## Step 6 - Create commit and report

1. Still inspect the chosen context and changed files first.
2. If the diff is clearly scoped to one task, one feature, or one repo-scoped support change under the context rules above, create the commit after preparing the message and file scope without asking a second approval question.
3. If the diff is ambiguous, spans multiple tasks, or includes unrelated work, stop and ask for clarification instead of using preapproval blindly.
4. After committing, report the commit message and resulting repository state.

Step 6 command sequencing rules:

- Do not rely on shell chaining semantics to serialize Git commit workflow steps across platforms
- Do not issue `git add`, `git commit`, or `git status` simultaneously through parallel tool calls
- Do not run `git status` at the same time as `git add` or `git commit`
- Run `git add`, `git commit`, and any post-commit `git status` as separate sequential shell commands
- Do not bundle `git add`, `git commit`, and `git status` into the same shell invocation

## Example Interaction Flow

```text
User: "run 8 mgmt for planned feature 03-user-auth"

AI: [Reads 00-feature-status.md and sees 03-user-auth is still planned]
AI: [Reviews the diff]
AI: [Treats `mgmt` as management mode and keeps the planned feature only as commit context]
AI: "Proposed commit: `mgmt: 03-user-auth-0+ - update auth rollout planning`"
```

```text
User: "run 8 fix feature 01-initial"

AI: [Reads 00-feature-status.md and the target feature task list]
AI: [Reviews the diff]
AI: [Uses the explicit feature selector rather than the active tracked feature]
AI: [Finds no strong task match inside that tracked feature]
AI: [Uses tracked-feature-scoped `0+`]
AI: "Proposed commit: `fix: 01-initial-0+ - resolve login redirect regression`"
```

```text
User: "run 8 fix"

AI: [Reviews the diff]
AI: [Finds no strong task match and no single clear feature match]
AI: [Uses repo-scoped context]
AI: "Proposed commit: `fix: repo-0+ - resolve shared config regression`"
```

```text
User: "run 8 approve"

AI: [Reads the active task list]
AI: [Reviews the diff]
AI: "The diff plausibly maps to task `3.4` and task `4.1`. I won't infer the task. Which one should this commit use?"
```
