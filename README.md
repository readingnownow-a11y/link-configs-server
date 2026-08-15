# Link Configs Admin

A local GUI (runs on `localhost`) for managing the config files your Link Configs app fetches, and pushing updates to GitHub with one click.

## Prerequisites

- **Node.js** installed (check with `node -v`; any recent LTS version works)
- **Git** installed and authenticated with GitHub, so `git push` works from your terminal without prompting for a password every time (an SSH key added to your GitHub account is the easiest way — search "GitHub SSH key setup" if you haven't done this before)
- A GitHub account

## Step 1 — Create the config repo on GitHub

1. On github.com, create a new **public** repository, e.g. `link-configs-server`.
2. Initialize it with a README so it's not empty.
3. Go to **Settings → Pages**, and under "Build and deployment" choose **Deploy from a branch**, branch `main`, folder `/ (root)`. Save.
4. GitHub will give you a Pages URL like `https://YOUR_USERNAME.github.io/link-configs-server/` — note it down.

## Step 2 — Clone it locally

In a terminal, pick a folder and run:

```
git clone git@github.com:YOUR_USERNAME/link-configs-server.git
```

(If you haven't set up an SSH key yet, you can use the HTTPS clone URL instead, but you'll be prompted for credentials on every push — SSH is worth setting up once.)

Note the full path to this cloned folder — you'll need it in Step 4.

## Step 3 — Install this admin tool

Unzip this `link-configs-admin` folder anywhere on your machine, then in a terminal:

```
cd link-configs-admin
npm install
```

## Step 4 — Configure it

Copy `.env.example` to `.env`:

```
cp .env.example .env
```

Open `.env` and fill in:
- `REPO_PATH` — the full path to the repo you cloned in Step 2 (e.g. `/home/reading/link-configs-server`)
- `GITHUB_USERNAME` — your GitHub username
- `REPO_NAME` — the repo name (`link-configs-server` if you used the suggested name)

## Step 5 — Run it

```
npm start
```

Open **http://localhost:4200** in your browser.

## Using it

1. **Add a location** at the top (code, name, city — e.g. `DE`, `Germany`, `Frankfurt`).
2. Click the location card to expand it. You'll see three sections: HTTP Custom, HA Tunnel Plus, Other.
3. Under the right section, click **Choose file**, pick your file from anywhere on your computer (e.g. `weekend.hc`), then click **Upload**. It keeps the original filename and extension exactly as-is.
4. Uploading a file with the same name to the same location + VPN type again will overwrite it and bump its version number automatically.
5. When you're happy with your changes, type an optional commit message at the top and click **Push to GitHub**. This commits and pushes everything to your repo.
6. Your app fetches its manifest from:
   ```
   https://YOUR_USERNAME.github.io/link-configs-server/manifest.json
   ```
   Make sure that's the URL configured in the Android app (replacing the old placeholder domain).

## Troubleshooting

- **Push fails with an auth error** — test `git push` manually from inside your cloned repo folder in a terminal. If that fails too, it's a Git/GitHub authentication issue, not this tool.
- **"REPO_PATH is missing or does not exist"** on startup — double check the path in `.env` is correct and the repo was actually cloned there.
- **New files don't show up in the app** — GitHub Pages can take a minute or two to update after a push. Try refreshing `https://YOUR_USERNAME.github.io/link-configs-server/manifest.json` directly in a browser first to confirm the push landed.
