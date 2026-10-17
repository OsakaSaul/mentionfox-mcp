# MentionFox MCP

Research on people and companies inside your AI assistant, with every claim cited: one-page briefs, full reports, credential checks, contact details and mention scans. New: find buyers now. Paste a website and get companies with a filed reason to buy this month (funding, new executives, IPO filings, layoffs), each with its record link. A free MentionFox account works; plans are at [mentionfox.com/pricing](https://mentionfox.com/pricing?utm_source=github_readme&utm_medium=mcp_listing).

![MentionFox](https://mentionfox.com/launch/lp-1280x800.png)

## Endpoint

```
https://mentionfox.com/mcp
```

- Transport: streamable HTTP
- Remote server: nothing to install or run locally. Point your AI client at the URL above.
- Sign-in: OAuth. The first time your client connects, it opens a MentionFox sign-in page in your browser; approve it and you're connected. Clients that can't do OAuth can send a personal access key instead (create one at https://mentionfox.com/dashboard/mcp-token) as an `Authorization: Bearer <your key>` header.

Usage is tied to your MentionFox account, the same as using the dashboard.

## Connect

### Claude (claude.ai and Claude Desktop)

1. Open **Settings > Connectors**.
2. Choose **Add custom connector**.
3. Name it `MentionFox` and paste the URL `https://mentionfox.com/mcp`.
4. Click **Connect** and sign in to MentionFox when prompted.

### Claude Code

From a terminal:

```
claude mcp add --transport http mentionfox https://mentionfox.com/mcp
```

Or add it to a project's `.mcp.json`:

```json
{
  "mcpServers": {
    "mentionfox": {
      "type": "http",
      "url": "https://mentionfox.com/mcp"
    }
  }
}
```

Then run `/mcp` inside Claude Code and choose **Authenticate** for mentionfox.

### ChatGPT

1. Open **Settings > Apps & Connectors**.
2. Under **Advanced settings**, turn on **Developer mode**.
3. Choose **Create**, name it `MentionFox`, paste `https://mentionfox.com/mcp` as the server URL and pick OAuth for authentication.
4. Save, then sign in to MentionFox when prompted.

If you call OpenAI's Responses API directly, the MCP tool entry looks like this (use a personal access key as the authorization value):

```json
{
  "type": "mcp",
  "server_label": "mentionfox",
  "server_url": "https://mentionfox.com/mcp",
  "authorization": "<your MentionFox personal access key>",
  "require_approval": "always"
}
```

### Cursor

Add this to `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project):

```json
{
  "mcpServers": {
    "mentionfox": {
      "url": "https://mentionfox.com/mcp"
    }
  }
}
```

Cursor will ask you to sign in to MentionFox the first time a tool is used. To use a personal access key instead:

```json
{
  "mcpServers": {
    "mentionfox": {
      "url": "https://mentionfox.com/mcp",
      "headers": {
        "Authorization": "Bearer <your MentionFox personal access key>"
      }
    }
  }
}
```

## Tools

These are the tools the server returns from `tools/list`:

| Tool | What it does |
| --- | --- |
| `source_check` | Checks the credentials someone claims (doctor, lawyer, broker, professor, company director) against the official lists that would record them, and answers verified, partly verified, could not verify, or contradicted by the record, with a link for each claim. |
| `enrich_person` | Finds how to reach a person you can already name: their email address, phone number where there is one, current role and profile links. |
| `get_snapshot` | Writes a one-page brief on a person, firm or publication, every claim cited, returned as text plus a shareable link. |
| `get_full_report` | Writes a long, section-by-section report on one subject, ending with its sources, fixed as of the day it was made. |
| `get_dossier` | Pulls together everything on file about one person: what they have done, who they work with, how they are spoken about, what they have said and recent news. |
| `compare_people` | Sets two to five people you have already looked up side by side in a table, framed by what the comparison is for. |
| `scan_for_mentions` | Finds posts, comments, articles and videos from the last day that mention a brand, product, topic or person, with a link, sentiment and a flag for anyone who sounds ready to buy. |
| `export_report` | Turns something you already have into a file to send: a web page, a print-ready page you can save as PDF, or plain text, with your own name, logo and colours. |
| `get_my_recent_research` | Lists the people and reports you have already researched here, so you can check before looking someone up again. |
| `find_buyers_now` | Give the website of the business you sell for and get up to 10 US companies with a filed reason to buy from you now: new funding filings, a new chief executive or other senior hire, IPO filings, activist stakes, layoff filings and notices, crowdfunding raises and new Y Combinator companies. Each one comes with the record it came from, a why-now line written from that record and a note on why it fits what you sell. Costs 1 credit when companies come back, nothing when none do. Try it free at [mentionfox.com/buyers](https://mentionfox.com/buyers?utm_source=github_readme&utm_medium=mcp_listing). |

## Links

- Developer docs: https://mentionfox.com/help/developers/mcp-server?utm_source=github_readme&utm_medium=mcp_listing
- Pricing: https://mentionfox.com/pricing?utm_source=github_readme&utm_medium=mcp_listing

## License

The files in this repository (this README and `server.json`) are MIT licensed. See [LICENSE](LICENSE).
