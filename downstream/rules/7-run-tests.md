---
version: 1.1.0
timestamp: 2026-04-18 00:00
---
# Rule: Running Project Validation And Tests

## Prerequisites

- Follow the repository guidance in `AGENTS.md`
- Review the relevant task file at `/ai-work/{feature-tag}-tasks.md` when working against a specific feature
- Review `/ai-work/00-master-techstack.md` if it exists
- Inspect the repository's available scripts, documented commands, and test tooling before choosing commands

## Core Principle

Run the smallest meaningful validation set that matches the user's request and the scope of the change.

- Prefer documented project commands over ad hoc shell invocations
- Prefer fast, focused checks before broad validation when both are relevant
- Use one-shot commands; do not start watch mode or long-running processes unless the user explicitly asks
- Do not invent commands that are not present in the repository
- Treat validation-option prompts as selection prompts, not approval gates

## Process

1. **Identify Scope**
    - Determine whether the user wants:
        - a quick validation pass
        - validation for a specific task or feature
        - targeted checks for changed files
        - full-project validation
    - If the user asks to "run tests" or invokes this rule without specifying scope, inspect available commands, then ask which validation option to run.

2. **Inspect Available Commands**
    - Review likely command sources such as:
        - `package.json`
        - repository guidance files
        - `/ai-work/00-master-techstack.md`
        - `/ai-work/{feature-tag}-tasks.md` when applicable
        - project-specific README or tooling docs
    - Identify only commands that are actually available in the current repository.

3. **Choose Commands**
    - For a quick validation pass, prefer the repository's documented primary check.
    - For implementation work, choose commands that match the changed area:
        - static checks for type, lint, formatting, or framework issues
        - unit tests for isolated logic changes
        - integration or end-to-end tests when those suites exist and are relevant
    - If multiple commands are warranted, run them from fastest or narrowest to broadest.

4. **Ask When Needed**
    - If the user did not specify which validation option to run, present a short numbered list of available options.
    - Put the recommended or most recently used option first.
    - Do not ask an extra `Approve this? Y/N.` question for routine validation commands under normal workspace permissions.

5. **Run And Capture Results**
    - Run the selected one-shot commands.
    - Track whether each command passed, failed, or could not run.
    - If a command fails, decide whether later commands are still useful before continuing.

6. **Report Results**
    - State exactly which commands ran.
    - State whether each command passed, failed, or could not run.
    - Summarize important failures with enough detail to act on them.
    - If validation coverage is limited or no relevant tests exist, say so directly.

## Selection Prompt Format

When asking the user to choose a validation option, use a concise numbered list:

```text
Validation options:
1. <recommended command or command group> (Recommended/default)
2. <alternate command or command group>
```

If a validation command was already used earlier in the conversation, make that option first and mark it as previous/default.

## Examples

```text
Validation options:
1. npm run check (Recommended/default)
2. npm run test
```

```text
Validation options:
1. npm run check (previous/default)
2. npm run test
3. npm run typecheck
```

## Final Instructions

1. Always inspect available validation commands before choosing what to run.
2. If the user did not specify validation scope or command choice, ask them to choose from available options before running anything.
3. Default to the smallest meaningful validation set, not the largest possible set.
4. Never use watch-mode or long-running validation commands unless the user explicitly asks.
5. Present validation choices as numbered options and place the recommended/default option first.
6. Report coverage gaps instead of implying validation is broader than it is.
