# Linux Environment Notes

Use this overlay when the downstream project is being run from a native Linux shell environment.

## Commands And Paths

- Use POSIX/Linux commands such as `ls`, `grep`, `cat`, and `export`.
- Prefer forward slashes in paths such as `ai-work/` and standard POSIX flags.
- Keep commands non-interactive. Add flags such as `-y` or `--yes` where applicable.

## Runtime Assumptions

- Treat the execution environment as native Linux shell behavior rather than Windows or WSL-specific shell behavior.
