# helix-cloudflare-prod-worker-template

A template for a Cloudflare worker which serves as a production CDN for an AEM project.

[`src/index.mjs`](https://github.com/adobe/helix-cloudflare-prod-worker-template/blob/main/src/index.mjs) is the content of the Workers script.

## 1. Setup Cloudflare production site

Follow the instructions [here](https://www.aem.live/docs/byo-cdn-cloudflare-setup).

## 2. Edit `wrangler.toml`

Update the following entries:

- `route` (route for your site, e.g. `*.mydomain.com/*`)
- `zone_id` (your Cloudflare Zone ID)
- `account_id` (your Cloudflare Account ID)
- `ORIGIN_HOSTNAME` (the hostname of your AEM project, e.g. `main--mysite--hlxsites.aem.live`)

To find your `account_id` and `zone_id` visit the [Websites Dashboard](https://dash.cloudflare.com/zones) in Cloudflare, select your site they will be listed on the right hand side of the dashboard under `API`.

## 3. Configure push invalidation (optional)

If you have succesfully configured [push invalidation](https://www.aem.live/docs/setup-byo-cdn-push-invalidation#cloudflare) for your project your worker should send the following opt-in header:

```
X-Push-Invalidation: enabled
```

All you have to do is set the `PUSH_INVALIDATION` environment variable in the Cloudflare dashboard to `enabled` or do the same via wrangler.

## 4. Enable Origin Authentication (optional)

If you have enabled [Site Authentication](https://www.aem.live/docs/authentication-setup-site) for your project your worker should send the following header:

```
Authorization: token <token>
```

All you have to do is set the `ORIGIN_AUTHENTICATION` environment variable in the Cloudflare dashboard to the token you have configured in your AEM project or do the same via wrangler.

## 5. Deploy your site

Install `wrangler` (if you haven't done so already):

```sh
npm i @cloudflare/wrangler -g
```

Publish your site:

```sh
wrangler deploy
```

## 5. Test your site

Point your browser to your site (e.g. `https://www.mydomain.com/`).

For troubleshooting you can turn on logging in your terminal:

```sh
wrangler tail -f pretty
```
