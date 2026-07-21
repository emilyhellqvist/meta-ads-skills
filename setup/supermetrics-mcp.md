# Setup — Supermetrics MCP

If you're already using Supermetrics for reporting, this adds live Meta Ads data to your AI agent in a few steps. Supermetrics also supports write actions (budget/bid/campaign changes), not just read-only analytics.

## 1. Connect Meta Ads in Supermetrics Hub

1. Go to [hub.supermetrics.com](https://hub.supermetrics.com) and log in.
2. Navigate to **Data Sources** and click **Add connection**.
3. Select **Meta Ads** and sign in with your Meta account.
4. Grant access and select your ad account(s) — Business Manager-level connections are supported.

> 📸 Screenshot: Supermetrics Hub Data Sources page showing Meta Ads listed as connected

## 2. Get your Supermetrics API key

1. In the Hub, go to **Settings → API Keys** (or **Profile → API Keys**).
2. Click **Generate new key**.
3. Copy it immediately and store it somewhere safe — it won't be shown again.

> 📸 Screenshot: API Keys page with "Generate new key" button

## 3. Connect to your AI agent

**Claude.ai (web)**

1. Go to **Settings → Integrations**, search for **Supermetrics**.
2. Click **Add** and authenticate.

**Claude Desktop or Cursor**

```json
{
  "mcpServers": {
    "supermetrics": {
      "url": "https://mcp.supermetrics.com/mcp",
      "headers": {
        "Authorization": "Api-Key YOUR_SUPERMETRICS_API_KEY"
      }
    }
  }
}
```

> 📸 Screenshot: Agent showing Supermetrics MCP active, with an example Meta Ads query response

## 4. Verify Supermetrics is connected

```
What data sources do I have connected in Supermetrics?
```

## Resources

- [hub.supermetrics.com](https://hub.supermetrics.com)
