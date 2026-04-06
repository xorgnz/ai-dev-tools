# Windows Environment Notes

Use this overlay when the downstream project is being run from a Windows shell environment.

## Commands And Paths

- Use commands that work in the current Windows shell environment unless higher-priority instructions require an alternative.
- Use Windows paths when executing local commands. Forward-slash paths are fine in documentation and code when the underlying tool supports them.
- In PowerShell, do not chain command steps with `&&`; run sequential commands as separate shell invocations instead.

## Runtime Assumptions

- Assume the project is being run with Node on Windows unless the target repository clearly documents a different local runtime expectation.
