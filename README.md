# MCP2skill

Turn MCP-backed tools into installable AI skills.

This repository contains one production-ready skill:

- `liepin-jobs`: Search jobs on Liepin, review and update resumes, and apply to jobs with explicit user confirmation — powered by the [`liepin-cli`](https://github.com/liepin-tech-2026/liepin-cil) local CLI tool.

It also includes a published MCP Registry manifest for the Liepin remote MCP server:

- `server.json`: official MCP Registry metadata for `io.github.xllinbupt/liepin-jobs`

## Prerequisite: Install `liepin-cli`

This skill wraps the [`liepin-cli`](https://github.com/liepin-tech-2026/liepin-cil) CLI tool. Install it first:

```bash
# Option A — pip + venv
python -m venv .venv && source .venv/bin/activate
pip install -e ".[dev]"   # run inside the liepin-cil clone

# Option B — uv
git clone https://github.com/liepin-tech-2026/liepin-cil.git
cd liepin-cil && uv sync
```

Verify: `liepin-cli --help`

## Install the Skill

### skills.sh

```bash
npx skills add https://github.com/xllinbupt/MCP2skill --skill liepin-jobs
```

### Playbooks

```bash
npx playbooks add skill xllinbupt/MCP2skill --skill liepin-jobs
```

### Claude Code marketplace or plugin source

This repository includes `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` so it can be used as a Claude Code plugin source or included in a custom marketplace.

### Official MCP Registry

The Liepin MCP server metadata from this repository has been published to the official MCP Registry under:

```text
io.github.xllinbupt/liepin-jobs
```

You can look it up via:

```bash
curl "https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.xllinbupt/liepin-jobs"
```

## Skill

### `liepin-jobs`

Use this skill when the user wants to:

- search jobs on Liepin
- inspect or improve their Liepin resume
- apply to a role on Liepin
- manage job preferences on Liepin

Skill path:

```text
liepin-jobs/SKILL.md
```

Reference:

```text
liepin-jobs/reference.md
```

MCP registry manifest:

```text
server.json
```

## Authentication

The `liepin-jobs` skill requires one Liepin token obtained from the official Liepin MCP page (`https://www.liepin.com/mcp/server`).

Token resolution priority: `--token` flag > `LIEPIN_USER_TOKEN` env var > `~/.config/liepin-cli/config.json`

Run the setup flow to save the token locally:

```bash
liepin-cli setup
# or
liepin-cli auth setup
```

If token expires: `liepin-cli auth open` → `liepin-cli auth setup`

The remote MCP endpoint declared in `server.json` uses the same token through:

- `x-user-token: <user_token>`

## Distribution

This skill has been published, submitted, or prepared for distribution on the following platforms.

### Already Live

| Platform | Status | Link |
|----------|--------|------|
| **ClawHub (OpenClaw)** | Published | Public listing URL pending |
| **Official MCP Registry** | Live | https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.xllinbupt/liepin-jobs |
| **GitHub** | Live | https://github.com/xllinbupt/MCP2skill |

### PR Submitted

| Platform | PR |
|----------|-----|
| **skills-hub.cc** | [qufei1993/skills-hub#36](https://github.com/qufei1993/skills-hub/pull/36) |
| **TerminalSkills.io** | [TerminalSkills/skills#471](https://github.com/TerminalSkills/skills/pull/471) |
| **alirezarezvani/claude-skills** | [#384](https://github.com/alirezarezvani/claude-skills/pull/384) |
| **travisvn/awesome-claude-skills** | [#329](https://github.com/travisvn/awesome-claude-skills/pull/329) |
| **BehiSecc/awesome-claude-skills** | [#132](https://github.com/BehiSecc/awesome-claude-skills/pull/132) |
| **VoltAgent/awesome-agent-skills** | [#247](https://github.com/VoltAgent/awesome-agent-skills/pull/247) |

### Auto-indexing / Crawler-based Platforms

| Platform | Status |
|----------|--------|
| **SkillHub** (skillhub.club) | Waiting for crawler/index sync |
| **LobeHub Skills** (lobehub.com/skills) | Waiting for crawler/index sync |
| **claudemarketplaces.com** | Repository has `.claude-plugin/` metadata |
| **SkillsMP** (skillsmp.com) | Waiting for sync from the GitHub repository |

## Repository Goals

- keep skills lightweight and easy to install
- package CLI workflows as reusable agent skills
- make each skill publishable across major skill directories

## License

MIT
