---
version: 2.0.0
timestamp: 2026-05-13 00:00
---
# Rule: Review Changelog Consistency Against Commit History

## Purpose

Use this rule when the user wants to review `/changes/changelog.md` for consistency and compare it against recent commit history to find:

- missing stakeholder-facing changes that should have been recorded
- extraneous bullets that do not appear justified by the relevant commits
- bullets that should be revised because the current text does not accurately represent the committed work

This rule is intended for release preparation, deploy preparation, or periodic changelog cleanup.

## Core Principle

Treat rule `08-prepare-commit.md` as the source of truth for changelog decision-making.

- Reuse rule 8's inclusion logic instead of inventing a second set of editorial rules here.
- Reuse rule 8's `ignore`, `add`, and `revise` outcomes when evaluating commit history against the changelog.
- Use this rule to review consistency, not to create a parallel changelog policy.
- If rule 8 and rule 13 appear to disagree, follow rule 8 and report the mismatch so the rules can be aligned.

## File Contract

- Use the repository-root path `/changes/changelog.md`.
- Treat the file as a markdown bullet list for stakeholder-facing change notes.
- If the file is missing, treat that as an empty changelog and compare it against the inspected commit range accordingly.
- If the file exists but is not a readable markdown bullet list, stop and ask the user how to proceed instead of guessing a repair.

## Review Scope

- Review the changelog against a user-specified commit range when one is provided.
- Otherwise inspect a reasonable recent range based on the current release-preparation context and state that range explicitly before proposing edits.
- Prefer a bounded recent range over the full repository history unless the user explicitly asks for a full-history review.

## Decision Rules

When evaluating each relevant commit or cluster of closely related commits, apply rule 8's outcome model:

1. `ignore`
   - The commit should not appear in the stakeholder changelog.
2. `add`
   - The changelog is missing a bullet that should exist.
3. `revise`
   - An existing bullet should be updated because it is incomplete, misleading, duplicative, or otherwise weaker than a revised representation.

Do not invent new outcome categories here.

## Matching Guidance

- Use commit subjects, scoped diffs, and surrounding commit context to compare committed work against existing changelog bullets.
- Allow one changelog bullet to represent multiple closely related commits when that better matches rule 8's stakeholder-facing intent.
- Look for opportunities to merge discontiguous but related commits into one changelog bullet when they clearly describe the same stakeholder-facing change, even if unrelated commits appear in between.
- A later bug fix, polish pass, follow-up tweak, or completion step may justify revising an earlier bullet instead of adding another one when the combined story is clearer for stakeholders.
- Allow one later commit to justify revising an earlier bullet rather than adding a new one when the combined result is the clearer stakeholder story.
- Do not require feature tags or task ids in every bullet, but use them as supporting evidence when they are present.
- Treat clearly administrative or agent-facing commits according to rule 8's ignore criteria rather than trying to surface them here as stakeholder changes.

## Process

### Inspect

1. Read `08-prepare-commit.md` and use its stakeholder change-list rules as the decision baseline.
2. Read `/changes/changelog.md` when it exists.
3. Determine the commit range to review.
4. Inspect the commits in that range.
5. Compare the changelog bullets and commit history for:
   - likely missing bullets
   - likely extraneous bullets
   - likely revision candidates
   - likely multi-commit groupings that should be represented as one bullet despite unrelated commits appearing between them

### Propose

6. Present the proposed changelog actions before writing.
7. Group the proposal into:
   - `add`
   - `revise`
   - `ignore`, for commits reviewed and intentionally left out
8. For each proposed `add` or `revise`, show:
   - the relevant commit or commit cluster, including discontiguous related commits when applicable
   - the reason based on rule 8's decision logic
   - the proposed bullet text
9. If an existing bullet appears clearly extraneous, present that as a `revise` proposal whose approved result is to remove the bullet because rule 8's logic would not record it.
10. If any mapping remains ambiguous, say so clearly instead of forcing a cleanup decision.
11. Ask `Approve this? Y/N.` before modifying `/changes/changelog.md`.

### Execute

12. Apply only the approved changelog edits.
13. Preserve bullet-list structure unless the user explicitly asks for broader reformatting.
14. Do not rewrite unaffected bullets for style alone.

### Report

15. Report the commit range that was reviewed.
16. Report how many bullets were added, revised, or removed.
17. Report whether any ambiguous or unresolved review items remain.
18. Report whether `/changes/changelog.md` was updated.

## Output Expectations

When using this rule, report:

- which commit range was reviewed
- which commits were treated as `ignore`
- which missing bullets were proposed
- which existing bullets were proposed for revision
- which existing bullets were proposed for deletion through `revise`, if any
- whether the changelog was updated
