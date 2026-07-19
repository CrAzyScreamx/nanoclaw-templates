# Credentials & connection errors

The Apify X scraper is authenticated by the OneCLI proxy, which injects
the credential into each outbound call. You never see or handle keys.
Read this only when a call fails to authenticate.

## When a call returns 401 / 403 / "not connected"

The service has no credential in the OneCLI vault yet. Do this:

1. Tell the user Apify needs connecting, and surface the OneCLI connect
   link if the gateway provided one (it opens a prefilled connection
   form).
2. Walk them through copying the token (below). Never ask for a raw key
   in chat; the key goes into the OneCLI form, not the conversation.
3. Ask them to retry once they have connected it.

## Apify: copy the API token

Walk the user through:

1. Sign in at **console.apify.com**.
2. Go to **Settings > API & Integrations** and copy the personal API token.
3. Paste it into the OneCLI connect form for host `api.apify.com` (it is
   sent as `Authorization: Bearer`).
4. Retry the failed call.

One caution: `.mcp.json` sets `APIFY_TOKEN: "placeholder"` only so the MCP
server can boot. That placeholder is not the credential and must never be
replaced with a real token; the real token lives only in the OneCLI vault.

Plan limits: the X actor does not run on Apify's free plan (the token will
authenticate but the actor refuses the run). If that happens, say it
plainly, point to https://apify.com/pricing, and carry on with web-only
digests instead of retrying.
