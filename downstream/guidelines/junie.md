# Junie-Specific Downstream Notes

Combine this file with `downstream/guidelines/shared.md` at deployment time.

Environment-specific shell and path behavior should come from the selected file in `downstream/environments/`.

## Junie-Specific Execution Rules

- Always set `MARKER_JUNIE_TERMINAL=1` before executing bash commands.
