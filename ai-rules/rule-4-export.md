# Root Export Rule

## Goal

To guide an agent in generating a clean downstream export bundle for one specific agent by merging the shared downstream guidelines with that agent's downstream guideline overlay, one required environment-specific guideline overlay, any requested toolset-specific guideline overlays, and replacing the contents of `downstream/export/` with the resulting bundle.

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
- build the export from `downstream/guidelines/shared.md`, one agent-specific downstream guideline file, one environment-specific guideline file, any explicitly requested toolset-specific guideline files, and the current downstream `ai-rules/`
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
- `downstream/guidelines/codex.md`
- `downstream/guidelines/claude.md`
- `downstream/guidelines/junie.md`
- `downstream/environments/`
- `downstream/toolsets/`
- `downstream/ai-rules/`
- `ai-rules/export-profiles.md`

When a change is specific to an environment or technology stack, prefer updating `downstream/environments/` or `downstream/toolsets/` rather than pushing that guidance into rules.

If it seems necessary to put environment-specific or toolset-specific behavior into a rule instead of an overlay, ask the user before doing so.

## Export Profiles

Saved export profiles live in `ai-rules/export-profiles.md`.

Each saved profile should define:

- a profile identifier
- one explicit target agent
- one explicit target environment
- zero or more explicit toolset overlays

A named saved profile counts as explicit export input when the user names that profile.

If the user asks to save or update a profile, write the resolved profile values to `ai-rules/export-profiles.md`.

If the user names both a saved profile and separate export values and they conflict, do not silently merge or override them. Ask the user which source of truth to use.

## Environment Overlays

Environment-specific guidance lives under `downstream/environments/`.

One environment overlay is required for every export.

The supported environment targets are:

- `windows`
- `wsl`
- `linux`

Do not infer the environment from the current session agent or shell. The export environment must come from the user's request or a clarification response.

## Toolset Overlays

Toolset-specific guidance lives under `downstream/toolsets/`.

Each toolset overlay is technology-specific rather than agent-specific and may be combined with any supported agent export.

Include toolset overlays only when the user explicitly asks for them or when an approved export already specifies them.

If the user asks to export with toolset-specific guidance but does not identify the toolset, ask which toolset overlay to include.

## Export Layout

Write the generated bundle into `downstream/export/`.

`downstream/export/` is a generated folder. Its contents should not be kept in git and should be created only when an export run needs them.

The export must contain:

1. One merged guideline file for the requested agent:
   - `codex` -> `downstream/export/AGENTS.md`
   - `claude` -> `downstream/export/CLAUDE.md`
   - `junie` -> `downstream/export/.junie/guidelines.md`
2. A full copy of `downstream/ai-rules/` under `downstream/export/ai-rules/`

The merged guideline file should consist of:

1. the shared downstream guidelines
2. the selected agent-specific downstream guideline file
3. the selected environment-specific guideline file
4. any selected toolset-specific guideline files

Keep clear separation between each section in the merged guideline file.

## Process

### Inspect

1. Confirm that the request is to export downstream artifacts, save a profile, update a profile, or a combination of those actions.
2. Identify any requested export profile.
3. If a profile is named, read `ai-rules/export-profiles.md` and resolve the profile values from there.
4. Identify the requested target agent.
5. Identify the requested target environment.
6. Identify any requested toolset overlays.
7. If no specific target agent is provided directly or through a named profile, ask which agent to export.
8. If no specific target environment is provided directly or through a named profile, ask which environment to export: `windows`, `wsl`, or `linux`.
9. Read the shared downstream guideline file, the selected agent-specific downstream guideline file, and the selected environment-specific guideline file.
10. Read any selected toolset-specific guideline files.
11. Read the downstream `ai-rules/` set that will be copied into the export bundle.
12. Inspect the current contents of `downstream/export/` if the folder already exists.

### Execute

13. If the user asked to save or update a profile, write the resolved profile entry to `ai-rules/export-profiles.md`.
14. If the request includes an export run and `downstream/export/` already exists, remove the existing files and directories inside it.
15. If the request includes an export run, create the export folder structure needed for the selected agent.
16. If the request includes an export run, write the merged guideline file to the correct agent-specific export path.
17. If the request includes an export run, copy the full downstream `ai-rules/` directory into `downstream/export/ai-rules/`.
18. If the request includes an export run, ensure the export contains only artifacts for the selected agent, the selected environment, and any explicitly selected toolset overlays.

### Report

19. Report which profile was used, created, or updated, if any.
20. Report which agent was exported.
21. Report which environment was exported.
22. Report which toolset overlays were included, if any.
23. Report which guideline file was generated.
24. Report that `downstream/export/` was replaced with the new export bundle when an export run occurred.

## Default Behavior

- If the user says `root rule 4`, treat that as a direct instruction to run this rule.
- If the user asks to export by profile, use the named profile as the explicit source of agent, environment, and toolset values.
- If the user asks to save or update a profile, require one explicit agent and one explicit environment for that profile, and record any explicit toolset overlays.
- If the user asks to export but does not name an agent directly or through a profile, ask which one: `codex`, `claude`, or `junie`.
- If the user asks to export but does not name an environment directly or through a profile, ask which one: `windows`, `wsl`, or `linux`, and do not proceed until the user answers.
- If the user asks to export with toolset-specific guidance but does not name the toolset, ask which toolset overlay to include.
- If the export folder already contains files, replace them as part of the export for the requested agent.
- If the export folder does not exist yet, create it as part of the export run.
- If the named profile does not exist, stop and report the missing profile instead of inferring a fallback.
- If the selected agent, selected environment, or requested toolset overlay does not have a source file, stop and report the missing source instead of inferring a fallback.

## Final Instructions

1. Require one explicit target agent before exporting, either directly or through a named saved profile.
2. Require one explicit target environment before exporting, either directly or through a named saved profile.
3. Do not infer the target agent or environment from the current session.
4. Treat a named saved profile as explicit export input, not as inferred context.
5. Include toolset-specific guidance only when the user explicitly asks for it or the approved export or saved profile already names it.
6. Replace the contents of `downstream/export/` on each export run.
7. Export exactly one merged guideline file and one `ai-rules/` copy for the selected agent.
8. Do not mix artifacts for multiple agents in the same export folder.
9. Treat `downstream/export/` as generated output and do not preserve its contents in git.
