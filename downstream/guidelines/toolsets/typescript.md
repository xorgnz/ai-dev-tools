# TypeScript Toolset Notes

Use this overlay when the downstream project is primarily built with TypeScript.

## Toolset Expectations

- Prefer TypeScript over plain JavaScript for application and library code unless the target repository clearly uses JavaScript in the relevant area.
- Follow the existing `tsconfig.json` and formatter/linter settings in the target repository rather than imposing new defaults.
- When logic accumulates behavior, state, or rules, prefer explicit object boundaries with named classes or similarly clear structures.
- Treat free-standing global functions as the exception rather than the default.
- Treat anonymous object literals as short-lived transport values, not as substitutes for named domain objects that carry behavior, invariants, or lifecycle.

## TypeScript

- Prefer explicit types where they materially improve readability or catch edge cases, especially for exported functions, public interfaces, and complex data shapes.
- Avoid introducing broad `any` usage unless the surrounding code already relies on it and tightening types is outside the requested scope.
- Do not spread related behavior across ad hoc exported helpers unless the code is genuinely tiny, stateless, and local in scope.
- Keep helper types readable; avoid type-level cleverness unless the existing codebase already uses that style.

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
