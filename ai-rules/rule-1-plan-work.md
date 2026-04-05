# Root Planning Rule

## Goal

To guide an agent in planning new root-level work for this repository by updating the relevant plan document and adding actionable items to the relevant task document in `ai-work/`.

## When To Use

Use this rule when the user asks to plan new work for this repository.

This rule applies to root-level planning only.

It does not create downstream scope or PRD artifacts, and it should not apply downstream planning rules inside this repository.

## Core Principle

Root planning in this repository is intentionally simple.

The agent should:

- identify the relevant planning artifact pair in `ai-work/`
- update the plan document to describe the intended work at a high level
- add or update actionable items in the task document
- keep the planning focused on documentation, rule changes, repository structure, or other root-level management work

Because this repository is primarily about AI rules and workflow assets, root planning should stay lighter than downstream software-planning workflows.

## Planning Artifacts

Root planning should use the relevant files in `ai-work/`.

The default planning files are:

- `ai-work/plan.md`
- `ai-work/tasks.md`

If only one obvious plan/task pair exists for the requested effort, use it.

If multiple plausible plan/task pairs exist, do not infer. Ask the user which planning set should be updated.

## Process

### Inspect

1. Review the user's request and determine whether it is root-level work for this repository.
2. Identify the relevant plan file and task file in `ai-work/`.
3. Read the existing planning documents before changing them.
4. Determine whether the requested work is:
   - a new planning item to add
   - an update to an existing phase or task set
   - a reorganization of the current plan
5. If the intended planning scope is unclear, ask concise clarifying questions before editing the planning files.

### Propose

6. Summarize the planned update briefly before making substantial changes when the direction is not already clear from the user's request.
7. Keep the proposed planning focused on root-level repository work, not downstream feature implementation.

### Execute

8. Update the relevant plan file with the high-level structure, phases, goals, or sequencing needed for the requested work.
9. Update the relevant task file with actionable tasks that correspond to the plan.
10. Keep tasks concrete, reviewable, and easy to mark complete over time.
11. Prefer modifying existing planning artifacts over creating duplicate planning files unless the user clearly wants a new planning track.

### Report

12. Report which plan file and task file were updated.
13. Summarize the new planning items that were added or changed.

## Default Behavior

- If the user asks to plan work and there is one obvious plan/task pair in `ai-work/`, use it.
- If the user asks to plan work for a new effort and no suitable planning files exist yet, create a new plan file and matching task file in `ai-work/`.
- If the user asks to plan work but the request is too vague to produce meaningful tasks, ask for clarification rather than writing filler.
- Root planning should produce both plan updates and task updates unless the user explicitly asks for only one.

## Final Instructions

1. Keep root planning simpler than downstream project planning.
2. Update the plan document and the task document together unless the user explicitly asks otherwise.
3. Do not use downstream scope or PRD workflows for root-level repository planning.
4. Do not infer among multiple plausible planning targets in `ai-work/`.
5. Keep planning artifacts aligned so the tasks clearly support the plan.
