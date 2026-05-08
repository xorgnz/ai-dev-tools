# Header

This file is the TypeScript toolset fragment used to build downstream guidelines.

Any agent working in this repository may read or edit it.

This `Header` section is source-only metadata and must not be copied into downstream export files.

# Content

## Toolset Expectations

- Prefer TypeScript over plain JavaScript for application and library code unless the target repository clearly uses JavaScript in the relevant area.
- Follow the existing `tsconfig.json` and formatter/linter settings in the target repository rather than imposing new defaults.
- When logic accumulates behavior, state, or rules, prefer explicit object boundaries with named classes or similarly clear structures.
- Treat free-standing global functions as the exception rather than the default.
- Do not leave related behavior scattered across floating top-level functions when a clear concept-owning class or module boundary would make the code easier to understand.
- When behavior is stateless and should remain functional, group related functions into a deliberately named utility module with one defensible purpose rather than a grab-bag of unrelated helpers.
- Do not replace a forest of small floating functions with a forest of one-function classes. Introduce classes when they represent a real concept, state owner, coordinator, or policy boundary.
- Prefer one obvious owner for each non-trivial concept. If multiple modules can plausibly claim the same behavior, the boundary is weak.
- Separate domain models, persistence projections, and UI-facing view models unless they are genuinely the same concept.
- Prefer explicit construction and clearly named factory/conversion points over broad implicit reshaping of objects across layers.
- Treat anonymous object literals as short-lived transport values, not as substitutes for named domain objects that carry behavior, invariants, or lifecycle.

## TypeScript

- Prefer explicit types where they materially improve readability or catch edge cases, especially for exported functions, public interfaces, and complex data shapes.
- Avoid introducing broad `any` usage unless the surrounding code already relies on it and tightening types is outside the requested scope.
- Do not spread related behavior across ad hoc exported helpers unless the code is genuinely tiny, stateless, and local in scope.
- Keep helper types readable; avoid type-level cleverness unless the existing codebase already uses that style.
- Avoid anonymous object types wherever practical. Prefer named types for reusable payloads, public contracts, cross-module boundaries, and any non-trivial data shape.
- Keep inline object types only for very local, obvious, one-use transport values where introducing a named type would not improve clarity.
- For a real domain concept, prefer a simple field-value type plus an entity class when behavior or invariants need a clear home.
- Keep entity and field-value names in domain/TypeScript shape. Do not let storage-specific naming conventions leak through the rest of the application.
- Treat anonymous objects as transport values at boundaries. If logic, invariants, or lifecycle accumulate around a concept, promote it to a named type or class.
- When a query returns a one-off aggregate or projection rather than a real domain object, keep that result shape local to the persistence or service layer unless it is reused meaningfully elsewhere.
- Keep names aligned across layers unless there is a real boundary reason to translate them.
- Prefer test builders, fixtures, or named helpers over repeating large ad hoc object literals across tests.
- Use explicit suffixes when they clarify role: prefer \*DAO` for persistence boundaries, `*Service` for orchestration, `*Fields` for plain entity field-value shapes, and `*ViewModel` for UI-facing projection types.`

## JavaScript Style

- Use 4-space indentation. Do not use tabs for indentation.
- Put opening braces on a new line for functions, methods, conditionals, loops, and classes unless an existing file clearly follows a different local convention.
- Prefer simple functions and methods where practical.
- Favor straightforward control flow and small units of logic over clever or densely abstracted code.
- Add brief comments before each logical block of code to orient the reader.
- Keep comments short and directional. Do not restate obvious code behavior unless an obscure or complex algorithm needs explanation.
- Precede standalone comments with a blank line.
- End-of-line comments are acceptable in short declaration blocks. Align those comments to a consistent visual column so they remain tidy.

## Validation

- When practical, prefer targeted checks that fit the stack, such as TypeScript checking or focused test runs already defined by the target repository.
