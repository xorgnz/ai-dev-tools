# Root Planning Rule

## Goal

To guide an agent in planning new root-level work for this repository by creating or updating a single active plan document in `ai-work/active/` and recording the planning activity in `ai-work/work-log.md`.

## When To Use

Use this rule when the user asks to plan new work for this repository.

This rule applies to root-level planning only.

It does not create downstream scope or PRD artifacts, and it should not apply downstream planning rules inside this repository.

Do not invoke this rule for small ad hoc root-level requests unless the user explicitly asks to create or update a plan.

## Core Principle

Root planning in this repository is intentionally simple.

The agent should:

- identify the relevant active plan document in `ai-work/active/`
- update the plan document to describe the intended work at a high level and include actionable items
- record the planning update in `ai-work/work-log.md`
- keep the planning focused on documentation, rule changes, repository structure, or other root-level management work

Because this repository is primarily about AI rules and workflow assets, root planning should stay lighter than downstream software-planning workflows.

## Planning Artifacts

Root planning should use the relevant files in `ai-work/`.

The default planning locations are:

- `ai-work/active/`
- `ai-work/archive/`
- `ai-work/work-log.md`

Each root-level effort should have exactly one active plan document.

Plan filenames should use the format `yyyy-mm-dd - NN - description - plan.md`, where `NN` is a two-digit sequence number for that date.

If only one obvious active plan exists for the requested effort, use it.

If multiple plausible active plans exist, do not infer. Ask the user which plan should be updated.

## Process

### Inspect

1. Review the user's request and determine whether it is root-level work for this repository.
2. Identify the relevant active plan file in `ai-work/active/`, or determine that a new plan must be created.
3. Read the existing plan document before changing it when one already exists.
4. Read `ai-work/work-log.md` when prior planning context is needed.
5. Determine whether the requested work is:
   - a new planning item to add
   - an update to an existing phase or task set
   - a reorganization of the current plan
6. If the intended planning scope is unclear, ask concise clarifying questions before editing the planning files.

### Propose

7. Summarize the planned update briefly before making substantial changes when the direction is not already clear from the user's request.
8. Keep the proposed planning focused on root-level repository work, not downstream feature implementation.
9. If approval is needed before writing the plan, present the proposed update and then ask `Approve this? Y/N.`

#### Approval Policy

`@shared-snippets/approval-policy.md`

### Execute

10. Create a new dated and numbered plan file in `ai-work/active/` when no suitable active plan exists, or update the existing active plan when it does.
11. Keep the plan concrete, reviewable, and easy to execute over time.
12. Include actionable checklist items or similarly explicit work items in the plan document itself.
13. Prefer modifying an existing active plan over creating a duplicate plan unless the user clearly wants a separate work track.
14. Add a concise entry to `ai-work/work-log.md` describing the planning action taken.

### Report

15. Report which plan file was created or updated.
16. Report whether `ai-work/work-log.md` was updated.
17. Summarize the new planning items that were added or changed.

## Default Behavior

- If the user asks to plan work and there is one obvious active plan in `ai-work/active/`, use it.
- If the user asks to plan work for a new effort and no suitable active plan exists yet, create a new dated and numbered plan file in `ai-work/active/`.
- If the user asks to plan work but the request is too vague to produce meaningful actions, ask for clarification rather than writing filler.
- Root planning should update the plan and the work log unless the user explicitly asks otherwise.
- Treat `root rule 1` as a direct instruction to run this rule.

## Final Instructions

1. Keep root planning simpler than downstream project planning.
2. Use one active plan document per root-level effort.
3. Do not use downstream scope or PRD workflows for root-level repository planning.
4. Do not infer among multiple plausible planning targets in `ai-work/active/`.
5. Record planning activity in `ai-work/work-log.md`.
