# AI GTM's — Rebuilt Site

Rebuilt from screenshots of the original ai.gtms.com Wix site. Three files: `index.html`, `pricing.html`, `styles.css`. No build step, no dependencies.

## Preview locally
Just open `index.html` in a browser, or:
```bash
cd ai-gtms-site
python3 -m http.server 8000
# visit http://localhost:8000
```

## Deploy to Azure Static Web Apps (Free tier — $0/month)

### Option A: GitHub-based (recommended, 5 min)

1. **Push to GitHub**
   ```bash
   cd ai-gtms-site
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   # create empty repo on github.com, then:
   git remote add origin https://github.com/<your-user>/ai-gtms-site.git
   git push -u origin main
   ```

2. **Create the Static Web App in Azure Portal**
   - Portal → "Create a resource" → search **Static Web Apps** → Create
   - Plan: **Free**
   - Source: **GitHub** → authorize → pick your repo and `main` branch
   - Build presets: **Custom**
   - App location: `/`
   - Output location: leave blank
   - Click **Review + create** → **Create**

3. **Wait ~2 minutes.** Azure auto-generates a GitHub Action and deploys. You'll get a URL like `https://nice-pebble-12345.azurestaticapps.net` — that's your live site.

4. **Hook up ai-gtms.com**
   - In the Static Web App resource → **Custom domains** → **Add**
   - Enter `ai-gtms.com` (and `www.ai-gtms.com` as a second entry)
   - Azure gives you a CNAME/TXT record to add
   - Go to your domain registrar (Wix → Domains → DNS) and add the records
   - Wait ~15 min to 1 hr for propagation. HTTPS auto-provisions.

### Option B: Direct ZIP upload via SWA CLI
```bash
npm install -g @azure/static-web-apps-cli
swa login
swa deploy ./ai-gtms-site --env production
```

## Cost
- Free tier: 100 GB bandwidth/month, free SSL, free custom domain, free GitHub Actions builds.
- For a marketing site like this, you will not exceed the free tier.

## Edits later
Just edit the HTML/CSS, `git push` — Azure redeploys automatically in ~1 min.

## Notes on the rebuild
- The gradient waves are recreated in SVG (the original used a background image we couldn't extract). They're tunable in the `<svg class="hero-wave">` blocks.
- The logo is a simplified SVG. If you have the original PNG/SVG, drop it in and replace the `<svg>` inside `.logo-icon`.
- Footer year reads "© 2035 BY AI GTM's" to match the screenshot. Change in both HTML files if you want.
- Forms are unwired. To capture emails, point them at Formspree, Azure Functions, or any form service.
