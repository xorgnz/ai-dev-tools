# Root Execution Rule

## Goal

To guide an agent in carrying out approved root-level work for this repository in a controlled, trackable way, while keeping execution aligned with the current active plan in `ai-work/active/` and the work log in `ai-work/work-log.md`.

## When To Use

Use this rule when the user asks to perform planned work in this repository.

This rule applies only to root-level repository work.

It does not apply downstream implementation rules inside this repository.

## Core Principle

Root execution in this repository should be simple and explicit.

The agent should:

- identify the relevant active plan and approved work item within it
- perform only the approved task
- keep the work scoped to root-level repository maintenance
- update plan progress and the work log as work is completed

Do not silently continue into the next task after finishing the current one.

## Task Source

Use the relevant plan document in `ai-work/active/` as the default execution source unless the user explicitly points to a different planning artifact.

Use `ai-work/work-log.md` as the supporting activity record when broader context is needed.

Plans stored in `ai-work/archive/` are historical records and should not be executed directly. If the user wants to resume archived work, move or copy the plan back into `ai-work/active/`, confirm the active work item, and then proceed.

## Task Selection Process

1. If the user gives a specific work item or plan name, use that after confirming the request is explicit enough to execute.
2. If the user asks to do work without naming a task, review the relevant active plan, identify the next sensible incomplete item, present it briefly, and wait for approval before proceeding.
3. If more than one plausible work item or active plan matches the request, do not infer. Ask the user which one to perform.

## Execution Rules

- Never start root work without explicit user approval.
- Complete only the approved task.
- Do not silently expand scope.
- Do not silently move to the next task.
- Keep the work focused on root rules, root docs, planning artifacts, repository structure, or other approved root-level maintenance.

## Progress Tracking

As each approved work item or sub-task is completed:

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
6. If the approved effort is complete, move its plan file from `ai-work/active/` to `ai-work/archive/` and record that transition in `ai-work/work-log.md`.
7. Do not execute work directly from an archived plan; reactivate it into `ai-work/active/` first.
8. If an active work item appears complete, ask the user whether it should be treated as done and archived rather than assuming closure.

## Process

### Inspect

1. Identify the relevant active plan in `ai-work/active/`.
2. Read that active plan before starting work.
3. Read `ai-work/work-log.md` when broader context is needed.
4. Confirm the intended task and scope before editing files.

### Execute

5. Perform the approved task.
6. Keep edits focused and traceable.
7. Run any appropriate validation that fits the work.
8. Update plan progress in the active plan when the task or sub-task is completed.
9. Add a concise execution entry to `ai-work/work-log.md`.

### Report

10. Report what was changed.
11. Report any validation performed.
12. Report whether the active plan and work log were updated.

## Final Instructions

1. Never start work without explicit user approval.
2. Use the relevant plan in `ai-work/active/` as the default execution source.
3. Use `ai-work/work-log.md` for supporting context when needed.
4. Update completed checklist items promptly.
5. Stop after the approved task unless the user explicitly asks for more.
6. Treat archived plans as history, not active execution sources.
7. Ask the user before treating active work as complete and moving it to `ai-work/archive/`.
