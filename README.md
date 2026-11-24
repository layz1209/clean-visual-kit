# Clean Visual Kit

一套面向 AI Coding Agent 的**高信息密度中文输出与多端自适应可视化插件**，同时兼容 **Antigravity（App / CLI / IDE）**、**T3 Code**、**Claude Code** 与 **Codex**。

## 核心能力

- **紧凑中文输出规范**：统一 `##` / `###` 标题层级、高信息密度中文行文、可运行代码块标注与必要注释。
- **宿主通道自动路由**：
  - **T3 Code**：自动走 `html_preview → html_render` 自包含画布。
  - **Antigravity App**：自动走 `generative_ui` + `<agent-embed>` 正文穿插画布（含右上角 `pr-12` 安全区约束）。
  - **纯终端 / 无画布客户端**：自动降级为紧凑 Markdown 表格、列表或 Mermaid 图，避免输出被剥离样式的裸 `<div style="...">`。
- **克制黑白灰视觉体系**：默认中性灰阶 + `1px` 细线与留白建立层次，禁用彩色渐变，严格消费宿主 CSS 变量实现深浅色自适应。
- **内置 `vision-plus` Skill**：提及 `Vision+` 或「高级可视化」时触发，使用原生 SVG / Canvas 与轻量交互（标签页、折叠面板）绘制架构图、状态机、对比矩阵与数据图表，零第三方 CDN 依赖。

## 仓库结构

```text
clean-visual-kit/
├── .antigravity-plugin/plugin.json   # Antigravity 官方插件清单
├── .claude-plugin/
│   ├── plugin.json                   # Claude Code 插件清单
│   └── marketplace.json              # Claude Code Marketplace 索引
├── assets/logo.svg                   # 1:1 矢量图标（适配浅/深色主题）
├── rules/AGENTS.md                   # Antigravity 常驻输出与可视化规则
├── skills/vision-plus/SKILL.md       # Vision+ 高级可视化按需技能
├── AGENTS.md                         # Codex / Cursor / 通用项目规则入口
└── LICENSE                           # MIT
```

## 安装方式

### Antigravity CLI / App

```bash
# 本地目录或克隆后校验并安装
agy plugin validate ./clean-visual-kit
agy plugin install ./clean-visual-kit
```

也可直接将本仓库目录放入全局插件目录 `~/.gemini/config/plugins/clean-visual-kit/`。

### Claude Code

```text
/plugin marketplace add layz1209/clean-visual-kit
/plugin install clean-visual-kit@clean-visual-kit
```

### Codex / 通用 Agent

- 将根目录的 `AGENTS.md` 合并至全局 `~/.codex/AGENTS.md` 或项目根目录。
- 将 `skills/vision-plus/` 复制到 `~/.codex/skills/vision-plus/`。

## License

MIT
