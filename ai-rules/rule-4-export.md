# Root Export Rule

## Goal

To guide an agent in generating a clean downstream export bundle for one specific agent by merging the shared downstream guidelines with that agent's downstream guideline overlay, plus any requested toolset-specific guideline overlays, and replacing the contents of `downstream/export/` with the resulting bundle.

## When To Use

Use this rule when the user asks to export downstream guidance for a specific agent from this repository.

This rule applies only to generating downstream export artifacts from the source files stored in this repository.

## Core Principle

Export generation should be explicit and reproducible.

The agent should:

- require one specific target agent before exporting
- build the export from `downstream/guidelines/shared.md`, one agent-specific downstream guideline file, any explicitly requested toolset-specific guideline files, and the current downstream `ai-rules/`
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
- `downstream/toolsets/`
- `downstream/ai-rules/`

## Toolset Overlays

Toolset-specific guidance lives under `downstream/toolsets/`.

Each toolset overlay is technology-specific rather than agent-specific and may be combined with any supported agent export.

Include toolset overlays only when the user explicitly asks for them or when an approved export already specifies them.

If the user asks to export with toolset-specific guidance but does not identify the toolset, ask which toolset overlay to include.

## Export Layout

Write the generated bundle into `downstream/export/`.

The export must contain:

1. One merged guideline file for the requested agent:
   - `codex` -> `downstream/export/AGENTS.md`
   - `claude` -> `downstream/export/CLAUDE.md`
   - `junie` -> `downstream/export/.junie/guidelines.md`
2. A full copy of `downstream/ai-rules/` under `downstream/export/ai-rules/`

The merged guideline file should consist of:

1. the shared downstream guidelines
2. the selected agent-specific downstream guideline file
3. any selected toolset-specific guideline files

Keep clear separation between each section in the merged guideline file.

## Process

### Inspect

1. Confirm that the request is to export downstream artifacts.
2. Identify the requested target agent.
3. Identify any requested toolset overlays.
4. If no specific target agent is provided, ask which agent to export.
5. Read the shared downstream guideline file and the selected agent-specific downstream guideline file.
6. Read any selected toolset-specific guideline files.
7. Read the downstream `ai-rules/` set that will be copied into the export bundle.
8. Inspect the current contents of `downstream/export/` before replacing them.

### Execute

9. Remove the existing files and directories inside `downstream/export/`.
10. Recreate the export folder structure needed for the selected agent.
11. Write the merged guideline file to the correct agent-specific export path.
12. Copy the full downstream `ai-rules/` directory into `downstream/export/ai-rules/`.
13. Ensure the export contains only artifacts for the selected agent and the explicitly selected toolset overlays.

### Report

14. Report which agent was exported.
15. Report which toolset overlays were included, if any.
16. Report which guideline file was generated.
17. Report that `downstream/export/` was replaced with the new export bundle.

## Default Behavior

- If the user says `root rule 4`, treat that as a direct instruction to run this rule.
- If the user asks to export but does not name an agent, ask which one: `codex`, `claude`, or `junie`.
- If the user asks to export with toolset-specific guidance but does not name the toolset, ask which toolset overlay to include.
- If the export folder already contains files, replace them as part of the export for the requested agent.
- If the selected agent or requested toolset overlay does not have a source file, stop and report the missing source instead of inferring a fallback.

## Final Instructions

1. Require one explicit target agent before exporting.
2. Do not infer the target agent from the current session.
3. Include toolset-specific guidance only when the user explicitly asks for it or the approved export already names it.
4. Replace the contents of `downstream/export/` on each export run.
5. Export exactly one merged guideline file and one `ai-rules/` copy for the selected agent.
6. Do not mix artifacts for multiple agents in the same export folder.
