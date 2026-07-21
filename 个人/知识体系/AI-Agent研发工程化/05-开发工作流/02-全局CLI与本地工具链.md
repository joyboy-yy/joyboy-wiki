---
title: 全局 CLI 与本地工具链
tags: [AI-Agent, CLI, Windows, 工具链]
created: 2026-07-21
updated: 2026-07-21
status: evergreen
---

# 全局 CLI 与本地工具链

本页记录本机为 Agent 提供的命令能力和边界。绝对路径、环境变量和已验证版本以用户级 `ENVIRONMENT.md` 为准，不维护第二份易过期副本。

## 已验证工具

| 工具 | 主要用途 | 使用边界 |
|---|---|---|
| Java 17 | Java 应用编译和运行 | 项目 Java 版本仍以 POM/构建配置为准 |
| Maven | Java 依赖与生命周期 | 项目存在 Taskfile 时通过项目 `task` 调用 |
| Node.js / npm / npx | 前端与 Node 工具 | 项目存在 Taskfile 时通过项目任务调用 |
| Task | 项目统一构建、测试、运行、打包入口 | 执行前查看项目 `task -l` |
| Playwright CLI | 一次性浏览器自动化入口 | 使用前加载 `playwright-cli` Skill |
| Python | 脚本、数据处理和 Python MCP Server | 不替代简单文件工具或 Apply Patch |
| Git | 状态、diff、历史、提交和协作 | 未经明确要求不提交、不推送、不覆盖他人改动 |
| Git Bash | Windows 执行仓库 `.sh` 和 Bash 任务 | 使用 UTF-8 locale；不直接用 PowerShell 执行 `.sh` |
| PowerShell 7 | Windows 默认终端与系统操作 | 优先显式可执行路径，避免依赖不稳定 PATH |

## 调用优先级

```text
项目 Taskfile > 项目已有脚本 > 明确的全局 CLI > 临时拼装命令
```

项目任务封装参数、日志、跨平台处理和团队约定。直接调用底层 Maven/npm 可能绕过这些边界。

## 文件工具与终端

- 查找文件使用 Glob，不用终端遍历目录。
- 搜索内容使用 Grep，不用终端 grep/Select-String。
- 读取文件使用 Read，不用 Get-Content。
- 手工修改使用 Apply Patch，不用脚本或 shell 重写文件。
- Bash 用于 Git、Task、构建、测试、Docker 等终端操作。
- 多个独立命令并行执行，依赖命令按顺序执行。

## 维护与故障

- 显式工具路径失败时报告准确失败，不自动搜索替代安装。
- 缺失路径或环境变量时向用户确认，并立即验证路径和版本。
- 工具升级后先更新并验证 `ENVIRONMENT.md`；能力边界变化时再更新本页。
- 本页不记录私有 PATH、Token、代理地址和凭据。

## 相关主题

- [[../01-体系架构/03-全局工具能力地图|全局工具能力地图]]
- [[03-工具选择路由|工具选择路由]]
- [[01-Agent开发闭环|Agent 开发闭环]]
