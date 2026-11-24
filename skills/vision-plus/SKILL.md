---
name: vision-plus
description: >-
  Generate restrained, theme-adaptive native SVG/Canvas architecture diagrams,
  comparison matrices, data charts, and interactive tabs/accordions without
  external CDNs. Use when the user mentions "Vision+", "高级可视化", or asks
  for structured diagrams, dashboards, or interactive visual explanations.
---

# Vision+ 高级可视化指南

当用户提及 `Vision+`、`高级可视化`，或需要将复杂架构、状态流转、多维对比与数据趋势以高信息密度呈现时，严格按本技能构建可视化画布。

## 1. 宿主通道自动路由

1. **T3 Code（具备 `html_preview` / `html_render`）**
   - 编写自包含 HTML（内联 `<style>` 与 `<script>`，零外部 CDN）。
   - 先调用 `html_preview` 检查排版、换行与实际 `contentHeight`，再调用 `html_render` 传入准确高度。
   - 不在 `html`、`body` 或最外层容器设置背景色、外框或大标题栏。
2. **Antigravity App（具备 `generative_ui` 与 `<agent-embed>`）**
   - 在 Artifact 目录生成自包含 `.html` 文件（`UserFacing: true, RequestFeedback: false`）。
   - 通过 `<agent-embed src="file:///..."></agent-embed>` 无缝穿插于正文流；顶部右侧预留至少 `48px` 安全区（`pr-12`），避免可点击控件被右上角悬浮按钮遮挡。
3. **无画布环境（纯 CLI / 文本终端）**
   - 降级为紧凑 Markdown 表格、列表或 Mermaid 图，禁止输出裸 `<div style="...">`。

## 2. 视觉与交互红线

- **色阶与克制**：默认黑白灰中性色阶，依靠 `1px` 细线、间距与留白建立层次；**禁用彩色渐变**与纯装饰性插画。
- **语义色**：仅在关键状态、路径焦点或结论指标上克制使用宿主变量 `--primary`、`--success`、`--warning`、`--destructive`（或 `--error`）。
- **深浅色自适应**：严格消费宿主 `:root` CSS 变量（`--foreground`、`--muted-foreground`、`--card`、`--border`/`--card-border`、`--secondary`、`--background`、`--radius`、`--font-sans`、`--font-mono`）；禁止硬编码页面背景色或在 `:root` 覆写本地色值。
- **原生矢量与图表**：逻辑图、流程图、状态机、树状层级与数据图表全部使用原生 `<svg>` 或 `<canvas>` 实现，不引入任何第三方外部 CDN。
- **紧凑边界**：内嵌画布目标高度 `≤ 450px`，禁止顶层使用 `100vh` / `height: 100%`；长内容使用轻量交互 Tab 或 `<details>` 折叠面板收拢，避免内部滚动条。
- **图文互补**：画布与 Markdown 正文分工明确，正文不再重复复述画布中已经展示的节点与数据。

## 3. 交付前自检

- 检查文本在 728px 与窄屏下是否出现异常断字或溢出。
- 检查 SVG 箭头的 `marker`、坐标与字号是否清晰对齐且在浅/深色模式下均具备足够对比度。
- 检查所有交互控件（Tab 切换、模式分段按钮、`<details>`）切换后内容高度不会超出画布产生裁切。
