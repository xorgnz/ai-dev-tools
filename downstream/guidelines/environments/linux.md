# Overview

This file is the Linux environment fragment used to build downstream guidelines.

Any agent working in this repository may read or edit it.

Combine it with `downstream/guidelines/shared.md` during export.

All text in the `Fragment Content` section is included in the downstream export file. During export, heading levels are adjusted to fit the merged document hierarchy, and this fragment is placed under its own section header.

## Fragment Content

### Linux Environment Notes

Use this fragment when the downstream project is being run from a native Linux shell environment.

#### Commands And Paths

- Use POSIX/Linux commands such as `ls`, `grep`, `cat`, and `export`.
- Prefer forward slashes in paths such as `ai-work/` and standard POSIX flags.
- Keep commands non-interactive. Add flags such as `-y` or `--yes` where applicable.

#### Runtime Assumptions

- Treat the execution environment as native Linux shell behavior rather than Windows or WSL-specific shell behavior.
