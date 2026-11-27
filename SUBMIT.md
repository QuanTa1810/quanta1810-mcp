# Where to submit

Prepared 2026-11-27. Nothing below has been submitted yet. Use the same name, summary and URL everywhere (copy from `listing-kit.json`).

- Name: `Quanta1810 Web Audit & Lazada Tools`
- Registry ID: `io.github.QuanTa1810/quanta1810-mcp`
- Summary (97 chars, limit 100): `Bulk website health, PageSpeed, redirect, SSL and DMARC/SPF checks, email finder, Lazada scraper.`
- Repo: `https://github.com/QuanTa1810/quanta1810-mcp` (must be public first)
- MCP URL: see `server.json` → `remotes[0].url`

## 0. Before anything: publish the repo

Create the public GitHub repo `QuanTa1810/quanta1810-mcp` with these files (README.md, LICENSE, server.json, glama.json, listing-kit.json, SUBMIT.md). Add topics: `mcp`, `mcp-server`, `remote-mcp`, `apify`, `seo`.

## 1. Official MCP Registry (free) — do first

Other directories read from it (Glama connectors, PulseMCP, GitHub's MCP list). Remote-only servers need no package. Versions cannot be changed after publishing; bump `version` for any edit.

```bash
curl -L "https://github.com/modelcontextprotocol/registry/releases/latest/download/mcp-publisher_$(uname -s | tr '[:upper:]' '[:lower:]')_$(uname -m | sed 's/x86_64/amd64/;s/aarch64/arm64/').tar.gz" | tar xz mcp-publisher
./mcp-publisher validate            # in this folder
./mcp-publisher login github        # human step: open github.com/login/device, enter the code, sign in as QuanTa1810
./mcp-publisher publish
curl "https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.QuanTa1810"
```

Limits: `description` 1–100 chars, `title` ≤100, `name` must start `io.github.QuanTa1810/` (case as on GitHub). The registry does not check that we own the remote URL; another Apify seller (`ai.xomia/xomiadata-apify-actors`) is listed the same way.

## 2. Glama (free)

- Connectors (remote servers): glama.ai/mcp/connectors. Check a few days after step 1 whether it appeared at `https://glama.ai/mcp/connectors/io.github.QuanTa1810/quanta1810-mcp`. If not, use "Add Server" (sign in with GitHub).
- Claiming a connector asks for `/.well-known/glama.json` on the server's domain. The domain is `mcp.apify.com`, which we cannot edit, so a connector claim may not be possible; e-mail support@glama.ai if needed.
- Repo listing: `glama.json` is in the root (`"maintainers": ["QuanTa1810"]`); sign in with GitHub and claim the repo.
- Both awesome lists from punkpeye (below) require the Glama badge, so this step blocks them.

## 3. awesome-remote-mcp-servers (punkpeye, ~4.2k stars, active) — PR

Remote-only servers go here, not in punkpeye/awesome-mcp-servers (that one is for self-hosted servers with a package). Rules: star the repo first (required), Glama connector badge required, CI checks the URL answers `initialize` (Apify answers 401 + OAuth metadata, which the list treats as OAuth `🔐`). One-sentence description ≤120 chars, alphabetical within the category. Suggested category: pick the closest existing one (e.g. developer tools / SEO); check the README index.

Entry:

```markdown
- [Quanta1810 Web Audit & Lazada Tools](https://apify.com/quanta1810) `https://mcp.apify.com/?tools=quanta1810/website-health-audit,quanta1810/bulk-pagespeed,quanta1810/bulk-redirect-checker,quanta1810/lazada-scraper,quanta1810/dmarc-spf-checker,quanta1810/ssl-certificate-checker,quanta1810/website-contact-finder`
  [![Quanta1810 Web Audit & Lazada Tools MCP connector](https://glama.ai/mcp/connectors/io.github.QuanTa1810/quanta1810-mcp/badges/score.svg)](https://glama.ai/mcp/connectors/io.github.QuanTa1810/quanta1810-mcp)
  🔐 - Bulk website health, PageSpeed, redirect, SSL and DMARC/SPF checks, a contact email finder and a Lazada scraper.
```

PR title: `Add Quanta1810 Web Audit & Lazada Tools`
PR body:

```
Adds a remote MCP server (Streamable HTTP, Apify OAuth or API token) with seven bulk tools: website health audit, PageSpeed/Lighthouse, redirect chains, SSL expiry, DMARC/SPF, contact email finder and Lazada product data. Tools run as Apify Actors and are billed per result to the user's own Apify account.

Glama connector: https://glama.ai/mcp/connectors/io.github.QuanTa1810/quanta1810-mcp
Repo: https://github.com/QuanTa1810/quanta1810-mcp
```

## 4. Other GitHub lists — PR (free)

Use the `awesome_list_line` from `listing-kit.json`:

```markdown
- [Quanta1810 Web Audit & Lazada Tools](https://github.com/QuanTa1810/quanta1810-mcp) - Remote MCP server (via Apify) for bulk website health, PageSpeed, redirect, SSL and DMARC/SPF checks, an email finder and a Lazada scraper.
```

| List | Activity (checked 2026-11-27) | Notes |
|---|---|---|
| TensorBlock/awesome-mcp-servers | ~1.2k stars, pushed today, 15 open issues/PRs | Read its CONTRIBUTING and category files before the PR |
| MobinX/awesome-mcp-list | ~920 stars, pushed 2026-11-19, 165 open | Same line, match its format |
| toolsdk-ai/toolsdk-mcp-registry | ~360 stars, pushed today | Uses JSON files per server, not a README line; follow its template |

Skip: jaw9c/awesome-remote-mcp-servers (no merges since 2026-06), punkpeye/awesome-mcp-servers (out of scope for remote-only).

## 5. Directories with a web form (free path)

| Directory | Free path | Notes |
|---|---|---|
| MCP.so | free form, "remote" type | $39 fast track optional; does not read the official registry |
| mcpservers.org | free review (~2 weeks) | dofollow link only on $39 tier |
| MCP Market (mcpmarket.com/submit) | submit GitHub repo | free queue 4–6 weeks, $29 fast track |
| mcp.directory | free form | not `mcpdirectory.app` |

Ask Quân before paying for any fast track.

## 6. Smithery — on hold

Smithery was bought by Arcade (Aug 2026). Its hosting, CLI and old publish docs were shut down or deprecated on 2026-10-31 (docs URLs now 404). smithery.ai/future says it stays as a curated registry of verified servers but gives no submit flow. No Smithery config file is needed in the repo. Only contact listed: ani@smithery.ai. Recheck later or skip.
