---
version: 1.0.0
timestamp: 2026-04-30 00:00
---
# Rule: Create or Update the Project Overview

## Purpose

Create or refresh `/ai-work/00-project-overview.md` so agents can quickly understand the project as a whole without re-reading the entire repository and planning layer first.

## Output

- **Format:** Markdown
- **Location:** `/ai-work/`
- **Filename:** `00-project-overview.md`

## Process

### Inspect

1. Review the project as a whole before drafting the overview
2. Read all planning documents in `/ai-work/` that are relevant to understanding the project
   - Use the full planning set to understand the project as a whole rather than carrying individual planning documents forward into the overview
   - Summarize the system as it currently stands by integrating relevant material from active, planned, completed, closed, and archived feature documents into a single synthesized description
   - After summarizing the current system, identify current work and future work separately where that helps explain the project's present direction
   - Do not reproduce, embed, or enumerate full feature planning documents inside the overview
3. Review the repository structure and the implementation surface enough to describe:
   - the project's overall objective
   - the key features or workflows
   - the architecture and relevant tech stack
   - the high-level directory layout and key files
4. If `/ai-work/00-project-overview.md` already exists, treat the rule invocation as an update request
5. When updating, compare the existing overview against the current repository and planning documents, then identify what must be added, corrected, removed, or reorganized

### Propose

6. Prepare the proposed overview content in a concise, agent-facing form
7. If creating the file for the first time, present the proposed document or a clearly structured summary of its sections before writing
8. If updating an existing file, show a concise summary of the proposed changes before asking for approval
   - Include the important additions, removals, corrections, and structural changes
   - Make it clear that approval will update `/ai-work/00-project-overview.md`

### Approval Gate

9. Do not write or update `/ai-work/00-project-overview.md` until the user explicitly approves
10. Ask `Approve this? Y/N.` when the proposal is ready to write

### Execute and Report

11. Write the approved content to `/ai-work/00-project-overview.md`
12. Report whether the file was created or updated

## Required Content

The overview must include:

1. A brief statement of what the project seeks to achieve
2. A summary of the key features or functional areas
3. A brief architecture overview that refers to the relevant tech stack where needed
4. A high-level directory guide describing the layout of major folders and the location of key files

## Default Template

Use this as the default starting structure unless the user asks for a different format or the project clearly needs a different organization:

```md
# Project Overview

## Purpose

Briefly describe what the project is for, who it serves, and what it is trying to achieve.

## Current System Summary

Summarize the system as it exists today in a single integrated narrative.
Fold in relevant understanding from completed, closed, or archived work without treating those planning documents as current work.

## Key Features

- Feature or capability area
  - What it does
  - Why it matters
- Feature or capability area
  - What it does
  - Why it matters

## Architecture Overview

### Tech Stack

- Frontend:
- Backend:
- Data/storage:
- Testing:
- Tooling/infrastructure:

### System Shape

Briefly explain how the main parts of the system fit together.
Focus on major boundaries, data flow, and important implementation structure.

## Directory Guide

### Top-Level Layout

- `top-level-folder-or-file/` - What this area contains and why it matters
- `top-level-folder-or-file/` - What this area contains and why it matters
- `top-level-folder-or-file/` - What this area contains and why it matters

If `src/` or an equivalent implementation root exists, unpack its important subfolders instead of leaving it as a single broad entry. The goal is to show where the real implementation is organized, not merely to mention that source code exists.

Example pattern:

- `src/` - Primary implementation root
  - `src/area-or-module/` - Responsibility of this part of the system
  - `src/area-or-module/` - Responsibility of this part of the system

### Key Files

- `path/to/file` - Why it matters
- `path/to/file` - Why it matters
- `path/to/file` - Why it matters

## Current Work

List the active or near-term work that is relevant to understanding the project's current direction.

- Work item
- Work item

## Future Work

List planned or future work that helps explain where the project is heading.

- Work item
- Work item
```

## Writing Guidance

- Optimize for fast orientation by a newly arrived agent
- Prefer concise synthesis over exhaustive detail
- Keep the document current with both the repository and the planning documents
- Refer to key files and directories explicitly when that improves navigation
- Describe the project's observed layout as it exists; do not treat the template examples as a prescribed directory structure
- When a source root such as `src/` contains meaningful internal structure, unpack the important subfolders so the overview helps agents navigate the implementation
- You may refer to active, planned, or future work directly when that helps explain the current project trajectory
- Do not refer directly to closed, completed, or archived feature documents in the overview; instead, fold any still-relevant understanding into the synthesized project description
- Do not turn the directory guide into a full file listing; keep it high level and practical
