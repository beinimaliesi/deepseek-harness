# Web UI style reference

English | [中文](web-styling.zh.md)

This reference defines styling ownership and component rules for browser client packages. The current token values live in [`packages/client/ui-theme/src/styles/`](../packages/client/ui-theme/src/styles/); this document does not duplicate that generated-by-source inventory.

## Ownership

[`ui-theme`](../packages/client/ui-theme/README.md) owns the `--dsw-*` static scale, semantic aliases, named product-specific colors, typography, motion, gradients, shadows, scrollbar styles, and light/dark preference. [`ui-layout`](../packages/client/ui-layout/README.md) applies the resolved theme snapshot to the document. Feature packages consume theme-owned semantic or product-specific tokens and do not define another global theme.

Global style sheets belong in `ui-theme/src/styles/`. Component styles live beside their component as CSS Modules. A component may define a local custom property when its value is part of that component's layout or presentation contract; shared colors, typography, elevation, and motion belong to the theme package.

## Visual language

The Web UI uses a project-owned island visual language: warm brown text, cream surfaces, mint primary actions, pale green patterned backgrounds, rounded controls, soft elevation, and shallow 3D depth on primary actions. Dark mode maps the same roles onto forest-green surfaces and cream text. Code, terminal, and diff content retain the product's monospace requirements.

Existing controls and labeled function rows may receive icons on small mint, sun, coral, sky, or lilac tiles. The icon tile is decorative: it does not create a new action, replace the control's accessible name, or alter its event handler. Hover motion stays small, uses only transform, and is suppressed by the Web shell's shared reduced-motion rule.

The visual vocabulary is informed by the public [Animal Island UI design system](https://github.com/guokaigdg/animal-island-ui/tree/main/docs/design-system), whose repository is licensed under [CC BY-NC 4.0](https://github.com/guokaigdg/animal-island-ui/blob/main/LICENSE). DeepSeek Harness does not copy its source, font files, illustrations, or other assets and does not depend on that library. Theme values, CSS patterns, icon tiles, and motion are implemented locally with the existing component and icon systems.

## Component rules

- Use CSS Modules and `clsx`; do not add a component library or Tailwind.
- Use `--dsw-alias-*` semantic tokens or theme-owned `--dsw-specific-*` product tokens in feature components. Do not copy static palette values or write literal colors there.
- Keep theme selectors out of feature component CSS. Light/dark overrides belong to the theme owner.
- Pair font sizes with line heights and use the theme typography variables when an existing role matches.
- Keep source text, terminal output, and diff lines unwrapped when their component contract requires column preservation; use the shared scrollbar styles rather than component-specific scrollbar selectors.
- Put presentation in CSS. Inline React styles may pass component-local custom-property values but must not encode theme branches.
- Preserve keyboard focus visibility and reduced-motion behavior when adding transitions or hover-only controls.

## Changing the system

Add or change a shared token in the owning `ui-theme` sheet, then consume its semantic alias or named product-specific token from feature packages. Update the owning package reference when a public styling contract changes. Visual behavior follows the [testing policy](testing.md); the [styling-system Agent Note](../.agents/notes/implemented/process/2026-07-19-web-styling-system.md) records framework rationale, and the [island visual-language Agent Note](../.agents/notes/implemented/process/2026-08-14-island-web-visual-language.md) records the current baseline.
