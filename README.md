# Brivvy AI

This repo is your public entry point for Brivvy AI integrations. You get MCP server metadata, install steps, client connection profiles, and release notes.

The implementation stays private. Everything here is safe to publish.

## What you connect to

- **Server type:** Remote MCP (Streamable HTTP).
- **Production URL:** `https://mcp.brivvy.io`.
- **Auth:** OAuth 2.1-style flow with PKCE.
- **Discovery:** Use these before you call the JSON-RPC endpoint:
  - `https://mcp.brivvy.io/.well-known/oauth-protected-resource`.
  - `https://mcp.brivvy.io/.well-known/oauth-authorization-server`.

### Tools you can rely on

These tool names are the public contract. Short descriptions match what the hosted server exposes today (see [MCP Server](https://docs.brivvy.io/mcp-server) for connection guides, security notes, and FAQs).

| Area      | Tool                      | What it does                                                        |
| --------- | ------------------------- | ------------------------------------------------------------------- |
| Voices    | `list_voices`             | Lists published voices in your workspace.                           |
| Voices    | `get_voice`               | Returns tone and style rules for the default or a chosen voice.     |
| Templates | `list_templates`          | Lists content templates saved in your workspace.                    |
| Templates | `list_discover_templates` | Lists public templates from the Brivvy community catalog.           |
| Templates | `get_template`            | Returns the full prompt and instructions for a template you select. |

## Quick start

### Cursor

Add Brivvy as a remote MCP server:

```json
{
  "mcpServers": {
    "Brivvy": {
      "url": "https://mcp.brivvy.io"
    }
  }
}
```

Connect once, then finish OAuth in the browser when the client asks you to.

### Claude

Point your MCP connector at:

- **URL:** `https://mcp.brivvy.io`.
- **Transport:** Streamable HTTP.
- **Auth:** OAuth.

Claude reads `.well-known` metadata and walks you through consent.

## Workspace scope

Your Brivvy account uses **one workspace at a time** for MCP. The workspace you **last picked** on the OAuth screen applies to **every** MCP client until you authorize again and choose a different one. If you run Cursor and Claude side by side, they do not keep separate workspace picks today.

## Sessions and reconnection

Your access token stays short-lived. The client should refresh it with your refresh token. Refresh tokens last **90 days** (Amazon Cognito). When that window ends, connect again and run through OAuth.

## When something breaks

- **`401` on `POST /`:** Normal before OAuth. Your client should follow the `WWW-Authenticate` hint and complete discovery.
- **Disconnects right after consent:** Check the callback URL, try once more, and make sure you finished the OAuth popup.
- **Token errors:** Reconnect so you get a fresh bearer token. Do not reuse an old web session token.
- **No tools listed:** Your MCP consent or workspace access may be missing or expired.
- **Wrong workspace:** Reconnect and pick the workspace you want on the OAuth screen. That choice applies across all MCP clients on your account.

## What lives here

- `mcp/server.json`, registry metadata.
- `mcp/install/`, Cursor and Claude profiles.
- `VERSIONING.md`, how we version this public metadata.
- `CHANGELOG.md`, release notes.
- `SECURITY.md`, how to report issues.

Internal release and directory workflows stay in the private Brivvy MCP repo.

## How to reach us

- Support: [`support@brivvy.io`](mailto:support@brivvy.io).
- Security: [`security@brivvy.io`](mailto:security@brivvy.io).
