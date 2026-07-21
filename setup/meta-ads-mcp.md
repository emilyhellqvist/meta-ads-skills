# Setup — Meta's Official Ads MCP {#option-a}

Meta's own MCP server, launched in open beta on April 29, 2026. Auth runs through your own Meta login — no developer app, no API key, no shared third-party credentials, and no third-party cost.

**Prerequisites:** A Meta ad account you have access to, with an admin or advertiser role in Business Manager.

## 1. Check availability

Meta is rolling this out in phases (US and higher-spend accounts first). In Business Manager, look for an **"Ads AI Connectors"** option under settings.

> 📸 Screenshot: Business Manager settings showing the "Ads AI Connectors" entry point

If it's not there yet, there's no manual override or support ticket that speeds it up — use [Windsor](windsor-mcp.md) or [Supermetrics](supermetrics-mcp.md) in the meantime and switch later.

## 2. Add the connector to your agent

**Claude Desktop**

1. Go to **Settings → Connectors** (or **Developer → MCP**).
2. Click **Add connector / Add MCP server**.
3. Paste the endpoint: `https://mcp.facebook.com/ads` (no trailing slash).

> 📸 Screenshot: Claude Desktop's Add MCP Server dialog with the endpoint pasted in

4. Complete OAuth in the browser when prompted. Select the specific ad account and Business Manager you want to connect.
5. Back in Claude Desktop, confirm the connector shows as **Connected**.

**Cursor**

Open **Settings → Tools & Integrations → New MCP Server** and add:
```json
{
  "mcpServers": {
    "meta-ads": {
      "url": "https://mcp.facebook.com/ads"
    }
  }
}
```
A "Needs Login" button will appear — click it to authorize via browser.

## 3. Verify the connection

```
What are my top 10 Meta Ads campaigns by spend in the last 30 days?
```

> 📸 Screenshot: Agent response listing real campaign names and spend

## Scopes

The official MCP inherits whatever permissions your Meta login already has in Business Manager. If write actions (pausing, budget changes) get rejected later, confirm the `ads_management` scope was granted during OAuth — some accounts are intentionally read-only until you grant it explicitly.

## Keep this in mind

- Tokens can go stale over time. If a previously-working connection suddenly returns nothing, reauthorize via Business Manager rather than assuming it's a data issue.
- The Marketing API enforces hard, points-based rate limits per app and per ad account. Space out bulk changes; don't let an agent retry aggressively on errors.
- This connector doesn't bypass Meta's standard ad review or policy enforcement — see the [account safety section](../getting-started.md#keeping-your-ad-account-safe) of the Getting Started Guide before running write actions on a production account.

## Resources

- [Meta Ads AI Connectors (official docs)](https://www.facebook.com/business/help/1456422242197840)
- [Meta Marketing API rate limits](https://developers.facebook.com/docs/marketing-api/overview/rate-limiting/)
- [Meta System User tokens](https://developers.facebook.com/docs/business-management-apis/system-users) (useful if you later move to server-to-server automation)
