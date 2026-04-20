# Shared Snippets (Root)

Purpose
- Centralize short, canonical text snippets that are reused across files to prevent wording drift.

Scope
- For any section that points to a snippet, the snippet file is the source of truth for that section text.
- Root guidance references snippet files directly with `@...`.
- Downstream shared guidance references snippet files with include tags that are resolved during export.
- Snippet files are source artifacts and should not be copied as standalone files into `downstream/export/`; their content is inlined where includes are resolved.

Conventions
- One concept per file; keep each snippet small and self-contained.
- In root guidance (`ai-rules/*`), reference snippets with `@shared-snippets/<file>.md`.
- In downstream shared guidance (`downstream/guidelines/*`), reference snippets with include tags:
  - `<include src="../../shared-snippets/<file>.md" />`
- During export or other assembly steps, resolve downstream include tags by inlining the referenced snippet text.

Maintenance Workflow
1. Edit the relevant snippet here first.
2. Keep destination files pointing at snippet references instead of duplicating snippet text.
3. Resolve downstream include tags only in generated output that needs fully inlined text.

Current Snippets
- `scope-discipline.md` - Canonical scope-discipline sentence used in root and downstream.
- `approval-style-question.md` - Canonical approval question string.
- `clarification-line.md` - Canonical one-line clarification guidance.
- `explicit-instruction-required.md` - Canonical requirement that agents do work only when explicitly instructed.
- `tone-baseline.md` - Canonical shared tone bullets for root and downstream guidance.
- `environment-agnostic-defaults.md` - Canonical command execution defaults.
- `execution-constraints.md` - Canonical constraints for process and Git command execution.
- `editing-expectations.md` - Canonical editing and validation expectations.

Notes
- If a snippet needs environment- or toolset-specific detail, that detail likely belongs in a fragment under `downstream/guidelines/environments/` or `downstream/guidelines/toolsets/`, not in the snippet itself.
