# Overview

This file is the SvelteKit toolset fragment used to build downstream guidelines.

Any agent working in this repository may read or edit it.

Combine it with `downstream/guidelines/shared.md` during export.

All text in the `Fragment Content` section is included in the downstream export file. During export, heading levels are adjusted to fit the merged document hierarchy, and this fragment is placed under its own section header.

## Fragment Content

### SvelteKit Toolset Notes

Use this fragment when the downstream project is primarily built with SvelteKit.

#### Toolset Expectations

- Preserve the existing SvelteKit project structure and naming conventions unless the task explicitly requires restructuring.
- Prefer SvelteKit-native patterns for routing, data loading, form actions, and endpoint handling over custom framework abstractions.
- Follow the existing `svelte.config.*` and formatter/linter settings in the target repository rather than imposing new defaults.

#### SvelteKit

- Prefer `+page`, `+layout`, `+page.server`, `+server`, and related SvelteKit file conventions instead of custom routing layers.
- Keep server-only code out of client bundles.
- A Svelte component is itself a reasonable local boundary, so small component-specific helpers may live inside the component when they are tightly coupled to that component's view logic.
- Outside that component boundary, keep framework-required exported functions thin and move substantial behavior behind named classes or other explicit object-oriented structures rather than embedding it directly in `load` functions, actions, or request handlers.
- For load functions and actions, prefer straightforward data flow and explicit error handling over deeply abstracted helper wrappers.
- When editing Svelte components, preserve reactivity semantics and keep state flow easy to trace.

#### Validation

- When practical, prefer targeted checks that fit the stack, such as Svelte checks or focused test runs already defined by the target repository.
