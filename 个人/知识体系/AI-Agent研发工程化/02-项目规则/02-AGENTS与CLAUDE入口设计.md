---
title: AGENTS 与 CLAUDE 入口设计
tags:
  - AGENTS
  - Claude-Code
  - 上下文管理
created: 2026-07-21
status: evergreen
---

# AGENTS 与 CLAUDE 入口设计

`AGENTS.md` 面向 OpenCode、Codex 等客户端，`CLAUDE.md` 面向 Claude Code。它们是兼容入口，不是两套独立规则。

## 最小结构

```markdown
# Repository Instructions

## Always On
- 当前源码和清单优先
- 统一项目命令入口
- 提交、安全和本地文件边界

## Read By Change
| 变更类型 | 必读文档 |

## Completion
- 最小验证
- 真实报告
- 剩余风险
```

## 应自动加载的内容

- 不读取其他文档就可能造成破坏的规则。
- 告诉 Agent 按什么条件读取哪份文档。
- 命令入口、安全、提交和验证真实性。
- 项目中特别反常的约束，例如测试目录禁止提交。

## 不应自动加载的内容

- 所有 task 命令及参数。
- 详细 Java/前端编码规范。
- 完整测试矩阵。
- MCP 工具说明、账号和本机路径。
- 只在少数场景使用的排障手册。

## 镜像策略

- 英文 `AGENTS.md` 与 `CLAUDE.md` 保持等价。
- 中文镜像保持章节和语义一致，但不作为额外触发入口。
- 每次只编辑一个主版本，再同步复制或翻译。
- 不使用同名 Skill 的多个 `SKILL.md` 作为语言镜像，否则可能重复发现。

## 预算建议

- 根入口控制在 30–40 行。
- 只保留 3–5 条始终生效规则。
- 条件阅读表优于长篇调查顺序。
- 每个规则应能回答“如果删除，最坏后果是什么”。
