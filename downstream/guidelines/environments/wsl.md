# WSL Environment Notes

Use this fragment when the downstream project is being run from WSL on Windows.

## Commands And Paths

- Use POSIX/Linux commands such as `ls`, `grep`, `cat`, and `export`. Do not use PowerShell cmdlets.
- Prefer forward slashes in paths such as `ai-work/` and standard POSIX flags.
- Keep commands non-interactive. Add flags such as `-y` or `--yes` where applicable.

## Runtime Assumptions

- Treat the execution environment as Linux-style shell behavior running under WSL rather than native Windows shell behavior.
- Treat `wsl` and `windows` as distinct environment choices. Do not assume native Windows shell behavior when the selected environment is WSL.
