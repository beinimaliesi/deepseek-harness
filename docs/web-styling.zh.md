# Web UI 样式参考

[English](web-styling.md) | 中文

本文规定浏览器客户端包的样式职责归属与组件规则。当前 token 值位于 [`packages/client/ui-theme/src/styles/`](../packages/client/ui-theme/src/styles/)；本文不重复这份由源码生成的清单。

## 职责归属

[`ui-theme`](../packages/client/ui-theme/README.md) 负责 `--dsw-*` 静态色阶、语义别名、具名产品专用颜色、排版、动效、渐变、阴影、滚动条样式以及明暗主题偏好。[`ui-layout`](../packages/client/ui-layout/README.md) 将解析后的主题快照应用到文档。功能包使用主题所有的语义或产品专用 token，不得另行定义全局主题。

全局样式表归 `ui-theme/src/styles/` 所有。组件样式以 CSS Modules 形式放在组件旁。当某个值属于该组件的布局或呈现约定时，组件可以定义局部自定义属性；共享颜色、排版、层级和动效属于主题包。

## 视觉语言

Web UI 使用项目自有的岛屿视觉语言：暖棕文字、奶油色表面、薄荷绿主操作、淡绿色纹理背景、圆润控件、柔和层级，以及主操作上的浅 3D 厚度。深色主题将同一组角色映射为森林绿表面与奶油色文字。代码、终端和 diff 内容继续采用产品所需的等宽字体。

现有控件与带标签的功能行可以获得图标，并放在薄荷、阳光黄、珊瑚、天空蓝或丁香紫的小色块上。图标色块仅作装饰：不得创建新操作、替换控件的无障碍名称或改变其事件处理器。悬停动效保持轻微，仅使用 transform，并由 Web 壳的共享减少动态效果规则关闭。

这套视觉词汇参考了公开的 [Animal Island UI 设计系统](https://github.com/guokaigdg/animal-island-ui/tree/main/docs/design-system)，其仓库使用 [CC BY-NC 4.0](https://github.com/guokaigdg/animal-island-ui/blob/main/LICENSE) 许可。DeepSeek Harness 不复制其源码、字体文件、插画或其他资产，也不依赖该组件库。主题值、CSS 纹理、图标色块和动效均基于项目现有组件与图标系统在本地实现。

## 组件规则

- 使用 CSS Modules 和 `clsx`；不得添加组件库或 Tailwind。
- 功能组件使用 `--dsw-alias-*` 语义 token 或主题所有的 `--dsw-specific-*` 产品 token。不得复制静态色板值或在其中写入颜色字面量。
- 功能组件 CSS 不得包含主题选择器。明暗主题覆盖属于主题所有方。
- 字体大小必须与行高配对；已有角色匹配时使用主题排版变量。
- 当组件约定要求保留列结构时，源码文本、终端输出和 diff 行不得换行；使用共享滚动条样式，不得定义组件专用滚动条选择器。
- 呈现规则写在 CSS 中。React 内联样式可以传递组件局部自定义属性值，但不得编码主题分支。
- 添加过渡动画或仅悬停可见的控件时，保留清晰可见的键盘焦点和减少动态效果行为。

## 变更系统

在所属 `ui-theme` 样式表中添加或修改共享 token，然后在功能包中使用其语义别名或具名产品专用 token。公共样式约定发生变化时，更新所属包的参考文档。视觉行为遵循[测试策略](testing.md)；[样式系统 Agent Note](../.agents/notes/implemented/process/2026-07-19-web-styling-system.md) 记录框架依据，[岛屿视觉语言 Agent Note](../.agents/notes/implemented/process/2026-08-14-island-web-visual-language.md) 记录当前视觉基线。
