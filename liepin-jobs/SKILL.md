---
name: liepin-jobs
description: Use when Liepin (猎聘) workflows need the CLI—missing or expired token, unauthorized responses, first-time setup, resume fetch/update, job search or apply, choosing job-kind from search results, machine-readable JSON for parsing, or summarizing user-facing `liepin-cli` help without advanced flags.
  触发词: 找工作, 搜职位, 投简历, 猎聘, liepin, 求职, 招聘, 简历
version: 0.3.0
author: xllin
license: MIT
homepage: https://github.com/xllinbupt/MCP2skill
repository: https://github.com/xllinbupt/MCP2skill
keywords:
  - jobs
  - liepin
  - resume
  - cli
  - chinese
requires:
  bins: liepin-cli
allowed-tools: Bash(liepin-cli:*)
---

# liepin-cli

## Overview
`liepin-cli` 是猎聘简历查询与更新、职位搜索与投递的本地 CLI 工具。优先使用已安装的 `liepin-cli` 命令，而非手写 HTTP 请求。

## When to Use
- 运行 `liepin-cli`
- 管理猎聘 token 配置、刷新或状态查看
- 获取或更新简历数据
- 搜索职位或投递职位

Do not use this skill for unrelated non-Liepin tasks.

## 安装 CLI（首次使用必须）

若尚未安装 `liepin-cli`，请先从 [liepin-tech-2026/liepin-cil](https://github.com/liepin-tech-2026/liepin-cil) 安装：

```bash
# 方式一 — pip + 虚拟环境
python -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"

# 方式二 — uv
git clone https://github.com/liepin-tech-2026/liepin-cil.git
cd liepin-cil && uv sync
```

安装完成后验证：`liepin-cli --help`

## Core Rules
- 优先使用已安装的 `liepin-cli` 命令。
- **首次向用户说明帮助时**：不提 `--token`、`--input`、`--base-url`、`--timeout`、`--output`、`--help`，除非用户明确要求完整/高级帮助。
- **执行命令时**：按下方 Command Map 操作；需要机器可读结果时使用 `--output json`；仅需人类可读输出时省略 `--output json`。
- token 过期时，引导用户先执行 `liepin-cli auth open`，再执行 `liepin-cli auth setup`。
- `job apply --job-kind` 必须复用搜索结果中的类型编码，禁止猜测标签。
- 不要假设 README 示例 payload 文件在本地已存在。

## Command Map

| Intent | Preferred command |
|------|------|
| 获取当前简历 | `liepin-cli resume get --output json` |
| 搜索职位 | `liepin-cli job search ... --output json` |
| 投递职位 | `liepin-cli job apply --job-id <id> --job-kind <kind> --output json` |
| 首次 token 配置 | `liepin-cli setup` |
| Auth 管理 | `liepin-cli auth setup/status/open/clear` |

## 典型求职流程

当用户说"帮我找工作"、"搜一下猎聘上的 XX 职位"时，按以下步骤执行：

1. **检查 Token** → 未配置则引导 `liepin-cli setup`
2. **查看简历** (`liepin-cli resume get`) → 确认简历完整，提醒补充缺失项
3. **搜索职位** (`liepin-cli job search`) → 根据意向搜索，用表格展示结果
4. **分析匹配度** → 结合简历与职位要求，帮用户筛选
5. **投递职位** (`liepin-cli job apply`) → **必须先向用户展示职位详情并获得明确确认后再投递**

## Help Summary Defaults
- 根命令帮助：`setup`、`auth`、`resume`、`job`
- `auth --help`：`status`、`clear`、`open`、`setup`
- `resume --help`：用途说明 + 子命令概览
- `job --help`：`search`、`apply`
- `job apply --help`：`--job-id`、`--job-kind`

## Common Mistakes
- 在首次帮助回答中暴露隐藏/内部 flag
- 猜测 `jobKind` 而不复用搜索结果
- 把 README payload 示例路径当作已存在的文件
- 一次性倾倒全部简历字段，而不是优先摘要最有用的业务字段

## Reference
详见 [reference.md](reference.md)，包含安装上下文、命令表、auth 恢复步骤、`--input` / `--output` 说明。
