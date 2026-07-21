---
title: Skill 设计与触发治理
tags:
  - AI-Agent
  - Skills
  - 工作流
created: 2026-07-21
status: evergreen
---

# Skill 设计与触发治理

Skill 适合承载“在什么条件下，采用什么判断流程”，不适合保存项目稳定事实或纯命令参考。

## 何时创建 Skill

- 同一判断在多个任务中重复出现。
- Agent 经常在工具选择、测试范围或排障顺序上犯错。
- 流程包含条件分支，不能简单用脚本替代。
- 需要跨 OpenCode、Codex、Claude Code 复用。

不适合创建 Skill 的情况：一次性任务、标准语法参考、可由 lint/脚本强制的规则、只属于某项目的静态事实。

## 触发描述

Skill 的 `description` 只描述触发条件，不概括全部流程：

```yaml
---
name: testing-orchestration
description: Use when implementing or completing code, API, SQL, configuration, frontend, bug-fix, refactor, release changes, or when users ask for 测试、验证、回归、发版检查.
---
```

## 设计原则

- 名称使用小写连字符，职责单一。
- 触发关键词覆盖中英文实际表达。
- 主体先给目标，再给决策流程和升级门禁。
- 可选工具必须有“何时不使用”的反向条件。
- 工具不存在时提供回退路径。
- 不把敏感配置和项目密码写入 Skill。

## 防止重复触发

- 每个 Skill 目录只保留一个 `SKILL.md` 加载入口。
- 中文镜像使用 `SKILL.zh-CN.md`，不会被扫描为第二个 Skill。
- 两个 Skill 的触发范围不要大面积重叠；上层编排 Skill 应明确是否委托下层 Skill。
- 团队入口文件不复制 Skill 的触发词列表。

## Skill 验证

1. 在没有 Skill 的情况下运行典型场景，记录错误决策。
2. 编写最小 Skill，只修复已观察到的问题。
3. 用纯后端、API、前端、数据库等不同场景验证。
4. 检查是否过度调用工具或无条件扩大测试。
5. 修改触发描述后重新验证隐式匹配。

## 生命周期

```text
个人试验 -> 多场景验证 -> 去除本机耦合 -> 团队评审 -> 团队 Skill / 插件
```
