# Junie-Specific Downstream Notes

Combine this file with `downstream/guidelines/shared.md` at deployment time.

These Junie-specific notes override the shared downstream guidance where shell behavior or path conventions differ.

## Environment And Commands

- Treat this terminal as WSL/Linux rather than Windows.
- Use POSIX/Linux commands such as `ls`, `grep`, `cat`, and `export`. Do not use PowerShell cmdlets or Windows path/backslash conventions.
- Prefer forward slashes in paths such as `ai-work/` and standard POSIX flags.
- All commands must be non-interactive. Add flags such as `-y` or `--yes` where applicable.

## Junie-Specific Execution Rules

- Always set `MARKER_JUNIE_TERMINAL=1` before executing bash commands.
