# Junie-Specific Downstream Notes

This file is for Junie. If you are a different agent, ignore this file and look for your own guidelines file instead. If your guidelines file does not exist in this project, report that to the user before proceeding.

Combine this file with `downstream/guidelines/shared.md` at deployment time.

Environment-specific shell and path behavior should come from the selected file in `downstream/environments/`.

## Junie-Specific Execution Rules

- Always set `MARKER_JUNIE_TERMINAL=1` before executing bash commands.
