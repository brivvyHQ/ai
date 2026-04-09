# Claude profile

## Prerequisites

- Claude MCP connector access.
- A browser so you can finish OAuth.

## Values to enter

- **MCP server URL:** `https://mcp.brivvy.io`.
- **Transport:** Streamable HTTP.
- **Auth:** OAuth.

## What happens when you connect

1. Claude calls the MCP endpoint without a token.
2. Brivvy returns `401` and points Claude to resource metadata.
3. Claude discovers authorization metadata and starts OAuth.
4. You grant workspace consent in the browser.
5. Claude exchanges the code with PKCE and reconnects with a bearer token.

## Workspace scope

The workspace you last chose on the OAuth screen applies to every MCP client on your Brivvy account. Reconnect when you want to change it.

## Sessions

Access tokens stay short-lived. The client should refresh them until the refresh token expires. Refresh tokens last **90 days**. After that, reconnect the integration and complete OAuth again.

## Troubleshooting

- **Reconnect loop:** Try once more after consent, and confirm you finished OAuth in the same browser session.
- **No workspace access:** You may not have active MCP consent in Brivvy.
- **Invalid token:** Refresh the connection and repeat OAuth. Stale tokens fail validation.
- **No tools:** Check consent scope and workspace access.

## Related docs

- MCP overview: [https://docs.brivvy.io/mcp-server](https://docs.brivvy.io/mcp-server).
- Claude setup page: [https://docs.brivvy.io/claude](https://docs.brivvy.io/claude).
