# MentionFox MCP

Cited reports on any company or person, credential checks and mention scans for your AI.

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
| `get_snapshot` | Writes a one-page brief on a person, firm or publication from the public record, returned as text plus a shareable link. |
| `get_full_report` | Writes a long, section-by-section report on one subject, ending with its sources, fixed as of the day it was made. |
| `get_dossier` | Pulls together everything on file about one person: what they have done, who they work with, how they are spoken about, what they have said in public and recent news. |
| `compare_people` | Sets two to five people you have already looked up side by side in a table, framed by what the comparison is for. |
| `scan_for_mentions` | Finds posts, comments, articles and videos from the last day that mention a brand, product, topic or person, with a link, sentiment and a flag for anyone who sounds ready to buy. |
| `export_report` | Turns something you already have into a file to send: a web page, a print-ready page you can save as PDF, or plain text, with your own name, logo and colours. |
| `get_my_recent_research` | Lists the people and reports you have already researched here, so you can check before looking someone up again. |

## Links

- Developer docs: https://mentionfox.com/help/developers/mcp-server
- Pricing: https://mentionfox.com/pricing

## License

The files in this repository (this README and `server.json`) are MIT licensed. See [LICENSE](LICENSE).
