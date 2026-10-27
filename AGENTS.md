# Repository guide

This repository packages Kooga's hosted MCP server for assistants and directories. It holds no server code. It is published from Kooga's main repository, so a change made only here is replaced at the next sync: make it there.

- Keep the four plugin manifests (`plugin.json`, `.claude-plugin/plugin.json`, `.codex-plugin/plugin.json`, `.cursor-plugin/plugin.json`) on the same name, version and description, and bump their versions together.
- Keep `mcp.json` (`streamable-http`) and `.mcp.json` (`http`) on the same server name, `kooga`, and the same address, `https://mcp.kooga.io/mcp`. Streamable HTTP only: the server has no SSE endpoint.
- `skills/kooga-mcp/references/tools.md` is generated from the server's tool list. Never edit it by hand. The connected server's own tool list and schemas are authoritative over anything written here.
- Keep the skill's rules on confirmation: anything that leaves Kooga, or cannot be taken back, is put to the person word for word, and its `confirmToken` is sent only after their yes.
- `server.json` versions are immutable once published, and a change to `server.json` on `main` publishes it to the MCP Registry. Bump `version` with every change, and never push it without the maintainer's go-ahead.
- Plugin versions and the registry version are independent.
- Never commit tokens, private keys, customer data or publishing credentials. Private reports go through [SECURITY.md](SECURITY.md).
