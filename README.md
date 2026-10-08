# Rumoro MCP server

[Rumoro](https://rumoro.dev) tracks what people say about your product, your competitors and your topics on Reddit, X, Hacker News, GitHub, YouTube, LinkedIn, Bluesky, Stack Overflow, DEV, TikTok, Instagram and news sites. Each mention is scored for relevance to your company.

The MCP server gives Claude, Cursor, Codex and any other MCP client access to your Rumoro workspace. Your agent can search and triage mentions, manage keywords and alerts, and read analytics, with 55 tools in total.

This repository holds the setup instructions and the server's [MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=dev.rumoro) entry. The server itself is hosted by Rumoro, so there is nothing to install or run.

- Endpoint: `https://mcp.rumoro.dev/mcp` (streamable HTTP)
- Sign-in: OAuth in the browser, or an API key sent as a Bearer header
- Registry name: `dev.rumoro/mcp`

## Connect

You need a Rumoro account. Sign up at [rumoro.dev](https://rumoro.dev); new accounts start with $5.80 of free credit.

### Claude Code

```bash
claude mcp add --transport http --scope user rumoro https://mcp.rumoro.dev/mcp
```

Then run `/mcp` in Claude Code, pick `rumoro`, choose Authenticate and approve in the browser.

### Claude Desktop and claude.ai

Open Customize › Connectors, choose Add › Add custom connector, paste `https://mcp.rumoro.dev/mcp` and sign in.

### Cursor

Add this to `~/.cursor/mcp.json`, or to `.cursor/mcp.json` in one project:

```json
{
  "mcpServers": {
    "rumoro": { "url": "https://mcp.rumoro.dev/mcp" }
  }
}
```

Cursor asks you to sign in the first time it uses the server.

### Codex

```bash
codex mcp add rumoro --url https://mcp.rumoro.dev/mcp
codex mcp login rumoro
```

### Other clients

Any client that supports remote MCP servers over streamable HTTP can connect to `https://mcp.rumoro.dev/mcp`. Clients that support OAuth find the sign-in on their own.

## With an API key

For CI, servers or clients without a browser, create a key on the API keys page of the Rumoro dashboard and export it as `RUMORO_API_KEY`.

```bash
# Claude Code
claude mcp add --transport http rumoro https://mcp.rumoro.dev/mcp \
  --header "Authorization: Bearer $RUMORO_API_KEY"

# Codex
codex mcp add rumoro --url https://mcp.rumoro.dev/mcp \
  --bearer-token-env-var RUMORO_API_KEY
```

In Cursor, add a header to the entry:

```json
"rumoro": {
  "url": "https://mcp.rumoro.dev/mcp",
  "headers": { "Authorization": "Bearer ${env:RUMORO_API_KEY}" }
}
```

## Try it

Once connected, ask your agent something like:

- "List the keywords I track in Rumoro"
- "Show me this week's relevant mentions from Reddit and Hacker News"
- "Which competitor got the most mentions this month?"

## Pricing

Prepaid, with no subscription. $5 per keyword per month plus $0.008 per matched mention. See [rumoro.dev/pricing](https://rumoro.dev/pricing).

## More

- Setup guides for [Claude](https://rumoro.dev/claude), [Cursor](https://rumoro.dev/cursor) and [Codex](https://rumoro.dev/codex)
- TypeScript SDK: [`@rumoro-dev/sdk`](https://www.npmjs.com/package/@rumoro-dev/sdk)
- Python SDK: [`rumoro`](https://pypi.org/project/rumoro/)
- CLI: [`@rumoro-dev/cli`](https://www.npmjs.com/package/@rumoro-dev/cli)

## Support

If the server won't connect or a tool behaves unexpectedly, open an issue in this repository or email markus@rumoro.dev.
