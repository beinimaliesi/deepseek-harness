# Agent Note: Project-owned island visual language for the Web UI

Status: implemented

English | [中文](2026-08-14-island-web-visual-language.zh.md)

## Problem

The Web UI's previous Chat-aligned visual baseline was coherent but did not provide the warm, playful, icon-led presentation selected for the product. Applying that direction component by component without a shared vocabulary would scatter palette values, decorative assets, and motion rules across feature packages. Directly importing the reference library would also introduce a CC BY-NC 4.0 dependency into a project that does not limit its runtime to non-commercial use.

## Decision

DeepSeek Harness implements an independent island visual language through its existing theme and component packages. `ui-theme` owns warm brown text, cream surfaces, mint actions, pale green organic patterns, forest-green dark surfaces, five icon-tile roles, rounded geometry, soft elevation, and shallow 3D primary-action shadows. Feature packages consume those tokens through CSS Modules.

Existing controls and labeled function rows receive decorative icons on colored tiles with small transform-only hover motion. The visual layer does not add actions, replace accessible names, change event handlers, alter state ownership, or change RPC and session behavior. Code, terminal, and diff surfaces retain monospace typography and their existing overflow behavior.

The public [Animal Island UI design system](https://github.com/guokaigdg/animal-island-ui/tree/main/docs/design-system) informs the visual vocabulary. Its repository uses [CC BY-NC 4.0](https://github.com/guokaigdg/animal-island-ui/blob/main/LICENSE), so this implementation copies none of its source, font files, illustrations, role images, or other assets and adds no dependency on the library. Background ornament is generated with project-owned CSS gradients, and icons come from the existing DeepSeek Harness icon system.

The framework constraints in [the Web styling-system decision](2026-07-19-web-styling-system.md) remain authoritative. This decision supersedes only that note's Chat-aligned visual baseline.

## Verification

- `pnpm run build:lib:client`
- `pnpm run build:web`
- `pnpm exec vitest run packages/client/locale/tests packages/client/ui-agent-preset/tests packages/client/ui-permission-presets/tests packages/client/ui-model-selection/tests packages/client/ui-settings-general/tests packages/client/ui-theme/tests packages/client/ui-primitives/tests packages/client/ui-conversation/tests`
- `pnpm run doc-sync`
- Real-browser checks cover the populated conversation, empty-session hero, settings dialog, and dark theme. The accessibility tree retains the same controls and names.
- The GUI recording uses the real Web server and contains no fixture or mock UI.

## Alternatives considered

**Import Animal Island UI.** Rejected because its license prohibits commercial use and the existing plugin UI architecture does not need another component framework.

**Copy illustrations or role images.** Rejected because those assets are unnecessary for the selected visual language and would bring provenance and licensing obligations into the product.

**Add new icon-only controls.** Rejected because the request is visual-only. Existing controls provide enough semantic anchors for icon tiles without expanding the interaction surface.

**Style only the empty hero.** Rejected because a single themed illustration would conflict with unchanged navigation, settings, composer, and message chrome. The vocabulary must apply across the durable product surfaces.

## Consequences

The Web UI has one light/dark visual vocabulary without changing its functional composition. Shared palette or icon-role changes belong in `ui-theme`; feature packages must not introduce local palette literals. Product screenshots and visual checks must cover both theme families and include settings or another icon-rich surface. Future imagery must be project-owned or carry a license compatible with the intended distribution.
