# CLAUDE.md

本文件为 Claude Code（claude.ai/code）在此代码库中工作时提供指引。

## 项目概述

这是一个单文件中文待办事项应用，所有 HTML、CSS 和 JavaScript 均位于 [index.html](index.html) 中。无需构建步骤，无依赖，无包管理器。

运行方式：直接在浏览器中打开 `index.html`，或使用任意静态文件服务器（如 `python3 -m http.server`）。

## 架构

所有代码集中在一个文件中：
- **CSS**（第 7–209 行）：内联 `<style>` 块；移动优先布局，最大宽度 393px
- **HTML**（第 211–230 行）：筛选标签页、输入行、任务列表 `<ul id="list">`、底部信息栏
- **JS**（第 232–332 行）：原生 ES6，无框架

状态为单一 `tasks` 数组（`[{ id, text, done }]`），以 `tasks` 为键持久化到 `localStorage`。所有变更遵循统一模式：修改数组 → `save()` → `render()`。

`render()` 每次通过 `innerHTML` 重建整个列表。ID 为 `Date.now()` 整数，HTML 转义由 `escHtml()` 手动处理。

## MCP 集成

Figma MCP 服务器已在 [.mcp.json](.mcp.json) 中配置（HTTP 传输，地址为 `https://mcp.figma.com/mcp`）。处理 Figma 设计时使用 `get_design_context`。该工具的权限已在 [.claude/settings.local.json](.claude/settings.local.json) 中预先放行。