# Header

This file is the SvelteKit toolset fragment used to build downstream guidelines.

Any agent working in this repository may read or edit it.

This `Header` section is source-only metadata and must not be copied into downstream export files.

# Content

## Toolset Expectations

- Preserve the existing SvelteKit project structure and naming conventions unless the task explicitly requires restructuring.
- Prefer SvelteKit-native patterns for routing, data loading, form actions, and endpoint handling over custom framework abstractions.
- Follow the existing `svelte.config.*` and formatter/linter settings in the target repository rather than imposing new defaults.

## SvelteKit

- Prefer `+page`, `+layout`, `+page.server`, `+server`, and related SvelteKit file conventions instead of custom routing layers.
- Keep server-only code out of client bundles.
- A Svelte component is itself a reasonable local boundary, so small component-specific helpers may live inside the component when they are tightly coupled to that component's view logic.
- Outside that component boundary, keep framework-required exported functions thin and move substantial behavior behind named classes or other explicit object-oriented structures rather than embedding it directly in `load` functions, actions, or request handlers.
- For load functions and actions, prefer straightforward data flow and explicit error handling over deeply abstracted helper wrappers.
- When editing Svelte components, preserve reactivity semantics and keep state flow easy to trace.
- Keep `load` functions, form actions, and request handlers focused on transport concerns: parse inputs, resolve request-scoped context, call the right service, and map service failures to HTTP or form responses.
- Return plain serializable data from `load` and action responses. Do not return class instances or other non-POJO values to SvelteKit page data.
- When route behavior needs cross-query orchestration, persistence coordination, or policy decisions, move that behavior into a named server-side service rather than growing the route file.
- Prefer one clear server-side orchestration layer per request flow. Routes should not become a second home for business rules that already exist in services.
- Treat page data as a deliberate contract. Add fields intentionally, name them clearly, and avoid growing load payloads with incidental internal state.
- Keep query-string parsing, param parsing, and form parsing explicit at the route boundary rather than relying on loosely shaped request access deep in the stack.
- Prefer server-derived truth for availability, permissions, workflow status, and other rule-bearing state. The client should reflect those decisions rather than recomputing them independently.
- Distinguish between coordinating components and presentational components. Avoid making one component carry both heavy workflow logic and broad rendering responsibility when a clearer split is available.
- Keep component APIs narrow and purposeful. A large set of booleans or mode flags is usually a sign that the component is handling too many roles.
- Prefer semantic callbacks and named payloads over passing raw DOM events through multiple layers when a higher-level intent is what the caller actually needs.


## Validation

- When practical, prefer targeted checks that fit the stack, such as Svelte checks or focused test runs already defined by the target repository.
