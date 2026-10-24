# hangel MCP server

Official remote [Model Context Protocol](https://modelcontextprotocol.io) server for **[hangel](https://hangel.org)**, a Turkiye-based social impact platform that brings NGOs (associations and foundations), volunteers, student clubs, brands and public institutions together.

**Server URL:** `https://hangel.org/api/mcp` · Streamable HTTP · stateless · **no authentication** (read-only, public data only)

Registry: [`org.hangel/hangel`](https://registry.modelcontextprotocol.io/v0/servers?search=org.hangel) · Server card: [/.well-known/mcp.json](https://hangel.org/.well-known/mcp.json) · Site summary for LLMs: [llms.txt](https://hangel.org/llms.txt)

## Tools

All tools are read-only and annotated with `title` and `readOnlyHint: true`.

| Tool | What it does |
|------|--------------|
| `search` | Search everything public on hangel (NGOs, events, volunteering, open grant calls, stores, products, library, pages). Returns ids for `fetch`. |
| `fetch` | Full public record for an id from `search` (`ngo:…`, `event:…`, `volunteer:…`, `fund:…`, `store:…`, `product:…`, `library:…`, `page:…`). |
| `search_ngos` | NGOs by keyword, city, cause area or minimum transparency score. |
| `list_events` | Upcoming and ongoing public events (filter by keyword, city, online). |
| `list_volunteering` | Open volunteering opportunities (filter by keyword, city, online, urgent). |
| `list_open_funds` | Grant and funding calls currently open for applications, with deadlines. |
| `search_products` | hangel Market products; buying through hangel turns a share of the price (donation rate %) into a donation to an NGO. |
| `list_stores` | Partner stores with their donation rates. |
| `search_library` | Civil-society library: legislation, templates, data, academic articles, glossary. |
| `platform_info` | What hangel is and how donation through shopping works. |

`search` and `fetch` follow the format expected by ChatGPT connectors / deep research and Claude connectors.

## Connect

**Claude (claude.ai / Desktop):** Settings → Connectors → Add custom connector → `https://hangel.org/api/mcp`

**ChatGPT:** Settings → Connectors (developer mode) → Create → `https://hangel.org/api/mcp`, authentication: none

**Claude Code:** `claude mcp add --transport http hangel https://hangel.org/api/mcp`

**Cursor / VS Code / other clients:**

```json
{ "mcpServers": { "hangel": { "url": "https://hangel.org/api/mcp" } } }
```

**Raw request:**

```sh
curl -s https://hangel.org/api/mcp -H 'Content-Type: application/json' \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"list_open_funds","arguments":{"limit":5}}}'
```

## Example prompts

- "Find animal welfare NGOs in Istanbul with a transparency score above 50."
- "Which grant calls for civil society are open this month, and when are the deadlines?"
- "Show online volunteering opportunities that need designers."
- "Find running shoes on hangel Market and tell me how much would be donated."

## Data and privacy

The server returns only information that is already public on hangel.org pages, selected through an allow-list of fields. It never returns e-mail addresses, phone numbers, street addresses, meeting links or user data. Conversations and prompts are not stored; product search terms are counted anonymously (no user identifier) for search statistics, as on the website. Requests are rate-limited per IP. Privacy policy: https://hangel.org/gizlilik-politikasi · Contact: info@hangel.org

## Note on donations

On hangel, donations happen only through shopping at partner stores (hangel Market); hangel does not collect direct cash donations. The brand name is always written in lowercase: **hangel**.

---

### Türkçe

hangel'in resmî, herkese açık MCP sunucusu: `https://hangel.org/api/mcp`. Anahtar gerekmez; yalnız hangel.org'da zaten herkese açık olan STK, etkinlik, gönüllülük, açık hibe/fon çağrısı, bağışa dönüşen mağaza/ürün ve kütüphane bilgilerini döndürür.
