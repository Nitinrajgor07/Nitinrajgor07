# Setup Guide — GitHub Branding Kit

Follow these steps in order. The whole setup takes about 15 minutes.

## 1. Create the profile repository
GitHub profile READMEs only render if the repository name **exactly matches your username**.

1. Go to `github.com/new`
2. Repository name: `Nitinrajgor07`
3. Visibility: **Public**
4. Check "Add a README file"
5. Create repository

## 2. Upload the kit
From the root of the new repo, upload or push everything in this `GitHub-Branding-Kit/` folder so the structure looks like:

```
Nitinrajgor07/
├── README.md
├── banner.svg
├── hero.svg
├── divider.svg
├── icons/logomark.svg
├── backgrounds/grid-glow.svg
└── illustrations/network-illustration.svg
```

Via git:
```bash
git clone https://github.com/Nitinrajgor07/Nitinrajgor07.git
cd Nitinrajgor07
# copy the contents of GitHub-Branding-Kit/ into this folder
git add .
git commit -m "Add premium profile branding"
git push origin main
```

## 3. Point the SVGs at raw GitHub URLs
Once pushed, every local reference in `README.md` (e.g. `banner.svg`) will resolve automatically on your profile page because GitHub serves files from the same repo as relative paths. No changes needed if you keep the folder structure above.

## 4. Enable the live GitHub stat widgets
The README references three community-run, open-source services. They work automatically once your username is correct — no signup, no API key:

- **github-readme-stats** — stats card, top languages
- **github-readme-streak-stats** — contribution streak
- **github-readme-activity-graph** — contribution graph
- **github-profile-trophy** — trophy case

If any card shows "Error" instead of your data, it's almost always a caching delay — wait a few minutes and refresh.

## 5. (Optional) Enable the contribution snake animation
This one needs a one-time GitHub Actions setup:

1. In your `Nitinrajgor07/Nitinrajgor07` repo, go to **Settings → Secrets and variables → Actions** — no secret needed, the workflow uses the built-in token.
2. Create `.github/workflows/snake.yml`:

```yaml
name: Generate Snake
on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
  push:
    branches: [ main ]

jobs:
  generate:
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk@v3
        with:
          github_user_name: Nitinrajgor07
          outputs: |
            dist/snake.svg
            dist/snake-dark.svg?palette=github-dark
      - uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

3. Commit the workflow, run it once manually from the **Actions** tab.
4. It publishes to an `output` branch — the README already points to that branch's raw SVG.

## 6. Verify on mobile
Glass panels and gradients render correctly on GitHub's dark theme by default. Toggle GitHub's light theme once and confirm the banner still reads clearly — SVG backgrounds in this kit are self-contained dark panels, so they hold up under both.

## 7. Keep it current
Revisit the **Featured Projects**, **Research Work**, and **Current Status** sections every 4–6 weeks. A profile that visibly hasn't moved in months reads worse to a recruiter than a shorter, current one.
