---
name: dreamtune-platform
description: Select the Dreamtune CLI, MCP or TypeScript SDK for model, tool, GPU and observability tasks. Use when a user asks to use Dreamtune, connect an agent, rent compute, or integrate Dreamtune into an application.
---

Use the interface selected by the user and available in this agent environment.
MCP must be connected to the agent; CLI commands require a local terminal; the
SDK is for application code. Installing the package does not connect an MCP
server or install skills into the agent automatically.

- For discovered platform API operations, use connected MCP tools and their
  advertised schemas. For terminal workflows, read `dreamtune --help` and the
  relevant command's help. Do not invent commands or methods.
- For a complete GPU workflow on this computer, use the CLI or advertised local
  compute tools. Both share saved SSH keys and named launch references.
- For hosted MCP, prepare access on the user's computer through the CLI; submit
  only public launch fields. A hosted server cannot write local keys or open
  a terminal on the user's computer.
- When building an application, use `@dreamtune/sdk`. Its HTTP compute methods
  require explicit public keys and idempotency keys. Node applications can use
  `LocalComputeClient` from `@dreamtune/sdk/node` for managed local access.
- Load the relevant installed `dreamtune-compute`, `dreamtune-tools`,
  `dreamtune-models` or `dreamtune-observability` skill for the full workflow.

Never submit the same billable work through both CLI and MCP. Preserve the same
launch name/request reference to recover uncertain work. If the selected
interface fails, report the failure and inspect existing work; do not switch
interfaces to submit it again. API scopes and wallet rules determine access.
Keep platform credentials and SSH private-key contents out of arguments,
responses, logs, prompts and committed files. A key file path is sufficient for
the SSH client; the agent does not need to read its contents.
