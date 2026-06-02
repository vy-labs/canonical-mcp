# Installation guide for AI agents (Cline, etc.)

This is a **hosted, remote MCP server**. There is **nothing to clone, build, or run
locally** — you only need to register the remote endpoint in the MCP client's config.
There are **no API keys or environment variables**; authentication is OAuth 2.0 and is
handled interactively in the browser on first use.

## Steps

1. Add the following server to the client's MCP settings (for Cline, this is
   `cline_mcp_settings.json`; merge into any existing `mcpServers` object):

   ```json
   {
     "mcpServers": {
       "canonical": {
         "type": "streamableHttp",
         "url": "https://trycanonical.ai/mcp"
       }
     }
   }
   ```

   Notes:
   - Transport is **Streamable HTTP**. If the client uses a different key for remote
     servers, use that client's remote/streamable-HTTP field with the same `url`.
   - Do **not** set `command`, `args`, or `env` — this is a remote server, not a local process.

2. Save the config and let the client connect. On the first tool call, the client will
   open Canonical's **OAuth consent** page in the browser. Approve it to authorize.
   (Free tier: 250 credits on signup, no credit card.)

3. Verify the connection by calling the free, read-only tool **`get_account_status`** —
   it returns the account's credit balance, plan, and rate limits without spending credits.

## Available tools (all read-only)

- `search_companies` — structured company search (free-text description + typed filters).
- `find_similar_companies` — find look-alikes of a seed company by domain.
- `get_company_details` — full profile for one company by domain.
- `lookup_companies` — disambiguate a free-text company name to a canonical domain.
- `get_account_status` — credit balance, plan, and rate limits (free; charges no credits).

## Troubleshooting

- **401 / authorization prompt loops:** ensure the client supports OAuth 2.0 with dynamic
  client registration and that a browser is available to complete the consent flow.
- **No tools listed before auth:** tool discovery requires an authorized session; complete
  the OAuth consent first, then re-list tools.
- Docs: https://trycanonical.ai/documentation/mcp
