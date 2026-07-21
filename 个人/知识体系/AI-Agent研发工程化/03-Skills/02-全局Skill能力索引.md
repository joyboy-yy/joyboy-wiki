---
title: 全局 Skill 能力索引
tags: [AI-Agent, Skills, OpenCode]
created: 2026-07-21
updated: 2026-07-21
status: evergreen
---

# 全局 Skill 能力索引

本页记录当前运行时公开的跨项目 Skills。Skill 负责条件判断和专项流程，不替代项目事实、原生文件工具或确定性的项目命令。

## 内容与发布

| Skill | 触发场景 | 不用于 |
|---|---|---|
| `baoyu-format-markdown` | 整理、格式化或美化 Markdown 文章 | 普通代码文件和小段文字修改 |
| `baoyu-markdown-to-html` | Markdown 转主题 HTML、微信 HTML 或渲染图表 | 只需保留 Markdown 的任务 |
| `baoyu-url-to-markdown` | 把网页、X、YouTube、Hacker News 等保存为 Markdown | 普通一次性网页事实查询 |

## Office 文档

| Skill | 触发场景 | 不用于 |
|---|---|---|
| `docx` | 创建、编辑、分析 Word，处理修订、批注和格式 | 纯文本或 Markdown 文档 |
| `pdf` | 提取、生成、拆分、合并、填写 PDF | 可直接读取的普通文本 |
| `pptx` | 创建、编辑、分析演示文稿及版式 | 普通文章或代码说明 |
| `xlsx` | Excel/CSV/TSV、公式、格式、分析和图表 | 无需电子表格能力的简单文本表格 |

## Agent 与工具工程

| Skill | 触发场景 | 不用于 |
|---|---|---|
| `playwright-cli` | 一次性浏览器导航、登录、交互、验收和探索 | 可维护 E2E 回归或纯网络诊断 |
| `writing-skills` | 创建、修改或验证 Skills | 普通项目文档 |
| `mcp-builder` | 设计或实现 MCP Server | 普通 API Client 或业务服务 |
| `customize-opencode` | 修改 OpenCode 配置、插件、Agent、Skill、MCP 或权限 | 用户应用代码和非 OpenCode 项目配置 |
| `grill-me` | 通过持续追问打磨计划、方案和设计 | 需求明确、应直接执行的任务 |

## 使用规则

- 先判断任务是否命中触发条件，再加载 Skill；不要把 Skill 当作固定启动清单。
- 同一任务只加载能够改变执行路径的 Skills。
- Skill 流程仍受项目规则、权限和用户指令约束。
- Office 和内容 Skills 只有处理对应文件格式时才加载。
- 一次性浏览器流程使用 `playwright-cli`；稳定回归使用项目 Playwright Test；运行时诊断使用 Chrome DevTools。
- 全局 Skill 不保存项目密码、主机地址、业务字典或项目静态架构。

## 项目 Skills

项目 Skills 不属于本索引，应记录在项目工程架构并根据项目入口发现。示例：[[工作/cssz/house-platform-backend/00-项目工程架构#Agent 工具层|house-platform-backend Agent 工具层]]。

## 相关主题

- [[01-Skill设计与触发治理|Skill 设计与触发治理]]
- [[../01-体系架构/03-全局工具能力地图|全局工具能力地图]]
- [[../05-开发工作流/03-工具选择路由|工具选择路由]]
