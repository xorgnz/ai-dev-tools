# TypeScript + SvelteKit Toolset Notes

Use this overlay when the downstream project is primarily built with TypeScript and SvelteKit.

## Toolset Expectations

- Prefer TypeScript over plain JavaScript for application and library code unless the target repository clearly uses JavaScript in the relevant area.
- Preserve the existing SvelteKit project structure and naming conventions unless the task explicitly requires restructuring.
- Prefer SvelteKit-native patterns for routing, data loading, form actions, and endpoint handling over custom framework abstractions.
- Outside an individual Svelte component, default to named classes and explicit object-oriented structure for application logic.
- Treat free-standing global functions as the exception rather than the default. There is usually no reason to model non-trivial behavior as a loose set of top-level helpers when that behavior can be owned by a class with clear responsibilities.
- Treat anonymous object literals as short-lived transport values, not as substitutes for named domain objects that carry behavior, invariants, or lifecycle.
- Follow the existing `tsconfig.json`, `svelte.config.*`, and formatter/linter settings in the target repository rather than imposing new defaults.

## TypeScript

- Prefer explicit types where they materially improve readability or catch edge cases, especially for exported functions, public interfaces, and complex data shapes.
- Avoid introducing broad `any` usage unless the surrounding code already relies on it and tightening types is outside the requested scope.
- When logic accumulates behavior, state, or rules, encapsulate it in a named class or another explicit object boundary with well-defined methods.
- Do not spread related behavior across ad hoc exported helpers unless the code is genuinely tiny, stateless, and local in scope.
- Keep helper types readable; avoid type-level cleverness unless the existing codebase already uses that style.

## SvelteKit

- Prefer `+page`, `+layout`, `+page.server`, `+server`, and related SvelteKit file conventions instead of custom routing layers.
- Keep server-only code out of client bundles.
- A Svelte component is itself a reasonable local boundary, so small component-specific helpers may live inside the component when they are tightly coupled to that component's view logic.
- Outside that component boundary, keep framework-required exported functions thin and move substantial behavior behind named classes or other explicit object-oriented structures rather than embedding it directly in `load` functions, actions, or request handlers.
- For load functions and actions, prefer straightforward data flow and explicit error handling over deeply abstracted helper wrappers.
- When editing Svelte components, preserve reactivity semantics and keep state flow easy to trace.

## Validation

- When practical, prefer targeted checks that fit the stack, such as TypeScript checking, Svelte checks, or focused test runs already defined by the target repository.
