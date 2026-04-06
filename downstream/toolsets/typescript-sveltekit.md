# TypeScript + SvelteKit Toolset Notes

Use this overlay when the downstream project is primarily built with TypeScript and SvelteKit.

## Toolset Expectations

- Prefer TypeScript over plain JavaScript for application and library code unless the target repository clearly uses JavaScript in the relevant area.
- Preserve the existing SvelteKit project structure and naming conventions unless the task explicitly requires restructuring.
- Prefer SvelteKit-native patterns for routing, data loading, form actions, and endpoint handling over custom framework abstractions.
- Follow the existing `tsconfig.json`, `svelte.config.*`, and formatter/linter settings in the target repository rather than imposing new defaults.

## TypeScript

- Prefer explicit types where they materially improve readability or catch edge cases, especially for exported functions, public interfaces, and complex data shapes.
- Avoid introducing broad `any` usage unless the surrounding code already relies on it and tightening types is outside the requested scope.
- Keep helper types readable; avoid type-level cleverness unless the existing codebase already uses that style.

## SvelteKit

- Prefer `+page`, `+layout`, `+page.server`, `+server`, and related SvelteKit file conventions instead of custom routing layers.
- Keep server-only code out of client bundles.
- For load functions and actions, prefer straightforward data flow and explicit error handling over deeply abstracted helper wrappers.
- When editing Svelte components, preserve reactivity semantics and keep state flow easy to trace.

## Validation

- When practical, prefer targeted checks that fit the stack, such as TypeScript checking, Svelte checks, or focused test runs already defined by the target repository.
