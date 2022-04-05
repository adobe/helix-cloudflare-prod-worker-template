# helix-cloudflare-prod-worker-template

A template for a Cloudflare worker which serves as a production CDN for a Helix project.

[`src/index.mjs`](https://github.com/adobe/helix-cloudflare-prod-worker-template/blob/main/src/index.mjs) is the content of the Workers script.

## 1. Setup Cloudflare production site

Follow the instructions [here](https://www.hlx.live/docs/byo-cdn-cloudflare-setup).

## 2. Edit `wrangler.toml`

Update the following entries:

- `route` (route for your site, e.g. `*.mydomain.com/*`)
- `zone_id` (your Cloudflare Zone ID)
- `account_id` (your Cloudflare Account ID)
- `ORIGIN_HOSTNAME` (the hostname of your Helix project, e.g. `main--mysite--hlxsites.live`)

## 3. Publish your site

Install `wrangler` (if you haven't done so already);

```sh
npm i @cloudflare/wrangler -g
```

Publish your site:

```sh
npm init
wrangler publish
```

## 4. Test your site

Point your browser to your site (e.g. `https://www.mydomain.com/`).

For troubleshooting you can turn on logging in your terminal:

```sh
wrangler tail -f pretty
```
