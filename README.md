# Canonical — MCP Server

> Find the companies others miss. **[Canonical](https://trycanonical.ai)** is a verified
> company graph — not a web search. Describe what you want in plain English (or pass
> structured filters) and get a precise, **LLM-verified, domain-keyed shortlist** your
> agent can act on.

This is the public home of Canonical's remote MCP (Model Context Protocol) server.
It documents the server and ships a one-click [Cursor](#cursor) plugin. The server
itself is hosted — there's nothing to run locally.

- **Server URL:** `https://trycanonical.ai/mcp`
- **Transport:** Streamable HTTP
- **Auth:** OAuth 2.0 with dynamic client registration (scope `search`) — read-only
- **Listed on:** [Official MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=ai.trycanonical/company-search) (`ai.trycanonical/company-search`) · [Smithery](https://smithery.ai/servers/canonical-ai/company-search)

## Tools

The server exposes five read-only tools:

| Tool | Purpose |
|------|---------|
| `search_companies` | Structured company search — free-text `description` plus typed filters (location, employee size, funding stage/amount/investor, founder attributes, exclusions). Unsupported constraints are reported back, never silently dropped. |
| `find_similar_companies` | Find companies similar to a seed domain. Multi-axis rerank across semantics, dimensions, funding, geo, investors, and size. |
| `get_company_details` | Full canonical profile for one company by domain, including founders/execs and their prior-employer category tags (e.g. FAANG, unicorn, MBB). |
| `lookup_companies` | Disambiguate a free-text company name to a canonical domain. Returns ranked candidates with confidence levels. |
| `get_account_status` | Credit balance, plan, and search rate limits. Read-only, charges no credits. |

## Install

On first use, your client opens Canonical's OAuth consent flow in the browser —
there's no API key to copy.

### Cursor

Install from the Cursor marketplace, or add the server manually to
`~/.cursor/mcp.json` (global) or `<project>/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "canonical": {
      "url": "https://trycanonical.ai/mcp",
      "type": "streamable-http"
    }
  }
}
```

### Claude (Desktop / Code / claude.ai)

Add a custom connector with the URL `https://trycanonical.ai/mcp` and complete the
OAuth flow. Step-by-step: https://trycanonical.ai/documentation/mcp

### VS Code (Copilot)

```json
{
  "servers": {
    "canonical": {
      "type": "http",
      "url": "https://trycanonical.ai/mcp"
    }
  }
}
```

### Any MCP client

Point it at the streamable-HTTP endpoint `https://trycanonical.ai/mcp` and authorize
via OAuth. Full client-by-client setup lives at
https://trycanonical.ai/documentation/mcp.

## Auth & pricing

- **Auth:** OAuth 2.0 with dynamic client registration (scope `search`). Read-only — no destructive operations.
- **Free tier:** 250 credits on signup, no credit card required.
- **Docs:** https://trycanonical.ai/documentation/mcp
- **Privacy:** https://trycanonical.ai/privacy-policy · **Terms:** https://trycanonical.ai/terms
- **Support:** support@trycanonical.ai

## Example prompts

- "Find fintech startups in India that raised Series A in the last 6 months."
- "Show me companies similar to stripe.com but headquartered in Europe."
- "Who are the founders of anthropic.com and where did they work before?"
- "List YC-backed B2B SaaS companies with a technical cofounder."

## Repository contents

| Path | What |
|------|------|
| `.cursor-plugin/plugin.json` | Cursor plugin manifest (makes this repo a valid Cursor plugin). |
| `mcp.json` | Remote server config — used by the Cursor plugin and copy-pasteable into any client. |

## License

MIT — see [LICENSE](./LICENSE). This license covers the contents of this repository
(manifest + docs); the Canonical service itself is operated at https://trycanonical.ai
under its own [terms](https://trycanonical.ai/terms).
