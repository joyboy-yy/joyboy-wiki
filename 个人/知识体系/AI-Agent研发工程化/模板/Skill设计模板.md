---
title: Skill 设计模板
tags:
  - AI-Agent
  - Skills
  - Template
created: 2026-07-21
---

# Skill 设计模板

## Frontmatter

```yaml
---
name: skill-name
description: Use when [具体触发条件、症状、任务类型和中英文关键词].
---
```

## Goal

一句话说明 Skill 要稳定解决的判断问题。

## Trigger Boundary

### 使用

-

### 不使用

-

## Required Inputs

- 当前 diff：
- 项目规则：
- 运行环境：
- 可选工具：

## Decision Flow

1.
2.
3.

## Tool Gates

| 工具 | 使用条件 | 不使用条件 | 回退方案 |
|---|---|---|---|
|  |  |  |  |

## Output Contract

- 决策：
- 执行动作：
- 证据：
- 剩余风险：

## Failure Scenarios

| 场景 | 无 Skill 的错误行为 | 期望行为 |
|---|---|---|
|  |  |  |

## Verification

- [ ] 已运行无 Skill 基线场景
- [ ] 已运行纯后端场景
- [ ] 已运行 API/数据库边界场景
- [ ] 已运行前端/浏览器场景
- [ ] 工具不可用时能回退
- [ ] 不会无条件运行全套工具
- [ ] 中文镜像与主文件同步
