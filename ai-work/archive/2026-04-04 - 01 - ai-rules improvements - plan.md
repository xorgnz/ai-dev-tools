# AI Rules Improvements Plan

## Archived Status

This plan is archived historical work that was previously tracked across `ai-work/plan.md` and `ai-work/tasks.md`.

It is kept as a past root-level effort under the current `ai-work/archive/` model.

## Overview

This document captures the proposed implementation plan for the workflow improvements identified in `ai-rules/__suggested_improvements.md`.

The work was executed in separate phases so rule contradictions were removed first, shared workflow standards were added second, and usability improvements were added last.

## Goals

1. Remove contradictions and ambiguous behavior from the current downstream `ai-rules` documents.
2. Standardize approval, ambiguity-handling, and execution patterns across the rule set.
3. Improve the usability of the rules with examples and shorthand guidance after the core behavior is stable.

## Non-Goals

- Changing application code outside `ai-rules`, `downstream`, and `ai-work` unless a supporting status or reference document must be updated.
- Activating a new product feature or switching the current implementation feature.
- Expanding the workflow beyond the improvements already identified in the suggestions review.

## Phase Breakdown

### Phase 1: Resolve Direct Rule Conflicts

#### Objective

Update the affected rule files so they no longer contradict themselves or each other in normal usage.

#### Target Files

- `downstream/ai-rules/1-create-feature-tag.md`
- `downstream/ai-rules/2-create-scope.md`
- `downstream/ai-rules/5-create-tasks.md`
- `downstream/ai-rules/8-prepare-commit.md`
- `downstream/ai-rules/9-change-feature.md`

#### Planned Changes

1. Narrow rule 1 so it only prompts for feature-tag creation when no valid target feature already exists.
2. Update rule 2 so scope creation is allowed for a specifically named `planned` feature without forcing activation through the feature-change workflow.
3. Define rule 5 parent-task behavior explicitly as a saved draft flow:
   - save the parent-task draft to `/ai-work/{feature-tag}-tasks.md`
   - wait for `Go`
   - expand the same file with sub-tasks and related details
4. Remove the `run 8 feat` ambiguity in rule 8 by treating ad hoc `feat` as a dedicated mode, not a generic follow-up prefix.
5. Enforce strict branch and feature-state alignment in rule 9 for pause and close flows.

### Phase 2: Add Shared Workflow Standards

#### Objective

Add cross-rule standards that reduce premature writes, ambiguous inference, and inconsistent execution flow.

#### Target Files

- `downstream/ai-rules/2-create-scope.md`
- `downstream/ai-rules/3-create-prd.md`
- `downstream/ai-rules/8-prepare-commit.md`
- `downstream/ai-rules/9-change-feature.md`

#### Planned Changes

1. Add explicit approval gates before writing durable scope and PRD documents.
2. Add a shared ambiguity-handling standard:
   - if two or more plausible interpretations exist, do not infer
   - present the candidates briefly
   - ask the user to choose
3. Standardize rule structure around:
   - inspect current state
   - propose artifact or action
   - wait for approval when needed
   - execute and report
4. Define a shared feature-state contract covering:
   - allowed status values
   - allowed transitions
   - whether no active feature is allowed
   - whether branch mismatch is ever permitted
   - completion metadata expectations
5. Tighten commit-task association guidance in rule 8 to prefer:
   - explicit task ID
   - best diff match
   - most recently completed task only as a fallback

### Phase 3: Improve Usability and Examples

#### Objective

Make the rule set easier to use in practice once the underlying behavior is stable.

#### Target Files

- `downstream/ai-rules/8-prepare-commit.md`
- `downstream/ai-rules/9-change-feature.md`
- `downstream/ai-rules/__suggested_improvements.md`
- `downstream/ai-rules/00-command-glossary.md`

#### Planned Changes

1. Add concrete examples for exceptional or high-risk cases:
   - creating scope for a planned feature
   - making a historical correction to a completed feature
   - preparing a commit when the diff spans multiple tasks
   - pausing or closing a feature when checkout is blocked by local changes
2. Add a short glossary for shorthand commands such as:
   - `Go`
   - `run 8`
   - `run 8 tidy`
   - `run 8 feat`
3. Update the suggestions document to show which recommendations were adopted and how they were implemented.

### Phase 4: Refine Feature-State Rules

#### Objective

Limit inactive-state handling and remove any implication that `main` is a normal working branch.

#### Planned Changes

