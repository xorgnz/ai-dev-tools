# CSS Toolset Notes

Use this fragment when the downstream project relies on custom CSS authoring conventions.

## Toolset Expectations

- Keep CSS edits local and predictable. Prefer extending existing selectors and structure over introducing a new styling pattern.
- Preserve existing design tokens (`var(--...)`) and spacing scales unless the task explicitly asks for new values.
- Keep selectors explicit and shallow where practical; avoid deep chained selectors unless the surrounding file already depends on them.

## Declaration Ordering

- Order declarations inside each rule in this sequence: size, position/layout, box/body, then text/content.
- Within each group, order declarations alphabetically.
- Size group: `width`, `height`, `min-*`, `max-*`, `aspect-ratio`.
- Position/layout group: `display`, `position`, inset properties, `z-index`, `transform`, and layout properties such as `flex`, `grid`, `align-*`, `justify-*`, and `overflow`.
- Box/body group: `box-sizing`, `margin`, `padding`, `border`, `border-radius`, `box-shadow`, `background-*`.
- Text/content group: `color`, typography properties, `line-height`, and text alignment.
- If a declaration does not fit clearly into one of the groups, place it in an `other` group at the end of the rule.

## Rule Ordering

- Inside each `<style>` block, order selectors to match markup flow from top to bottom as closely as practical.
- Put global/context selectors first (for example `:global(...)`), then page/container selectors, then child sections, then reusable utility selectors.
- Keep media-query overrides at the end, preserving the same selector order used in the base rules.

## Selector Strategy

- Prefer classes for reusable patterns and component styling.
- Use `id` selectors when the element is truly singular and the surrounding codebase already uses `id`-based styling for similar cases.
- If an element already has a stable selector in use, prefer extending that selector instead of adding a parallel one without a clear reason.

## Validation

- When practical, run the repository's existing style or check command after CSS edits.
