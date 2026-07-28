---
name: work-todo-triage
description: Use when adding, cleaning, or restructuring Chinese work todos in 工作/日志/YYYY-MM-DD.md, including 今日待办、Bug反馈、需求调整、接口问题、语义纠正、任务梳理、条目清洗.
---

# Work Todo Triage

## Overview

把零散的工作输入整理成今日工作日志里的可执行待办。目标是保留真实意图，纠正语义，拆清任务边界，去掉口语噪声和重复项。

## When To Use

Use this skill when the user provides any of these inputs:

- 测试、产品、前端、运营、同事提出的问题或反馈。
- 用户自己提出的问题、自测发现的问题、开发过程中发现的缺陷或优化点。
- Bug、接口异常、权限问题、页面问题、数据问题。
- 需求调整、优化点、技术方案想法、成本优化事项。
- 用户要求“整理到今日待办”“优化待办项”“语义纠正”“任务清洗”“条目清洗”。

Do not use this skill for long-form article formatting, generic markdown beautification, or non-work personal diaries.

## Target File

Default target is today's work log:

```text
工作/日志/YYYY-MM-DD.md
```

Use the current date from the runtime environment. If the user gives an explicit date or file path, use that instead.

If the file does not exist, create it with this structure:

```markdown
# YYYY-MM-DD

## 工作记录

-

## 待办


## 复盘

-
```

## Triage Rules

Convert raw input into clear tasks using these rules:

| Raw input type | Output shape |
|---|---|
| 问题反馈 | `修复/排查 + 对象 + 异常表现` |
| 产品需求 | `设计/实现 + 功能 + 管理端/客户端边界` |
| 前端问题 | `补齐/调整 + 接口/字段/权限 + 使用场景` |
| 测试问题 | `复现并修复 + 模块 + 失败条件` |
| 技术想法 | `评估/设计 + 技术方案 + 目标收益` |
| 成本问题 | `评估/优化 + 成本项 + 可选方案` |

Prefer verbs that make the task executable:

- `排查`
- `修复`
- `设计`
- `实现`
- `优化`
- `补齐`
- `评估`
- `确认`

## Cleanup Rules

- Normalize terms: `App`、`Admin`、`PC`、`C 端`、`接口`、`房源`、`机构`.
- Keep product names, route paths, API paths, error messages, table names, and enum values exactly as provided.
- Remove filler words such as “好像”“是不是”“然后”“晚上后开发” unless they encode a real uncertainty or dependency.
- Preserve uncertainty as an action: change “是不是要加配置？” to “确认是否需要加入配置”。
- Split one line into multiple tasks when it contains different modules, platforms, or acceptance conditions.
- Merge duplicates only when the object and desired outcome are the same.
- Do not invent business facts, owners, deadlines, API names, or implementation details.
- If the user explicitly limits fields, preserve that field whitelist exactly. Do not add inferred fields such as phone, ID card, institution, status, or permissions unless the user provided them.
- If an equivalent todo already exists, do not add a duplicate. If the new input adds missing constraints, update the existing item or its note instead.
- Treat two todos as duplicates when module, object, and desired outcome match, even if wording differs.

## Grouping

When adding multiple items, group under `## 待办` with `###` headings. Use these headings when they fit:

- `需求设计`
- `Admin 功能`
- `App 功能`
- `PC 功能`
- `接口与数据`
- `机构与权限`
- `问题修复`
- `需求确认`
- `技术治理`
- `成本优化`

If there are only one or two tasks, adding them directly under `## 待办` is acceptable.

## Output Contract

Each actionable task should be a checkbox:

```markdown
- [ ] 动词 + 对象 + 目标/验收点。
```

Examples:

```markdown
- [ ] 设计 App 端接口使用情况统计方案，并支持 Admin 端管理统计配置和数据。
- [ ] 修复个人房源详情访问异常：`无权限访问：无权查看该房源`。
- [ ] 确认 `/**`、`/webjars/**` 是否需要加入接口统计排除配置。
```

Use an Obsidian callout for larger context that should not become multiple checkboxes:

```markdown
> [!NOTE] OCR 成本优化：二代身份证识别
> 当前问题：...
>
> 可选方案：
> - `方案 A`：...
> - `方案 B`：...
```

- Use checkboxes for executable work only.
- Put field mappings, return field limits, display rules, and acceptance notes into a callout unless they are separate implementation tasks.

## Workflow

1. Read the target work log if it exists.
2. Identify existing tasks and avoid duplicates.
3. Classify incoming items by domain and intent.
4. Rewrite each item into executable wording.
5. Insert under the best `###` heading inside `## 待办`.
6. Keep `## 工作记录` and `## 复盘` intact unless the user explicitly asks to edit them.
7. Report a concise summary of what was added or cleaned.

If the user says “新增待办”, “加入待办”, or “记录到待办”, only update `## 待办`; do not add `## 工作记录` entries unless explicitly requested.

## Common Mistakes

| Mistake | Correction |
|---|---|
| Copying raw chat text directly | Rewrite into executable tasks |
| Turning every detail into a checkbox | Put context in notes/callouts |
| Losing uncertainty | Convert uncertainty into `确认/评估` tasks |
| Mixing platforms | Split Admin, App, PC, C 端 work when outcomes differ |
| Re-adding ignored work files to Git | Keep `工作/` local-only unless user explicitly changes Git policy |

## Git Boundary

In this vault, `工作/` is local-only and ignored by Git. Do not stage, commit, or push work logs unless the user explicitly asks to change that policy.
