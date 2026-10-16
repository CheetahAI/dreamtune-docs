# Dreamtune documentation

Customer documentation for `CheetahAI/dreamtune-docs`, published by Mintlify from
`main`. The documentation directory in Mintlify is blank (repository root).
`docs.json` defines branding and navigation; `.mdx` files contain customer pages.
This is a separate Git repository inside the local platform checkout.

## Maintain

Use Node.js 22.20 or later:

```sh
npm ci
npm run validate
npm run check:links
npm run check:a11y
```

The Mintlify CLI is pinned to `mint` 4.2.1042. The latest registry version was
verified on 2026-10-16 (Asia/Calcutta); no prior CLI dependency existed here.
Official documentation requires Node 20.17 or later; this project's minimum also
supports the Dreamtune SDK. Customer examples were checked against the published
`@dreamtune/sdk` 0.1.1 types, command definitions and README in the platform repo.
Validation checks documentation, not live paid provider execution.

## Publish

Commit reviewed source changes and push to `origin main`. The connected Mintlify
GitHub App builds the site. Verify the public docs after the existing GitHub integration publishes. No additional dashboard access is required.
Rollback by reverting the relevant documentation commit and pushing normally.
No frontend/backend application server or local trace Collector is required.

Use `docs.dreamtunelabs.com` as the documentation hostname. The apex
`dreamtunelabs.com` already serves the application through its Cloudflare Worker.
Add the docs subdomain in Mintlify and use the exact CNAME and verification TXT
records it supplies. Set the docs CNAME to DNS only for pre-validation. Do not
replace the application's Worker-managed apex record.

## Official sources and adaptations

Read through Context7 `/mintlify/docs` and live official pages on 2026-10-16:

- [Configuration](https://www.mintlify.com/docs/organize/settings): root `docs.json`,
  required name/theme/colors/navigation; no obsolete `mint.json`.
- [Branding](https://www.mintlify.com/docs/organize/settings-appearance): supported
  light/dark logos, favicon, background and colors. Dreamtune's existing diamond
  mark and website palette are retained, with its darker accent for readable links.
- [Cards](https://www.mintlify.com/docs/components/cards): native cards/columns for
  the introduction. No replacement frontend or custom runtime was added.
- [CLI installation](https://www.mintlify.com/docs/cli/install) and
  [commands](https://www.mintlify.com/docs/cli/commands): use the current `mint`
  package, strict validation, internal-link and accessibility checks.
- [GitHub deployment](https://www.mintlify.com/docs/deploy/github) and
  [domains](https://www.mintlify.com/docs/customize/custom-domain): connected `main`
  deployment and separate docs hostname. No nameserver migration is needed.

There are no credentials in documentation. Examples require the customer's own
key and selection of actual catalog identifiers. Private platform deployment,
vault paths and operator login information are excluded.

## Verification on 2026-10-16

- Before creation, `mint validate` failed explicitly because `docs.json` was absent.
- The official `mint new` command scaffolded an isolated starter under the platform
  checkout's ignored `.automation` directory; the existing repository/license were
  preserved. Customer files were written here with supported native configuration.
- The pinned CLI's strict build validation and internal-link/anchor checks passed.
- Accessibility initially failed a dark-mode button color. Using the existing
  website hover accent fixed it. All 56 MDX pages passed media-alt checks; colors
  meet the CLI's required contrast thresholds. It still advises AAA contrast for
  the primary link color, which meets AA at 6.16:1.
- Formatting, parent repository verification/contract/size gates and staged
  Gitleaks scanning passed. The original Dreamtune SVG assets are six physical lines;
  prose, JSON and the lockfile are not executable code under the size policy.
- `npm audit --omit=dev --audit-level=high` reported zero production dependencies
  with advisories. This excludes the Mintlify development tool dependency tree;
  npm reported upstream transitive deprecation and install-script warnings.
- No paid service calls, application server startup, trace Collector restart,
  credential changes or application DNS edits were needed for this documentation.

Coverage is documentation configuration, navigation, MDX compilation, links,
accessibility, formatting and source secrets. API authorization, concurrency and
billing behavior are outside this documentation-only change; source examples
were reviewed against the published SDK rather than executed with customer keys.
Hosted publication is verified in the final delivery record below.

## Expanded documentation, 2026-10-16

The site now contains 56 MDX pages across Guides, SDK & CLI, Agents & MCP,
and API reference. It includes 12 client-specific guides, official vendor
logos, two local workflow tutorials, resource/method/tool references,
prompt variables, media/session guidance, payment recovery and production
integration practices. See RESEARCH.md for primary-source research and client
format distinctions. Roo Code is clearly legacy following its official shutdown.

The header links Home to the application. Native Mintlify contextual controls
provide Copy page and Markdown. Native llms/skills discovery and distinct
human/execution/documentation MCP addresses support agent discovery. Published
0.1.1 skills are included verbatim in .mintlify/skills and downloads, with a ZIP
and license. No extra service, paid Assistant or agent login flow was added.

Strict build, internal-link/anchor and media accessibility checks pass. The
primary accent meets AA (6.16:1) and retains the CLI's AAA improvement advisory.
Published-package CLI help, skill listing and installation of all five skills
were exercised in an ignored isolated directory. This does not claim live
execution in every editor or a new paid-provider audit.

## Hosted delivery verified

The existing GitHub integration published all 56 pages at
https://docs.dreamtunelabs.com. Native Hurl checked the complete navigation,
exact logo homepage destination, canonical metadata, rendered Copy page control,
public Markdown, llms index, skills discovery and the public GitHub ZIP download.
The Dreamtune logo and Home header link both point to the application homepage.
The application was redeployed with direct links and permanent old-guide redirects.

The final desktop Lighthouse audit reported performance 98, accessibility 97,
best practices 100 and SEO 100. Its rendered screenshot was inspected. Native
Mintlify branding/footer contrast remains an accessibility advisory; interactive
clipboard/editor setup was not verified through a signed-in browser. No paid
service execution is claimed by these documentation checks.
