# Root Execution Rule

## Goal

To guide an agent in carrying out approved root-level work for this repository in a controlled, trackable way, while keeping execution aligned with the current plan and task list in `ai-work/`.

## When To Use

Use this rule when the user asks to perform planned work in this repository.

This rule applies only to root-level repository work.

It does not apply downstream implementation rules inside this repository.

## Core Principle

Root execution in this repository should be simple and explicit.

The agent should:

- identify the relevant task in `ai-work/tasks.md`
- perform only the approved task
- keep the work scoped to root-level repository maintenance
- update task progress as work is completed

Do not silently continue into the next task after finishing the current one.

## Task Source

Use `ai-work/tasks.md` as the default root task list unless the user explicitly points to a different planning artifact.

Use `ai-work/plan.md` as the supporting high-level reference for why the task exists and how it fits into the broader work.

## Task Selection Process

1. If the user gives a specific task number or task name, use that task after confirming the request is explicit enough to execute.
2. If the user asks to do work without naming a task, review `ai-work/tasks.md`, identify the next sensible incomplete task, present it briefly, and wait for approval before proceeding.
3. If more than one plausible task matches the request, do not infer. Ask the user which one to perform.

## Execution Rules

- Never start root work without explicit user approval.
- Complete only the approved task.
- Do not silently expand scope.
- Do not silently move to the next task.
- Keep the work focused on root rules, root docs, planning artifacts, repository structure, or other approved root-level maintenance.

## Progress Tracking

As each task or sub-task is completed:

1. Update `ai-work/tasks.md` promptly.
2. Change `- [ ]` to `- [x]` where appropriate.
3. Keep the task file aligned with the actual work completed.

## General Working Principles

1. Prefer editing existing files over creating new ones unless creation is required.
2. Validate changes when practical, using checks appropriate to the kind of work performed.
3. Ask clarifying questions if the approved task is still ambiguous at execution time.
4. Do not execute downstream rules as if this repository were a downstream project.
5. Consult downstream materials only when the approved root task is specifically about editing or reviewing those downstream materials.

## Process

### Inspect

1. Read `ai-work/tasks.md`.
2. Read `ai-work/plan.md` when broader context is needed.
3. Confirm the intended task and scope before editing files.

### Execute

4. Perform the approved task.
5. Keep edits focused and traceable.
6. Run any appropriate validation that fits the work.
7. Update task progress in `ai-work/tasks.md` when the task or sub-task is completed.

### Report

8. Report what was changed.
9. Report any validation performed.
10. Report whether the task file was updated.

## Final Instructions

1. Never start work without explicit user approval.
2. Use `ai-work/tasks.md` as the default execution source.
3. Use `ai-work/plan.md` for supporting context when needed.
4. Update completed task checkboxes promptly.
5. Stop after the approved task unless the user explicitly asks for more.
