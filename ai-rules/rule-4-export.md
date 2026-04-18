# Root Export Rule

## Goal

To guide an agent in generating a clean downstream export bundle for one specific agent by merging the shared downstream guidelines with that agent's downstream guideline fragment, one required environment-specific guideline fragment, any requested toolset-specific guideline fragments, and replacing the contents of `downstream/export/` with the resulting bundle.

This rule also supports saved export profiles so the user can reuse a previously recorded export target without restating every export input each time.

## When To Use

Use this rule when the user asks to export downstream guidance for a specific agent from this repository.

Use this rule also when the user asks to create, update, or reuse a saved export profile for this repository.

This rule applies only to generating downstream export artifacts from the source files stored in this repository.

## Core Principle

Export generation should be explicit and reproducible.

The agent should:

- require one specific target agent before exporting
- require one specific target environment before exporting
- build the export from `downstream/guidelines/shared.md`, one agent-specific downstream guideline file, one environment-specific guideline file, any explicitly requested toolset-specific guideline files, and the current downstream `rules/`
- allow a named saved export profile to supply that explicit target data
- treat `downstream/export/` as generated output rather than source content
- replace the existing contents of `downstream/export/` with the new bundle for that one agent
- avoid mixing artifacts for multiple agents in the same export pass

## Supported Agents

The supported export targets are:

- `codex`
- `claude`
- `junie`

Do not infer the target agent from the current session agent. The export target must come from the user's request or a clarification response.

## Source Materials

Use these source locations:

- `downstream/guidelines/shared.md`
- `downstream/guidelines/agents/codex.md`
- `downstream/guidelines/agents/claude.md`
- `downstream/guidelines/agents/junie.md`
- `downstream/guidelines/environments/`
- `downstream/guidelines/toolsets/`
- `downstream/rules/`
- `shared-snippets/`
- `ai-rules/export-profiles.md`

When a change is specific to an environment or technology stack, prefer updating `downstream/guidelines/environments/` or `downstream/guidelines/toolsets/` rather than pushing that guidance into rules.

If it seems necessary to put environment-specific or toolset-specific behavior into a rule instead of a fragment, ask the user before doing so.

## Export Profiles

Saved export profiles live in `ai-rules/export-profiles.md`.

Each saved profile should define:

- a profile identifier
- one explicit target agent
- one explicit target environment
- zero or more explicit toolset fragments

A named saved profile counts as explicit export input when the user names that profile.

If the user asks to save or update a profile, write the resolved profile values to `ai-rules/export-profiles.md`.

If the user names both a saved profile and separate export values and they conflict, do not silently merge or override them. Ask the user which source of truth to use.

## Environment Fragments

Environment-specific guidance lives under `downstream/guidelines/environments/`.

One environment fragment is required for every export.

The supported environment targets are:

- `windows`
- `wsl`
- `linux`

Do not infer the environment from the current session agent or shell. The export environment must come from the user's request or a clarification response.

## Toolset Fragments

Toolset-specific guidance lives under `downstream/guidelines/toolsets/`.

Each toolset fragment is technology-specific rather than agent-specific and may be combined with any supported agent export.

Include toolset fragments only when the user explicitly asks for them or when an approved export already specifies them.

If the user asks to export with toolset-specific guidance but does not identify the toolset, ask which toolset fragment to include.

## Structured Selection Prompt

If the user does not provide a profile and does not provide a complete export selection set, ask for missing selections in one structured prompt.

Use this menu format:

```text
Select export fragments:
1 Agent: A) codex  B) claude  C) junie
2 Environment: A) windows  B) wsl  C) linux
3 Toolsets (optional, combine letters): A) typescript  B) sveltekit  C) css
Reply with shorthand like: 1A 2B 3AB
```

Parsing rules:

- `1` selects the target agent and accepts one letter.
- `2` selects the target environment and accepts one letter.
- `3` selects optional toolset fragments and may contain multiple letters in one token, such as `3AB`.
- Tokens may be separated by spaces, commas, or both.
- Letter matching is case-insensitive.
- If a required selector (`1` or `2`) is missing or invalid, ask again with the same structured menu.
- If `3` is omitted, treat toolset selection as empty.
- If any token is ambiguous, ask the user to restate using the same shorthand format.

## Export Layout

Write the generated bundle into `downstream/export/`.

`downstream/export/` is a generated folder. Its contents should not be kept in git and should be created only when an export run needs them.

The export must contain:

1. One merged guideline file for the requested agent:
   - `codex` -> `downstream/export/AGENTS.md`
   - `claude` -> `downstream/export/CLAUDE.md`
   - `junie` -> `downstream/export/.junie/guidelines.md`
2. A full copy of `downstream/rules/` under `downstream/export/ai-rules/`

