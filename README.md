# MCP2skill

Turn MCP-backed tools into installable AI skills.

This repository currently contains one production-ready skill:

- `liepin-jobs`: Search jobs on Liepin, review resumes, update resume content, and apply to jobs with explicit user confirmation.

## Install

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

Runtime script:

```text
liepin-jobs/liepin_mcp.py
```

## Authentication

The `liepin-jobs` skill requires two Liepin tokens from the official Liepin MCP page:

- `LIEPIN_GATEWAY_TOKEN`
- `LIEPIN_USER_TOKEN`

The skill guides the user through setup and never assumes tokens already exist.

## Repository Goals

- keep skills lightweight and easy to install
- package MCP workflows as reusable agent skills
- make each skill publishable across major skill directories

## License

MIT
