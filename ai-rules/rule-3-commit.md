# Root Commit Rule

## Goal

To guide an agent in preparing a clean root-level management commit for this repository by inspecting the current changes, proposing a `mgmt:` commit message, and waiting for explicit user approval before creating the commit.

## When To Use

Use this rule when the user asks to commit changes made while maintaining this repository.

This rule applies to root-level repository management work, including edits made inside `downstream/` when those edits are part of maintaining this repository, unless the user explicitly asks to follow a different process.

## Core Principle

The agent must not commit automatically when using this rule unless the user explicitly includes approval in the same request.

The agent should:

- inspect the current changes
- summarize the current commit scope
- propose a commit message that starts with `mgmt:`
- wait for the user's approval unless approval was already included

All commits prepared under this rule are management commits for this repository and should use the `mgmt:` prefix.

## Process

### Inspect

1. Review the current Git status.
2. Review the changes since the last commit.
3. Identify the intended scope of the current root-level management changes.
4. Surface unrelated or unexpected changes clearly instead of silently bundling them into the proposed commit.
5. If the change set appears ambiguous, mixed, or overly broad, ask the user whether to narrow the scope before proposing the commit.

### Propose

6. Draft a concise commit message that starts with `mgmt:`.
7. Make the description reflect the actual scoped diff since `HEAD`, not just the most recent user request in the conversation.
8. Present the proposed message together with a short summary of the changes being committed.
9. Ask `Approve this? Yes/No.` unless the user already included approval in the same request.

### Execute And Report

10. Create the commit only after approval is available.
11. After committing, report the final commit message and resulting commit id.

## Default Behavior

- If the user asks to run this rule, assume they want a proposed commit message first.
- If there are no changes, do not propose a commit.
- If the diff includes both root-rule work and unrelated downstream changes, call that out clearly and ask the user how to scope the commit.
- Prefer one coherent management commit over a vague convenience commit.
- Treat `root rule 3` as a direct instruction to run this rule.

## PowerShell Command Guidance

- In this repository, commit preparation commands must be PowerShell-compatible.
- Do not chain `git add` and `git commit` with `&&`.
- Do not issue staging and commit commands simultaneously through parallel tool calls.
- Run staging, commit, and any follow-up status checks as separate sequential shell commands.

## Final Instructions

1. Do not create the commit until the user explicitly approves the message and scope, unless the same command already included approval.
2. Always inspect the current changes before proposing a commit.
3. Use a commit message that starts with the prefix `mgmt:`.
4. Make the proposed description match the full scoped set of changes being committed.
5. Surface unrelated changes clearly instead of silently bundling them.