The merged guideline file should consist of:

1. the shared downstream guidelines
2. the selected agent-specific downstream guideline file
3. the selected environment-specific guideline file
4. any selected toolset-specific guideline files

Keep clear separation between each section in the merged guideline file.

In the merged guideline file, each selected fragment must appear under its own section header.

Do not preserve fragment heading levels verbatim when that would break the merged file hierarchy. Normalize heading levels so each fragment's `Content` section fits cleanly under its section header in the merged output.

Because the merged file already has top-level structure, fragment section headers should not be emitted as top-level (`#`) headings in the merged output.

If any source section contains snippet include tags such as `<include src="../../shared-snippets/<file>.md" />`, resolve those includes by inlining the referenced snippet text in the merged export file.

## Process

### Inspect

1. Confirm that the request is to export downstream artifacts, save a profile, update a profile, or a combination of those actions.
2. Identify any requested export profile.
3. If a profile is named, read `ai-rules/export-profiles.md` and resolve the profile values from there.
4. Identify the requested target agent.
5. Identify the requested target environment.
6. Identify any requested toolset fragments.
7. If the user did not provide a profile and any required selection is missing, ask one structured selection prompt and parse the shorthand response.
8. If no specific target agent is provided directly, through a named profile, or through parsed shorthand, ask again using the structured selection prompt.
9. If no specific target environment is provided directly, through a named profile, or through parsed shorthand, ask again using the structured selection prompt.
10. Read the shared downstream guideline file, the selected agent-specific downstream guideline file, and the selected environment-specific guideline file.
11. Read any selected toolset-specific guideline fragment files.
12. Read the downstream `rules/` set that will be copied into the export bundle.
13. Inspect the current contents of `downstream/export/` if the folder already exists.

### Execute

14. If the user asked to save or update a profile, write the resolved profile entry to `ai-rules/export-profiles.md`.
15. If the request includes an export run and `downstream/export/` already exists, remove the existing files and directories inside it.
16. If the request includes an export run, create the export folder structure needed for the selected agent.
17. If the request includes an export run, write the merged guideline file to the correct agent-specific export path.
18. If the request includes an export run, copy the full downstream `rules/` directory into `downstream/export/ai-rules/`.
19. If the request includes an export run, resolve any snippet include tags in the merged guideline content before finalizing the output file.
20. If the request includes an export run, ensure each selected fragment is emitted under its own non-top-level section header and normalize fragment heading levels to match merged file hierarchy.
21. If the request includes an export run, ensure the export contains only artifacts for the selected agent, the selected environment, and any explicitly selected toolset fragments.

### Report

22. Report which profile was used, created, or updated, if any.
23. Report which agent was exported.
24. Report which environment was exported.
25. Report which toolset fragments were included, if any.
26. Report which guideline file was generated.
27. Report that `downstream/export/` was replaced with the new export bundle when an export run occurred.

## Default Behavior

- If the user says `root rule 4`, treat that as a direct instruction to run this rule.
- If the user asks to export by profile, use the named profile as the explicit source of agent, environment, and toolset values.
- If the user asks to save or update a profile, require one explicit agent and one explicit environment for that profile, and record any explicit toolset fragments.
- If no profile is provided and one or more selections are missing, ask once using the structured selection prompt and parse shorthand like `1A 2B 3AB`.
- If the user asks to export but does not name an agent directly, through a profile, or through valid shorthand, do not proceed until agent selection is resolved.
- If the user asks to export but does not name an environment directly, through a profile, or through valid shorthand, do not proceed until environment selection is resolved.
- If the user asks to export with toolset-specific guidance but does not name toolsets directly or through valid shorthand, ask again using the structured selection prompt.
- If the export folder already contains files, replace them as part of the export for the requested agent.
- If the export folder does not exist yet, create it as part of the export run.
- If the named profile does not exist, stop and report the missing profile instead of inferring a fallback.
- If the selected agent, selected environment, or requested toolset fragment does not have a source file, stop and report the missing source instead of inferring a fallback.

#### Approval Policy

`@shared-snippets/approval-policy.md`

## Final Instructions

1. Require one explicit target agent before exporting, either directly or through a named saved profile.
2. Require one explicit target environment before exporting, either directly or through a named saved profile.
3. Do not infer the target agent or environment from the current session.
4. Treat a named saved profile as explicit export input, not as inferred context.
5. Include toolset-specific guidance only when the user explicitly asks for it or the approved export or saved profile already names it.
6. Replace the contents of `downstream/export/` on each export run.
7. Export exactly one merged guideline file and one rules copy at `downstream/export/ai-rules/` for the selected agent.
8. Do not mix artifacts for multiple agents in the same export folder.
9. Treat `downstream/export/` as generated output and do not preserve its contents in git.