1. Update rule 9 so standalone `pause` is no longer a primary user-facing workflow action.
2. Update the shared feature-state contract so `no active feature` is allowed only before the first feature is activated or after closing an active feature with no replacement selected.
3. Update rule 9 so closing a feature does not automatically require checkout to `main`, and instead reports any resulting inactive branch state clearly.
4. Review rules 6 and 8 so implementation and commit work are rejected whenever no feature is active, even if the repository is still on an old feature branch.
5. Update rule 9 examples so switching leaves the old feature `paused`, closing can leave no active feature selected, and no example implies working directly on `main`.

## Archived Task Record

### Relevant Files

- `downstream/ai-rules/1-create-feature-tag.md` - Phase 1 update to reduce redundant feature-tag prompting.
- `downstream/ai-rules/2-create-scope.md` - Phase 1 and Phase 2 updates for planned-feature scope handling and approval gates.
- `downstream/ai-rules/3-create-prd.md` - Phase 2 updates for approval-gated PRD writing.
- `downstream/ai-rules/5-create-tasks.md` - Phase 1 update for parent-task draft persistence behavior.
- `downstream/ai-rules/8-prepare-commit.md` - Phase 1, Phase 2, and Phase 3 updates for `feat` handling, ambiguity policy, commit-task association, and examples.
- `downstream/ai-rules/9-change-feature.md` - Phase 1, Phase 2, Phase 3, and Phase 4 updates for branch/state alignment, shared workflow structure, and exceptional-case examples.
- `downstream/ai-rules/00-command-glossary.md` - Phase 3 glossary for shorthand workflow commands.

### Completed Tasks

- [x] 1.0 Execute Phase 1 and resolve direct rule conflicts
  - [x] 1.1 Update rule 1 so feature-tag prompting only occurs when no valid feature context already exists
  - [x] 1.2 Update rule 2 so a specifically named `planned` feature can receive scope work without forced activation
  - [x] 1.3 Update rule 5 to define a saved parent-task draft flow before sub-task expansion after `Go`
  - [x] 1.4 Update rule 8 so ad hoc `feat` is a dedicated mode and not also treated as a generic follow-up prefix
  - [x] 1.5 Update rule 9 to require strict branch and feature-state alignment for pause and close flows
  - [x] 1.6 Review the edited Phase 1 files for remaining contradictions in examples, defaults, and final instructions
- [x] 2.0 Execute Phase 2 and add shared workflow standards
  - [x] 2.1 Add approval gates to scope creation so clarification or draft approval happens before file writes
  - [x] 2.2 Add approval gates to PRD creation so clarification or draft approval happens before file writes
  - [x] 2.3 Add a shared ambiguity-handling standard to the rules that currently rely on inference
  - [x] 2.4 Standardize the affected rules around inspect, propose, approval, execute, and report phases
  - [x] 2.5 Add a shared feature-state contract in the chosen document location
  - [x] 2.6 Update rule 8 to prioritize explicit task ID, then best diff match, then most recently completed task as fallback
  - [x] 2.7 Review the edited Phase 2 files for cross-rule consistency with the Phase 1 decisions
- [x] 3.0 Execute Phase 3 and improve usability with examples and glossary support
  - [x] 3.1 Add planned-feature and completed-feature exception examples where the rules now allow or restrict those cases
  - [x] 3.2 Add commit-preparation examples for ambiguous multi-task diffs and the adopted `run 8 feat` behavior
  - [x] 3.3 Add feature pause or close examples that show behavior when checkout is blocked by local changes
  - [x] 3.4 Add a short shorthand-command glossary in the chosen location if still needed after the rule edits
  - [x] 3.5 Record the adopted Phase 1-3 decisions and implemented fixes
  - [x] 3.6 Review the Phase 3 wording so the examples and glossary match the final rule behavior exactly
- [x] 4.0 Refine feature-state rules so inactive state is limited and main is not implied as a working branch
  - [x] 4.1 Update rule 9 so standalone `pause` is no longer a primary user-facing workflow action
  - [x] 4.2 Update the shared feature-state contract so `no active feature` is allowed only before the first feature is activated or after closing an active feature with no replacement selected
  - [x] 4.3 Update rule 9 so closing a feature does not automatically require checkout to `main`, and instead reports any resulting inactive branch state clearly
  - [x] 4.4 Review rules 6 and 8 so implementation and commit work are rejected whenever no feature is active, even if the repository is still on an old feature branch
  - [x] 4.5 Update rule 9 examples so switching leaves the old feature `paused`, closing can leave no active feature selected, and no example implies working directly on `main`
