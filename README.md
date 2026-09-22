# Bowls Club App — Demo Preview (capped build)

This is a **deliberately limited preview** of the Bowls Availability &
Selection app, meant to be shared publicly (on club websites, forums,
Facebook groups, your Etsy listing) so people can try it before they buy.

It is **not** the product itself — see `bowls-club-app` (single-file) or
`bowls-club-app-cloud` (with shared cloud storage) for the real thing.

## What's capped here, and why it's safe to share publicly

- Max 3 rinks, 1 fixture, 2 leagues, 2 club officers, 1 maintenance slot,
  3 active rink bookings at a time — enough to click around every screen
  without it turning into a fully-populated club system.
- A red "DEMO PREVIEW" banner is shown on every screen, and a
  "What can this app do?" link on the login screen opens a short explainer.
- **All data lives only in the visitor's own browser tab** — there is no
  shared backend, database, or Azure Storage Account behind this build.
  Every visitor gets their own private, blank-slate copy the moment they
  open the page, and a page reload resets it. Multiple clubs can try it
  at the same time, or one after another, without ever seeing each
  other's data — there's nothing to "clear" between visitors because
  nothing persists in the first place.

## Deploying — GitHub + Azure Static Web Apps (no Storage Account needed)

**1. Push this folder to a new GitHub repository**

```bash
cd bowls-club-app-demo
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

**2. Create the Azure Static Web App**

- In the Azure Portal, create a new **Static Web App** resource, **Free plan**.
- Link it to the GitHub repo/branch you just pushed.
- Build details:
  - **Build presets:** Custom
  - **App location:** `src`
  - **Api location:** *(leave blank)*
  - **Output location:** *(leave blank)*
- Create it — Azure wires up the GitHub Actions deployment (the workflow
  file is already included here) and the first build/deploy starts
  automatically.

**3. Share the link**

Once deployed, Azure gives you a URL like
`https://<random-name>.azurestaticapps.net`. That's the link to put on
club websites, forums, or your Etsy listing — a proper URL rather than a
Claude artifact link, and not tied to your Claude account.

Updating the demo later (new wording, a tweaked cap) is the same as the
other two apps: edit `src/index.html`, commit and push (or drag-and-drop
a replacement file into the repo on github.com) — Azure redeploys
automatically within a minute or two.

## Project structure

```
bowls-club-app-demo/
├── src/
│   ├── index.html                      the capped demo app
│   └── staticwebapp.config.json        Azure Static Web Apps routing config
├── .github/workflows/
│   └── azure-static-web-apps.yml       CI/CD: deploy on every push to main
└── README.md
```

## License

© All rights reserved. This code is not licensed for redistribution or
resale by anyone other than the copyright holder.
