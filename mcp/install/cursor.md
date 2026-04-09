# Cursor profile

## Prerequisites

- Cursor with MCP support turned on.
- A browser so you can finish OAuth.

## Configuration

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

## What happens when you connect

1. Cursor sends `initialize` to `https://mcp.brivvy.io`.
2. Brivvy responds with `401` and a `WWW-Authenticate` metadata hint.
3. Cursor discovers `.well-known` endpoints.
4. You finish OAuth in the browser.
5. Cursor retries with a bearer token and loads tools.

## Workspace scope

Every MCP client on your account uses the workspace you **last chose** on the OAuth screen. To switch, reconnect and pick a different workspace there.

## Sessions

The client refreshes access tokens until the refresh token expires. Refresh tokens last **90 days**. After that, reconnect Brivvy MCP and sign in again.

## Quick checks

- Discovery works:
  - `GET /.well-known/oauth-protected-resource`.
  - `GET /.well-known/oauth-authorization-server`.
- After auth, you should see tools such as `list_voices`, `get_voice`, `list_templates`, `list_discover_templates`, and `get_template`.

## Related docs

- MCP overview: [https://docs.brivvy.io/mcp-server](https://docs.brivvy.io/mcp-server).
- Cursor setup page: [https://docs.brivvy.io/cursor](https://docs.brivvy.io/cursor).
