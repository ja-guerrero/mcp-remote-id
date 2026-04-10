# mcp-remote-id

A fork of [`mcp-remote`](https://github.com/geelen/mcp-remote) that adds support for using **id_tokens** as Bearer tokens when authenticating with remote MCP servers.

## Why this fork?

The upstream `mcp-remote` always sends the OAuth `access_token` as the Bearer token. However, some OAuth providers do not include identity claims (email, groups, etc.) in access tokens by default, making them insufficient for authorization decisions on the server side. The `id_token` contains these claims and is what remote MCP servers need to identify and authorize users.

This fork adds a `--token-type` flag that lets you send the `id_token` instead.

## What changed

- Added `--token-type` CLI argument (`access_token` | `id_token`, defaults to `access_token`)
- When `--token-type id_token` is set, the `id_token` from the OAuth token response is swapped into the Bearer header
- No behavior change when the flag is omitted — fully backwards compatible with upstream

## Usage

```json
{
  "mcpServers": {
    "remote-example": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote-id",
        "https://remote.mcp.server/sse",
        "--token-type", "id_token"
      ]
    }
  }
}
```

To use the default `access_token` behavior, simply omit `--token-type`:

```json
{
  "mcpServers": {
    "remote-example": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote-id",
        "https://remote.mcp.server/sse"
      ]
    }
  }
}
```

## Publishing

```bash
npm login
npm publish --access public
```
