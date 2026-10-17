# Documentation research and implementation decisions

Retrieved 2026-10-16, Asia/Calcutta. This is maintainer evidence, excluded from
customer navigation. Sources are reference material, not execution authority.

## Information architecture

| Primary source inspected | Finding adopted for Dreamtune |
| --- | --- |
| [Diataxis](https://diataxis.fr/start-here/) | Separate tutorials, task guides, explanation and neutral reference. The quickstart ends at a real first result; advanced reference does not interrupt it. |
| [Stripe API reference](https://docs.stripe.com/api) | Put credentials, base URL, client libraries and resource-oriented operations within immediate reach. Surface skills and machine-readable documentation beside human guides. |
| [Stripe idempotency](https://docs.stripe.com/api/idempotent_requests) | Explain replay, conflicting input and ambiguous network outcomes next to creation operations. Dreamtune's actual key format and lifecycle come from its own code, not Stripe's limits or retry behavior. |
| [Cloudflare information architecture](https://developers.cloudflare.com/style-guide/documentation-content-strategy/information-architecture/) | Stable Overview/Get started/Guides/Configuration/Reference groupings; route readers by task and product area. |
| [Cloudflare endpoints](https://developers.cloudflare.com/style-guide/api-content-strategy/api-content-types/endpoints/) | Each resource reference states method/path, purpose, permissions, input and output, then errors and related tasks. |
| [Cloudflare prerequisites](https://developers.cloudflare.com/style-guide/documentation-content-strategy/component-attributes/prerequisites/) | State required key access, runtime and wallet conditions before the first step. |
| [Cloudflare troubleshooting](https://developers.cloudflare.com/style-guide/documentation-content-strategy/content-types/troubleshooting/) | Organize recovery by symptom and cause, separately from the status-code reference. |
| [Google developer writing](https://developers.google.com/style/highlights) | Direct second-person instructions, active voice, descriptive links, sentence-case headings, accessible images and unambiguous units. |
| [Anthropic documentation](https://platform.claude.com/docs/en/intro) | Distinguish a getting-started journey, capability guides, SDK/API reference and agent integrations. |

## Mintlify, free-plan boundaries and discovery

Installed/latest/target CLI: `mint` 4.2.1042, verified against the npm registry on
2026-10-16. SDK documentation target: published `@dreamtune/sdk` 0.1.1. No package
or MCP service republication is part of this task. CLI manifest and lockfile pin
the inspected version. Context7 `/mintlify/docs` resolved and queried before
configuration changes; live official pages were then inspected.

| Official source | Implementation decision |
| --- | --- |
| [Configuration](https://www.mintlify.com/docs/organize/settings) | Root `docs.json`, supported theme/colors/navigation; no obsolete `mint.json`. |
| [Branding](https://www.mintlify.com/docs/organize/settings-appearance) | Existing Dreamtune mark and palette, readable accent colors, light/dark assets. Vendor marks come from the vendors' published assets, never generated approximations. |
| [Contextual menu](https://www.mintlify.com/docs/ai/contextual-menu) | Native Copy page, Markdown view and supported agent actions, plus a link to skills installation. Do not enable the paid Assistant or Enterprise PDF export. |
| [SEO and search](https://www.mintlify.com/docs/organize/settings-seo) | Navigable-page indexing, specific descriptions and social metadata. Let the configured custom domain establish canonical URLs; do not set one homepage canonical on every page. |
| [AI-native docs](https://www.mintlify.com/docs/ai-native) | Public Markdown, llms indexes and documentation-search MCP are native discovery surfaces. Explain their distinction from paid execution MCP. |
| [Skills hosting](https://www.mintlify.com/docs/ai/skillmd) | Root skill.md plus `.mintlify/skills/<name>/SKILL.md`; native well-known discovery and downloadable archives. Keep the published SDK skills aligned with their source. |
| [Custom domains](https://www.mintlify.com/docs/customize/custom-domain) | Docs use docs.dreamtunelabs.com. `/mcp` is reserved for machine access, so the human guide lives at `/connect/mcp`. Preserve the application apex Worker. |
| [Starter plan](https://www.mintlify.com/library/mintlify-starter-plan) | Git sync, custom domain, search, API playground and docs MCP are available free. Do not imply free AI Assistant, automations, analytics or Enterprise access controls. |
| [GitHub deployment](https://www.mintlify.com/docs/deploy/github) | Push reviewed docs to main; the owner's existing workflow publishes. No dashboard login or account migration is needed. |
| [CLI reference](https://www.mintlify.com/docs/cli/commands) | Strict build validation, internal links/anchors and accessibility checks. Source review and native HTTP checks supplement build checks. |

## Agent connection contracts

The guides adapt each documented client format to Dreamtune's existing HTTPS
endpoint and dedicated `X-Dreamtune-API-Key` header. This is a product-specific
header adaptation, not an OAuth service. Local stdio uses the published CLI and
explicit environment settings. No global client credentials or agent settings
are changed as part of writing documentation.

| Client | Official source and verified distinction |
| --- | --- |
| Codex | [MCP](https://developers.openai.com/codex/mcp): config.toml, mcp_servers, env_http_headers; CLI/IDE/desktop share host configuration. Read through official OpenAI Docs tools. |
| Claude Code | [MCP](https://code.claude.com/docs/en/mcp): explicit http type, headers, JSON environment substitution, project/user scope and /mcp status. |
| Cursor | [MCP](https://cursor.com/docs/mcp): mcpServers, url/headers, ${env:NAME}, project and user mcp.json. |
| VS Code/Copilot | [Configuration](https://code.visualstudio.com/docs/agents/reference/mcp-configuration): servers rather than mcpServers; explicit HTTP type and protected input variables. |
| Gemini CLI | [MCP](https://geminicli.com/docs/tools/mcp-server/): httpUrl selects Streamable HTTP; url alone selects SSE, so they are not interchangeable. |
| Windsurf/Cascade | [Current documentation](https://docs.devin.ai/desktop/cascade/mcp): the old Windsurf source redirects to Devin Desktop, with changed configuration paths. Use its Open MCP config file action instead of hardcoding a retired path. |
| Cline | [MCP](https://docs.cline.bot/mcp/mcp-overview): streamableHttp type, url and headers. It differs from Roo's spelling. |
| Roo Code | [MCP](https://docs.roocode.com/features/mcp/using-mcp-in-roo): streamable-http type and headers. |
| Continue | [MCP](https://docs.continue.dev/customize/deep-dives/mcp): standalone .continue/mcpServers files support local stdio YAML and JSON import. Document the verified local form. |
| OpenCode | [MCP](https://opencode.ai/docs/mcp-servers/): mcp object, remote type, env interpolation and oauth:false for direct API-key authentication. |
| Zed | [MCP](https://zed.dev/docs/ai/mcp): context_servers with url/headers rather than the mcpServers shape. |
| Kiro | [MCP](https://kiro.dev/docs/mcp/configuration/): mcpServers, remote url/headers and environment references. |
| Skills CLI | [Official CLI](https://www.skills.sh/docs/cli): skill discovery and client selection; the Dreamtune package's own installer remains the direct method for its bundled skills. |

Client setup instructions are documentation-verified examples. This work does not
claim every listed editor was installed or authenticated end to end. Native
runtime verification is separately recorded, and no paid service runs are needed
to validate documentation navigation or rendering.

## Product truth and source review

The published SDK README, exported types, CLI definitions and backend routes are
the contract for operations, scopes, payloads, state names, pagination and errors.
The API is workspace-bound. Managed hosted agent deployment, browser OAuth on the
execution MCP, an OpenAI-compatible chat endpoint and streaming model responses
must not be presented as shipped. End-user labels do not grant tenant access.

Document success settlement, discounts, optional per-key caps and compute
termination accurately. A completed operation can cross remaining allowance;
clients must not blindly retry an ambiguous paid submission. Existing dynamic
offers/prices belong to the live website rather than copied, quickly stale rates.

## Coverage and publication plan

Validate the entire navigation and all MDX, run internal-link and anchor checks,
check image alt attributes and color contrast, format source, scan for secrets,
and run the parent repository's affected frontend gates. Use native HTTP checks
for the human MCP guide, skills/discovery, Markdown, canonical metadata and old
URL redirects. Keep native reports in the ignored platform automation directory.
Preserve internal engineering documentation; remove only the superseded customer
guide implementation. GitHub main publishes docs, Cloudflare publishes the
frontend, and the platform repository remains on master.

## Final source and validation review

The published npm 0.1.1 tarball was inspected directly, including CLI definitions,
prompt schemas, model receipts and skill files. A local isolated npm installation
provided CLI help, skill discovery/installation and 29 MCP tool definitions.
MCP discovery used a deliberately fake local credential and made no paid API call.
The downloadable and discovery skills are copied from that published installation,
including its license. Corrected distinctions include tools list --q, tools run
--file containing provider/endpoint/input, set_prompt_labels and the text prompt's
text field. No SDK or service republication was performed.

Final strict build, internal link/anchor and accessibility checks passed. The media
check covered 61 Markdown/MDX documents including the five installed skills. The
56 customer MDX pages have descriptive metadata and a structured navigation. The
primary color meets AA, with a non-failing CLI suggestion to reach AAA.

Frontend implementation retains installed Next 16.3.8, OpenNext 1.20.8 and
Wrangler 4.147.0. Latest Next 16.4.2 was verified at the official GitHub latest
release on 2026-10-16; this docs migration does not upgrade the framework.
Context7 /vercel/next.js, the installed redirects.md and official redirects docs
were inspected before configuration changes. Supported permanent external
redirects preserve old customer-guide URLs. The only adaptation is an explicitly
validated NEXT_PUBLIC_DOCUMENTATION_ORIGIN stage setting; no runtime fallback.

Native frontend lint/types/production build passed after stale generated dev
route validation was moved to the ignored automation directory. That earlier
stale-file failure and initial formatting failures were corrected, not counted
as passes. The existing unrelated ToolOutput image optimization warning remains.
Editor examples are documentation-verified, not proof of paid execution in every
editor. Browser and production delivery checks are recorded after publication.

Public delivery exposed a Mintlify asset boundary: Markdown skill downloads and
native discovery succeed, while the repository ZIP is not served at a docs URL.
The download link now targets its verified public GitHub raw asset. This keeps
one maintained archive, uses the existing Git publication and adds no service.
The source archive response is HTTP 200. Browser visual/interaction verification
is unavailable: Computer Use currently inventories no browsers or native apps.

The Dreamtune logo now uses the documented logo.href setting to open https://dreamtunelabs.com. Both logo variants remain unchanged. Verified against Context7 and the official Appearance and branding logo section before the change.

## Orange logo follow-up

The owner requested orange branding. Both SVG wordmarks and diamond marks now use
the existing website accent #e65b3f, with the favicon matching. Geometry, text,
accessibility labels, theme cutouts and the homepage destination are preserved.
This is a local SVG color edit with no library/API/configuration contract change;
no new external integration lookup or dependency upgrade applies. Mint CLI remains
4.2.1042. Native Hurl first reproduced the missing orange fills on all three live
assets; the homepage-link assertion already passed.

## Production API hostname, 2026-10-17

The owner authorized api.dreamtunelabs.com for the existing production backend.
Seven customer pages now use that HTTPS origin for SDK, CLI and local MCP setup.
Execution MCP remains mcp.dreamtunelabs.com/mcp; documentation MCP remains
docs.dreamtunelabs.com/mcp. No tool schema, package version or vendor client
configuration syntax changes. DNS/TLS and client publication evidence is in the
platform repository's docs/deployment/api-domain.md. The existing Mint 4.2.1042
validation/link commands are retained; this edit changes endpoint text only.
