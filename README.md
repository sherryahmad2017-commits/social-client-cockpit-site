# Social Client Cockpit — landing page

Static marketing site for the [Social Client Cockpit](../social-client-cockpit) Chrome extension. No build step, no framework — plain HTML/CSS served by a small dependency-free Node server (`server.js`), which is what Railway runs in production.

## Run it locally

Requires Node.js 18+.

```
npm start
```

Then open http://localhost:3000. (No `npm install` needed — there are zero dependencies.)

## Project structure

```
public/            served as-is
  index.html        the landing page
  styles.css
  404.html
  images/            screenshots + icon
server.js           tiny static file server (reads PORT from env)
package.json         "start": "node server.js"
railway.json         explicit Nixpacks build/start config for Railway
mockups/              source HTML used to render the screenshots in public/images (not deployed)
```

## Deploy on Railway

1. Push this repo to GitHub (already done if you're reading this from the repo).
2. Go to [railway.app](https://railway.app) → **New Project** → **Deploy from GitHub repo** → select `social-client-cockpit-site`.
3. Railway detects `package.json` via Nixpacks and runs `node server.js` automatically (see `railway.json`). No environment variables are required — the server reads `PORT` from Railway automatically.
4. Once deployed, go to the service's **Settings → Networking** and click **Generate Domain** to get a public `*.up.railway.app` URL (or attach your own custom domain there).
5. Every future push to the connected branch redeploys automatically.

## Updating screenshots

The screenshots in `public/images/` are real renders of the extension's actual popup/options/overlay HTML+CSS (copied from the extension project) with sample data, captured via headless Chrome — not hand-drawn mockups. Source files are in `mockups/`. To regenerate after a UI change in the extension:

1. Copy the updated CSS from the extension project into `mockups/`.
2. Update the sample data in `mockups/*.html` if fields changed.
3. Re-screenshot with headless Chrome and re-crop, then copy into `public/images/`.
