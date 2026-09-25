# mcp-remote-id (Deprecated)

> **This fork is no longer needed.** The upstream [`mcp-remote`](https://github.com/geelen/mcp-remote) now natively supports `id_token` authentication via the `--use-id-token` flag. Please migrate to `mcp-remote` directly.

## Migration

Replace `mcp-remote-id` with `mcp-remote` and swap `--token-type id_token` for `--use-id-token`:

```json
{
  "mcpServers": {
    "remote-example": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://remote.mcp.server/sse",
        "--use-id-token"
      ]
    }
  }
}
```

## Original purpose

This fork added support for using **id_tokens** as Bearer tokens when authenticating with remote MCP servers. The upstream `mcp-remote` only sent the OAuth `access_token`, which some providers don't populate with identity claims (email, groups, etc.). This fork's `--token-type id_token` flag worked around that limitation.

The upstream project has since added this feature with a `--use-id-token` flag, along with additional improvements like JWT expiry handling for id_tokens.
