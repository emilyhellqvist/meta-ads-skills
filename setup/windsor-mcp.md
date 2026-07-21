# Setup — Windsor MCP

Windsor connects your Meta Ads account to your AI agent in about 10 minutes. No API tokens, no config files. Also works if Meta's official MCP isn't rolled out to your account yet.

## 1. Create a Windsor account

1. Go to [onboard.windsor.ai](https://onboard.windsor.ai) and sign up.
2. Start the free trial — no credit card required.

> 📸 Screenshot: Windsor homepage sign-up form

## 2. Connect Meta Ads

1. Inside Windsor, click **Add Data Source**.
2. Select **Meta Ads (Facebook/Instagram)** from the list.

> 📸 Screenshot: Windsor "Add Data Source" screen with Meta Ads highlighted

3. Click **Connect** and sign in with your Meta account.
4. Authorize the requested permissions.
5. Select which ad account(s) to include — you can select your whole Business Manager to cover multiple accounts at once.

> 📸 Screenshot: Meta OAuth authorization screen, then Windsor showing connected ad accounts

## 3. Connect Windsor to your AI agent

**Claude.ai (web app)**

1. Go to **Settings → Integrations**.
2. Search for **Windsor.ai**, click **Add**, and authorize with your Windsor account.
3. Set the permission level to **Always allow** for faster responses.

**Claude Desktop**

Edit `~/Library/Application Support/Claude/claude_desktop_config.json` and add:
```json
{
  "mcpServers": {
    "windsor": {
      "command": "mcp-proxy",
      "args": ["https://mcp.windsor.ai/", "--transport=streamablehttp"],
      "env": {
        "API_ACCESS_TOKEN": "YOUR_WINDSOR_API_KEY"
      }
    }
  }
}
```
First install `mcp-proxy`:
```bash
uv tool install mcp-proxy
```

**Cursor**

```json
{
  "mcpServers": {
    "windsor": {
      "url": "https://mcp.windsor.ai/"
    }
  }
}
```
Click the "Needs Login" button that appears to authorize via browser.

## 4. Verify Windsor is connected

```
What data sources do I have connected in Windsor?
```
You should see your Meta Ads account(s) listed in the response.

## Resources

- [windsor.ai](https://windsor.ai)
- [Windsor Claude integration guide](https://windsor.ai/documentation/windsor-mcp/how-to-integrate-data-into-claude/)
