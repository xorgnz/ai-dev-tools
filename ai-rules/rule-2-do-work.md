# Root Execution Rule

## Goal

To guide an agent in carrying out approved root-level work for this repository in a controlled, trackable way, while using the current active plan in `ai-work/active/` when the work is planned and otherwise allowing direct handling of small ad hoc requests.

## When To Use

Use this rule when the user asks to perform approved root-level work in this repository, whether that work is planned or ad hoc.

This rule applies only to root-level repository work.

It does not apply downstream implementation rules inside this repository.

## Core Principle

Root execution in this repository should be simple and explicit.

The agent should:

- identify the relevant active plan and approved work item within it when the work is being tracked through `ai-work/`
- perform only the approved task
- keep the work scoped to root-level repository maintenance
- update plan progress and the work log as work is completed when the work is being tracked through `ai-work/`

Do not silently continue into the next task after finishing the current one.

## Task Source

Use the relevant plan document in `ai-work/active/` as the execution source when the user is working from a planned effort or explicitly points to a planning artifact.

If the user makes a small ad hoc root-level request and does not ask to plan it, do not create or require a plan by default.

Use `ai-work/work-log.md` as the supporting activity record when broader context is needed for planned work.

Plans stored in `ai-work/archive/` are historical records and should not be executed directly. If the user wants to resume archived work, move or copy the plan back into `ai-work/active/`, confirm the active work item, and then proceed.

## Task Selection Process

1. If the user gives a specific work item or plan name, use that after confirming the request is explicit enough to execute.
2. If the user asks for a small ad hoc root-level change without asking to plan it, execute the approved request directly without creating a plan.
3. If the user asks to do work without naming a task but the request appears to refer to planned work, review the relevant active plan, identify the next sensible incomplete item, present it briefly, and then ask `Approve this? Yes/No.` before proceeding.
4. If more than one plausible work item or active plan matches the request, do not infer. Ask the user which one to perform.

## Execution Rules

- Never start root work without explicit user approval.
- Complete only the approved task.
- Do not silently expand scope.
- Do not silently move to the next task.
- Keep the work focused on root rules, root docs, planning artifacts, repository structure, or other approved root-level maintenance.

## Progress Tracking

As each approved work item or sub-task is completed in planned work:

1. Update the active plan promptly.
2. Change `- [ ]` to `- [x]` where appropriate.
3. Add a concise execution update to `ai-work/work-log.md`.
4. Keep the plan aligned with the actual work completed.

## General Working Principles

1. Prefer editing existing files over creating new ones unless creation is required.
2. Validate changes when practical, using checks appropriate to the kind of work performed.
3. Ask clarifying questions if the approved task is still ambiguous at execution time.
4. Do not execute downstream rules as if this repository were a downstream project.
5. Consult downstream materials only when the approved root task is specifically about editing or reviewing those downstream materials.
6. Do not create planning artifacts for small ad hoc requests unless the user explicitly asks to plan the work.
7. If the approved effort is complete and is being tracked through `ai-work/active/`, move its plan file from `ai-work/active/` to `ai-work/archive/` and record that transition in `ai-work/work-log.md`.
8. Do not execute work directly from an archived plan; reactivate it into `ai-work/active/` first.
9. If an active work item appears complete, ask the user whether it should be treated as done and archived rather than assuming closure.

## Process

### Inspect

1. Determine whether the request is planned work or a small ad hoc request.
2. If it is planned work, identify the relevant active plan in `ai-work/active/`.
3. If it is planned work, read that active plan before starting work.
4. Read `ai-work/work-log.md` when broader context is needed for planned work.
5. Confirm the intended task and scope before editing files.

### Execute

6. Perform the approved task.
7. Keep edits focused and traceable.
8. Run any appropriate validation that fits the work.
9. If the work is planned work, update plan progress in the active plan when the task or sub-task is completed.
10. If the work is planned work, add a concise execution entry to `ai-work/work-log.md`.

### Report

11. Report what was changed.
12. Report any validation performed.
13. Report whether the active plan and work log were updated, if applicable.

## Final Instructions

1. Never start work without explicit user approval.
2. Use the relevant plan in `ai-work/active/` when the work is planned.
3. Do not require a plan for small ad hoc root-level requests unless the user asks to create one.
4. Use `ai-work/work-log.md` for supporting context when needed for planned work.
5. Update completed checklist items promptly for planned work.
6. Stop after the approved task unless the user explicitly asks for more.
7. Treat archived plans as history, not active execution sources.
8. Ask the user before treating active work as complete and moving it to `ai-work/archive/`.
9. Treat `root rule 2` as a direct instruction to run this rule.
