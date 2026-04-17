# Overview

This file is the Windows environment fragment used to build downstream guidelines.

Any agent working in this repository may read or edit it.

Combine it with `downstream/guidelines/shared.md` during export.

All text in the `Fragment Content` section is included in the downstream export file. During export, heading levels are adjusted to fit the merged document hierarchy, and this fragment is placed under its own section header.

## Fragment Content

### Windows Environment Notes

Use this fragment when the downstream project is being run from a Windows shell environment.

This means native Windows shell usage, not WSL, unless the target repository explicitly says otherwise.

#### Commands And Paths

- Use commands that work in the current Windows shell environment unless higher-priority instructions require an alternative.
- Use Windows paths when executing local commands. Forward-slash paths are fine in documentation and code when the underlying tool supports them.
- In PowerShell, do not chain command steps with `&&`; run sequential commands as separate shell invocations instead.

#### Runtime Assumptions

- Assume the project is being run with Node on Windows unless the target repository clearly documents a different local runtime expectation.
- Treat `windows` and `wsl` as distinct environment choices. Do not assume WSL behavior when the selected environment is Windows.
