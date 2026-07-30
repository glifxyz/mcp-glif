<p align="center">
  <img src="assets/glif-icon-400.png" width="120" alt="Glif" />
</p>

# Glif MCP Server

**Glif** is a media-generation agent: generate images, video, and audio, transcribe, render HTML, search the web, run code, and chain multi-step media operations — from any MCP client.

- **Endpoint:** `https://glif.app/api/mcp` (Streamable HTTP, JSON-RPC 2.0)
- **Auth:** OAuth 2.1 with dynamic client registration — sign in with your Glif account, no API keys
- **Install page with one-click buttons:** https://glif.app/mcp
- **Docs for agents:** https://glif.app/llms.txt

This repo holds the registry metadata for the hosted server (see [`server.json`](server.json)); the server itself is part of the glif.app platform and is not open source.

> [!NOTE]
> Looking for the old locally-run stdio server (npm `@glifxyz/glif-mcp-server`)? It's deprecated — the code is parked on the [`legacy-local-server`](https://github.com/glifxyz/glif-mcp-server/tree/legacy-local-server) branch.

## Tools

| Tool                                  | What it does                                                                                                                                                           |
| ------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `compose_project`                     | Create or continue a Glif project from a plain-language prompt. Glif picks the models and chains the steps itself. Returns a `job_id` immediately while the work runs. |
| `get_job_status`                      | Poll a `compose_project` job; the completed poll carries the generated media.                                                                                          |
| `get_project`                         | Project state, active job, recent messages, and assets.                                                                                                                |
| `view_media`                          | Re-render already-generated media in the media viewer.                                                                                                                 |
| `list_projects`                       | Recent projects owned by the caller.                                                                                                                                   |
| `upload_file`                         | Upload an image, video, or audio file (URL or base64) for use as an input.                                                                                             |
| `list_user_skills` / `get_user_skill` | The caller's own saved skills.                                                                                                                                         |
| `whoami`                              | The signed-in account and its remaining credits.                                                                                                                       |

Generated media comes back as `resource_link` blocks pointing at CDN URLs. Most work is one `compose_project` call — describe the whole thing, including a series of variations, in a single prompt rather than looping.

Generation spends credits from the signed-in Glif account; read-only tools are free. See https://glif.app/pricing.

## Install

### Claude (web / desktop)

Settings → Connectors → **Add custom connector**, paste:

```
https://glif.app/api/mcp
```

### Claude Code

```sh
claude mcp add --scope user --transport http glif "https://glif.app/api/mcp"
```

### Cursor

[![Add to Cursor](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=glif&config=eyJ1cmwiOiJodHRwczovL2dsaWYuYXBwL2FwaS9tY3AifQ%3D%3D)

Or add to `.cursor/mcp.json`:

```json
{ "mcpServers": { "glif": { "url": "https://glif.app/api/mcp" } } }
```

### VS Code

```sh
code --add-mcp '{"name":"glif","type":"http","url":"https://glif.app/api/mcp"}'
```

### ChatGPT

Enable developer mode, then Settings → Apps & Connectors → **Add new connector**, paste `https://glif.app/api/mcp`, pick OAuth.

### Codex

```sh
codex mcp add glif --url "https://glif.app/api/mcp"
codex mcp login glif
```

### Any other MCP client

```json
{ "mcpServers": { "glif": { "url": "https://glif.app/api/mcp", "transport": "http" } } }
```

Your client opens a browser OAuth sign-in on first connect — approve it to link your Glif account. More clients (Replit, Hermes, OpenClaw, LM Studio, …) with copy-paste snippets: https://glif.app/mcp

## Links

- Website: https://glif.app
- MCP install page: https://glif.app/mcp
- Discord: https://discord.gg/glif
- X: https://x.com/heyglif

## Registries

- Anthropic MCP Registry

## License

MIT - see [LICENSE](LICENSE)
