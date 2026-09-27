---
title: MCP server
nav_order: 3
has_children: true
permalink: /mcp/
---

# The PageToVid MCP server
{: .no_toc }

Ask your AI assistant for a video in plain words — "make a 30-second ad for stripe.com", "turn this table into a chart video", "put a presenter in the corner of scene 2" — and it drives PageToVid for you: it inspects the page, writes and edits the storyboard, renders, reads the result and fixes it.

**Endpoint:** `https://pagetovid.com/mcp` · Streamable HTTP · OAuth sign-in (or an API key for headless agents).
{: .fs-5 }

1. TOC
{:toc}

## Install

Pick your client. Every one of them signs you in to PageToVid the first time a tool is called — there is no key to copy unless you want one.

### Claude Code

```bash
claude mcp add --transport http pagetovid https://pagetovid.com/mcp
```

Run /mcp inside Claude Code and authenticate — a browser opens, you sign in to PageToVid once, and that is it.

### Claude (web, desktop, mobile)

Settings → Connectors → Add custom connector → paste https://pagetovid.com/mcp

Claude opens a PageToVid sign-in and asks you to approve access. Custom connectors are available on paid Claude plans.

### Cursor

[Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=PageToVid&config=eyJ1cmwiOiJodHRwczovL3BhZ2V0b3ZpZC5jb20vbWNwIn0=){: .btn .btn-primary }

Opens Cursor and pre-fills the server. Cursor then runs the sign-in for you.

### VS Code (Copilot agent mode)

[Install in VS Code](vscode:mcp/install?%7B%22name%22%3A%22pagetovid%22%2C%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fpagetovid.com%2Fmcp%22%7D){: .btn .btn-primary }

VS Code signs you in on first use. Or add it by hand to .vscode/mcp.json.

### VS Code — by hand

In `.vscode/mcp.json`:

```json
{
  "servers": {
    "pagetovid": {
      "type": "http",
      "url": "https://pagetovid.com/mcp"
    }
  }
}
```

### Codex

In `~/.codex/config.toml`:

```toml
[mcp_servers.pagetovid]
url = "https://pagetovid.com/mcp"
```

Codex runs the sign-in on first use. For a headless agent, add http_headers = { Authorization = "Bearer cp_live_…" } instead.

### Gemini CLI

```bash
gemini mcp add --transport http pagetovid https://pagetovid.com/mcp
```

### Claude API (Messages)

```json
{
  "mcp_servers": [
    {
      "type": "url",
      "url": "https://pagetovid.com/mcp",
      "name": "pagetovid",
      "authorization_token": "YOUR_KEY"
    }
  ]
}
```

Pass alongside your messages request; the model can then call the tools directly.

### Anything else

```json
{
  "mcpServers": {
    "pagetovid": {
      "type": "http",
      "url": "https://pagetovid.com/mcp"
    }
  }
}
```

The shape most clients accept for a remote Streamable HTTP server. A client that cannot sign in can send an API key header instead — see below.

## API keys for headless agents

A client that cannot run a browser sign-in (a CI job, a server-side agent) sends an API key instead: create one in your [account](https://pagetovid.com/account) and pass it as `Authorization: Bearer cp_live_…`. A key spends your credits — keep it in your secret manager, never in a repository.

## What to read next

- [Tool reference](tools) — all 36 tools and every parameter, generated from the server.
- [The server's own guidance](instructions) — what the server tells every assistant when it connects.
- [Best practices](../guides/best-practices) — how to get a film that is ready to publish.
- [Recipes](../guides/recipes) — complete conversations for the common jobs.
