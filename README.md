# Quanta1810 Web Audit & Lazada Tools

Bulk website health, PageSpeed, redirect, SSL and DMARC/SPF checks, email finder, Lazada scraper.

A remote MCP server that gives your AI assistant seven bulk tools: website health audits, Google PageSpeed / Lighthouse results, redirect chains, SSL certificate expiry, DMARC/SPF email security, public contact e-mails, and Lazada product data. Each tool takes a list (domains, URLs or search terms) and returns one row per item.

The tools are [Apify Actors](https://apify.com/quanta1810) published by `quanta1810`. They are served through Apify's hosted MCP endpoint, so there is nothing to install or run locally. This repository only holds the connection details and documentation.

## Server URL

```
https://mcp.apify.com/?tools=quanta1810/website-health-audit,quanta1810/bulk-pagespeed,quanta1810/bulk-redirect-checker,quanta1810/lazada-scraper,quanta1810/dmarc-spf-checker,quanta1810/ssl-certificate-checker,quanta1810/website-contact-finder
```

- Transport: Streamable HTTP
- Auth: your own Apify account, via OAuth sign-in or an API token (see [Authentication](#authentication))

## Add it to your client

### Claude (claude.ai, Claude Desktop)

Settings → Connectors → Add custom connector. Paste the server URL above. Claude opens an Apify sign-in page the first time you connect.

### Claude Code

```bash
claude mcp add --transport http quanta1810 "https://mcp.apify.com/?tools=quanta1810/website-health-audit,quanta1810/bulk-pagespeed,quanta1810/bulk-redirect-checker,quanta1810/lazada-scraper,quanta1810/dmarc-spf-checker,quanta1810/ssl-certificate-checker,quanta1810/website-contact-finder"
```

Then run `/mcp` in Claude Code and choose the server to sign in with Apify.

### Cursor

Add to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "quanta1810": {
      "url": "https://mcp.apify.com/?tools=quanta1810/website-health-audit,quanta1810/bulk-pagespeed,quanta1810/bulk-redirect-checker,quanta1810/lazada-scraper,quanta1810/dmarc-spf-checker,quanta1810/ssl-certificate-checker,quanta1810/website-contact-finder"
    }
  }
}
```

To use a token instead of OAuth, add `"headers": { "Authorization": "Bearer <your-apify-api-token>" }` next to `url`.

### VS Code

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "quanta1810": {
      "type": "http",
      "url": "https://mcp.apify.com/?tools=quanta1810/website-health-audit,quanta1810/bulk-pagespeed,quanta1810/bulk-redirect-checker,quanta1810/lazada-scraper,quanta1810/dmarc-spf-checker,quanta1810/ssl-certificate-checker,quanta1810/website-contact-finder"
    }
  }
}
```

### ChatGPT and other clients

Any client that can add a remote MCP server by URL (Streamable HTTP) works the same way: paste the server URL and sign in with Apify when asked. In ChatGPT this is done by adding a custom connector/app in developer mode; menu names change between versions.

## Authentication

The server runs on **your** Apify account. There are two ways to connect:

1. **OAuth (recommended).** The client opens an Apify sign-in page and stores the access for you. No token goes into a config file.
2. **API token.** Create a token in Apify Console → Settings → API & Integrations, then send it as the header `Authorization: Bearer <your-apify-api-token>`.

Without either, the endpoint answers `401` and lists no tools. Keep your token private; anyone with it can run Actors on your account.

## Tools

Tool names are `quanta1810--<actor-name>`. Prices are per result, charged by Apify to your Apify account (checked 2026-11-27; the Actor's Pricing tab on Apify is the current source). There is no start fee on any of them.

| Tool | What it returns | Price |
|---|---|---|
| `quanta1810--website-health-audit` | One row per site: 0–100 health score, top 3 issues in plain English, SSL expiry, on-page SEO, security headers, SPF/DMARC, sitemap, public contact e-mails | $0.003 per site audited; $0.0005 per unchanged site in monitoring mode. Unreachable, bot-protected and login-walled sites are not charged |
| `quanta1810--bulk-pagespeed` | Google PageSpeed Insights (Lighthouse) performance, SEO and accessibility scores plus real-user Core Web Vitals (LCP, INP, CLS) for mobile and/or desktop; accepts a sitemap | $0.002 per URL per device. URLs that cannot be analysed are not charged |
| `quanta1810--bulk-redirect-checker` | Every hop of each URL's redirect chain, final URL and status, loops, 302 vs 301, meta refresh, HTTPS downgrade, and checks against an old → new redirect map | $0.0005 per URL. Unreachable, blocked and invalid URLs are not charged |
| `quanta1810--dmarc-spf-checker` | One row per domain: SPF (with recursive lookup count against the limit of 10), DMARC policy and reports, DKIM keys, MX and mail provider, 0–100 score and the first thing to fix | $0.0005 per domain. Non-existent domains and DNS failures are not charged |
| `quanta1810--ssl-certificate-checker` | SSL/TLS certificate expiry date and days left, issuer, SAN names, hostname match, chain trust, TLS version and key size | $0.0005 per domain. Unreachable hosts and invalid lines are not charged |
| `quanta1810--website-contact-finder` | E-mail addresses a website publishes on its own pages, the page each was found on, the contact page URL and company social profile links | $0.001 per website, charged only when an e-mail is found |
| `quanta1810--lazada-scraper` | Lazada search and category results in Vietnam, Indonesia, Malaysia, the Philippines, Thailand and Singapore: price, discount, rating, sold count, shop, stock; optional product details and reviews | $0.0015 per product; $0.004 per product detail page; $0.001 per review. Unchanged products in monitoring mode are free |

Apify's endpoint also adds four of its own helper tools to the list (`get-actor-run`, `get-dataset-items`, `get-key-value-store-record`, `abort-actor-run`) so the assistant can read results of longer runs.

You can set a maximum cost per run on Apify to cap spending.

## Example prompts

- **Website health:** "Audit these sites and list the three with the lowest health score and their top issues: example.com, example.org, example.net"
- **PageSpeed:** "Run PageSpeed on mobile for the URLs in https://example.com/sitemap.xml (first 50) and tell me which pages fail Core Web Vitals."
- **Redirects:** "Check these old → new redirects from our migration and list any that end on the wrong URL or use 302: …"
- **DMARC/SPF:** "Check SPF and DMARC for example.com and example.org. Which one is over the 10 DNS lookup limit, and what should be fixed first?"
- **SSL:** "Which of these domains has an SSL certificate expiring in the next 30 days? example.com, example.org, example.net"
- **Contact finder:** "Find the public contact e-mail and LinkedIn page for each of these company websites: …"
- **Lazada:** "Get the top 40 results for 'air fryer' on Lazada Vietnam and Thailand, with price, discount and sold count, then show the ten with the most sold."

## Notes

- **Unofficial.** Bulk PageSpeed uses Google's public PageSpeed Insights API; it is not affiliated with or endorsed by Google. The Lazada scraper is not affiliated with or endorsed by Lazada. This project is not made by Apify.
- **Billing goes through Apify.** You need an Apify account. Runs are charged per result to that account at the prices above; nothing is billed by this repository.
- **Contact data.** The contact finder only collects addresses that websites publish on their own pages. You are responsible for using them in line with GDPR, CAN-SPAM and similar rules.
- Full documentation for each tool is on its Apify page: [apify.com/quanta1810](https://apify.com/quanta1810).

## License

MIT for the contents of this repository. See [LICENSE](LICENSE).
