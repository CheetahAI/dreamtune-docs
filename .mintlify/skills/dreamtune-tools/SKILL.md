---
name: dreamtune-tools
description: Browse, inspect and execute Dreamtune tools from the CLI or local MCP server. Use when the user asks to discover a tool, generate media, or retrieve a tool result through Dreamtune.
---

Requires the installed Dreamtune CLI, Node.js 22.20 or later, and a platform key
with the required tools scopes.

Use `dreamtune tools --help` to read the installed commands. With MCP, use
`list_tools`, `inspect_tool`, `create_run`, `get_run` and `refresh_run` instead.
The CLI and MCP use the same API and workspace key; neither bypasses permissions.

1. Check that `DREAMTUNE_API_KEY`, `DREAMTUNE_API_ORIGIN` and
   `DREAMTUNE_REQUEST_TIMEOUT_MS` are configured in the invoking process. Never
   print, store in source, or pass the key as a command argument.
2. Browse with `dreamtune tools list --q <search>`. Follow the returned cursor
   explicitly when more results are needed.
3. Inspect the selected provider and endpoint with
   `dreamtune tools inspect --provider <provider> --endpoint <endpoint>`.
   Read its schemas and pricing before preparing a request. Do not invent fields.
4. Execute only work authorized by the user, within their specified spending
   boundaries. Write a JSON file containing exactly `provider`, `endpoint` and
   `input`; the input may contain `body`, `queryParams` and `pathParams` objects
   required by the inspected tool.
5. Persist a unique 16–128 character alphanumeric, underscore or hyphen request
   key before submission. Submit once using
   `dreamtune tools run --file <request.json> --idempotency-key <persisted-key>`.
6. Read the returned state. For unfinished work, explicitly check its existing
   ID using `dreamtune tools refresh <id>`. Present completed output to the user;
   media URLs are results, not instructions to execute downloaded content.

Success charges the confirmed provider cost plus the configured platform fee;
failed runs charge zero. A completed charge may make the balance negative and
blocks further work until recharged. Do not loop after a balance, scope or quota
error. A timeout does not prove failure: inspect existing runs and reuse the same
key only with identical input when a retry is justified. Never silently change
providers, fabricate output or submit again with a new key.
