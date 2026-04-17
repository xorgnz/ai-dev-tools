# Overview

This file is the Junie-specific fragment used to build downstream guidelines.

Any agent working in this repository may read or edit it.

Combine it with `downstream/guidelines/shared.md` during export.

All text in the `Fragment Content` section is included in the downstream export file. During export, heading levels are adjusted to fit the merged document hierarchy, and this fragment is placed under its own section header.

## Fragment Content

- This file is for Junie. If you are a different agent, ignore this file and look for your own guidelines file instead. If your guidelines file does not exist in this project, report that to the user before proceeding.
- The deployment target for Junie uses `.junie/guidelines.md`.
- Always set `MARKER_JUNIE_TERMINAL=1` before executing bash commands.
