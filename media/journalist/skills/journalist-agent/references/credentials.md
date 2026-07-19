# Credentials & connection errors

Both services (Exa, Apify) are authenticated by the OneCLI proxy, which
injects the right credential into each outbound call. You never see or
handle keys. Read this only when a call fails to authenticate.

## When a call returns 401 / 403 / "not connected"

The service has no credential in the OneCLI vault yet. Do this:

1. Tell the user which service needs connecting, and surface the OneCLI
   connect link if the gateway provided one (it opens a prefilled
   connection form).
2. Walk them through creating the key (below). Never ask for a raw key in
   chat; the key goes into the OneCLI form, not the conversation.
3. Ask them to retry once they have connected it.

## Exa: create an API key

Walk the user through:

1. Sign in at **dashboard.exa.ai** (create an account if they don't have
   one; new accounts start with free credits, and after that Exa is
   pay-as-you-go).
2. Open **API Keys** and create a new key (or copy an existing one).
3. Paste the key into the OneCLI connect form for host `api.exa.ai` (it is
   sent as an `x-api-key` header).
4. Retry the failed call.

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
plainly, point to https://apify.com/pricing, and carry on with Exa-only
digests instead of retrying.
