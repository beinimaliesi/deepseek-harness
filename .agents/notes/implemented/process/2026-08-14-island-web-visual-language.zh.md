# Agent Note：Web UI 的项目自有岛屿视觉语言

Status: implemented

[English](2026-08-14-island-web-visual-language.md) | 中文

## 问题

Web UI 原有的 Chat 对齐视觉基线保持了一致性，但无法提供产品选定的温暖、轻松和图标主导的呈现方式。如果没有共享视觉词汇而逐个组件实施这一方向，色板值、装饰资产和动效规则会散落到各功能包。直接引入参考组件库还会把 CC BY-NC 4.0 依赖带入一个未将运行场景限制为非商业用途的项目。

## 决策

DeepSeek Harness 通过现有主题包与组件包独立实现岛屿视觉语言。`ui-theme` 负责暖棕文字、奶油色表面、薄荷绿操作、淡绿色有机纹理、森林绿深色表面、五种图标色块角色、圆润几何、柔和层级与主操作的浅 3D 阴影。功能包通过 CSS Modules 使用这些 token。

现有控件与带标签的功能行获得装饰性图标、彩色色块和仅使用 transform 的轻微悬停动效。视觉层不增加操作，不替换无障碍名称，不改变事件处理器、状态职责、RPC 或会话行为。代码、终端与 diff 表面继续使用等宽排版及原有溢出行为。

公开的 [Animal Island UI 设计系统](https://github.com/guokaigdg/animal-island-ui/tree/main/docs/design-system)为视觉词汇提供参考。其仓库使用 [CC BY-NC 4.0](https://github.com/guokaigdg/animal-island-ui/blob/main/LICENSE)，因此本实现不复制其源码、字体文件、插画、角色图片或其他资产，也不增加对该组件库的依赖。背景装饰由项目自有 CSS 渐变生成，图标来自 DeepSeek Harness 现有图标系统。

[Web 样式系统决策](2026-07-19-web-styling-system.md)中的框架约束继续作为权威。本决策仅取代其中的 Chat 对齐视觉基线。

## 验证

- `pnpm run build:lib:client`
- `pnpm run build:web`
- `pnpm exec vitest run packages/client/locale/tests packages/client/ui-agent-preset/tests packages/client/ui-permission-presets/tests packages/client/ui-model-selection/tests packages/client/ui-settings-general/tests packages/client/ui-theme/tests packages/client/ui-primitives/tests packages/client/ui-conversation/tests`
- `pnpm run doc-sync`
- 真实浏览器检查覆盖已填充的对话、新会话空状态、设置弹窗与深色主题。无障碍树保留相同的控件和名称。
- GUI 录制使用真实 Web server，不包含 fixture 或模拟 UI。

## 考虑过的替代方案

**引入 Animal Island UI。** 否决，因为其许可禁止商业使用，而且现有插件化 UI 架构不需要另一个组件框架。

**复制插画或角色图片。** 否决，因为实现所选视觉语言不需要这些资产，而且这会给产品引入来源与许可义务。

**增加新的纯图标控件。** 否决，因为需求仅涉及视觉。现有控件已经提供足够的语义锚点，可以添加图标色块而无需扩展交互面。

**只修改空状态主视觉。** 否决，因为单个主题插画会与未调整的导航、设置、输入区和消息操作区冲突。视觉词汇必须覆盖持久的产品表面。

## 后果

Web UI 在不改变功能组合的前提下获得一套统一的明暗视觉词汇。共享色板或图标角色的变更属于 `ui-theme`；功能包不得引入局部色板字面量。产品截图与视觉检查必须覆盖两类主题，并包含设置或其他图标丰富的表面。后续图像必须由项目所有，或采用与预期分发方式兼容的许可。
