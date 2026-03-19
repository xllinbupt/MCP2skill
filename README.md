# MCP2skill

Turn MCP-backed tools into installable AI skills.

This repository currently contains one production-ready skill:

- `liepin-jobs`: Search jobs on Liepin, review resumes, update resume content, and apply to jobs with explicit user confirmation.

It also includes a published MCP Registry manifest for the Liepin remote MCP server:

- `server.json`: official MCP Registry metadata for `io.github.xllinbupt/liepin-jobs`

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

Runtime script:

```text
liepin-jobs/liepin_mcp.py
```

MCP registry manifest:

```text
server.json
```

## Authentication

The `liepin-jobs` skill requires two Liepin tokens from the official Liepin MCP page:

- `LIEPIN_GATEWAY_TOKEN`
- `LIEPIN_USER_TOKEN`

The skill guides the user through setup and never assumes tokens already exist.

The remote MCP endpoint declared in `server.json` uses the same token pair through:

- `Authorization: Bearer <gateway_token>`
- `x-user-token: <user_token>`

## Repository Goals

- keep skills lightweight and easy to install
- package MCP workflows as reusable agent skills
- make each skill publishable across major skill directories

## License

MIT
