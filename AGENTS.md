# Agent instructions

This repository is `ThriftyStack/terraform-provider-unifi`. Provider schema docs stay in this repository. ThriftyStack operations docs live in Notion.

## Documentation in Notion

Notion is the source of truth for ThriftyStack docs. Notion replaced the ThriftyStack/docs GitHub repo. The migration point is commit `74b017f`. Do not edit that repo.

Read the relevant Notion page before you change behavior that the page describes. In the same task, update that page. If no page covers the change, add one under the matching section. On every edit, keep the page line that starts with `Last updated by`. If the page has no such line, add `Last updated by: <name>, <YYYY-MM-DD>` at the top.

Record a new decision as an ADR page under ADRs.

Never put secrets in Notion. Controller passwords, API keys, tokens, and private keys stay out of Notion pages.

### Pages for this repository

Read these pages before you change the matching behavior.

- [ThriftyStack Docs](https://www.notion.so/400972443c7081fd83efd3e8710fc9a6) is the root.
- [Systems](https://www.notion.so/400972443c7081658761c83b9fc2de16) is the section for system pages. Add a UniFi operations page here when this provider needs one.
- [CI](https://www.notion.so/400972443c7081b39966d2c0eb174498) covers CI. Read it before you change workflows, release, or checks.
- [ADRs](https://www.notion.so/400972443c708169b262e47f7c9c56e0) is the section for decision records.

Authentik, Vault, NetBird, Disaster Recovery, and Governance are linked from the root. Open the matching page when a change touches that subject.

### Notion MCP setup

The hosted server is `https://mcp.notion.com/mcp`. The project config names the server `notion` and stores no tokens. Each person completes the OAuth login once per tool. Share the ThriftyStack Docs root page with the Notion user who signs in.

#### Cursor

The project file is `.cursor/mcp.json`.

1. Open this repository in Cursor.
2. Open Customize in the sidebar.
3. Enable Notion.
4. Complete the OAuth login.
5. Confirm Notion stays enabled and lists its tools. When the connection fails, open the Output panel, select MCP Logs, and read the error.

#### Claude Code

The project file is `.mcp.json`. The entry uses `"type": "http"`. Claude Code skips a `url` entry that has no `type`.

1. Run `claude` in this repository and accept the workspace trust dialog.
2. Approve the `notion` server from `.mcp.json` when Claude Code asks.
3. Run `/mcp`, select `notion`, and complete the OAuth login. `claude mcp login notion` starts the same login from a shell.
4. Run `claude mcp list`. `Connected` means the login worked. `Needs authentication` means the login is still required. `Pending approval` means the project server is not approved yet.

Do not add a second `notion` server with `claude mcp add`. A second scope with the same name conflicts with this file.

#### Codex

The project file is `.codex/config.toml`. The server is `[mcp_servers.notion]`. Codex loads that file only after you trust the project.

1. Open this repository in Codex and trust the project.
2. Run `codex mcp login notion` and complete the OAuth login.
3. Run `codex mcp list`. `/mcp` in the Codex TUI shows the same server. The server still needs login when the list says it requires OAuth.

`codex mcp add` writes only `~/.codex/config.toml`. Do not use it for this server. The project file is the config.

## Provider code in this repository

Registry docs under `docs/`, examples under `examples/`, and `terraform-registry-manifest.json` stay in this repository. Do not move them to Notion.

Read `.github/copilot-instructions.md` before you change provider code. Read `.claude/timeouts.instructions.md` before you change timeouts.
