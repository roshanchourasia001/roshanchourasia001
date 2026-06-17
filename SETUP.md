# Snake Animation Setup Guide

Follow these steps to enable the contribution snake on your profile.

## Step 1 — Create the workflow file

In your profile repo (`roshanchourasia001/roshanchourasia001`), create this file:

**Path:** `.github/workflows/snake.yml`

```yaml
name: Generate Snake Animation

on:
  schedule:
    - cron: "0 0 * * *"   # runs every day at midnight
  workflow_dispatch:        # allows manual trigger
  push:
    branches:
      - main

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Generate github-contribution-grid-snake.svg
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: roshanchourasia001
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      - name: Push snake to output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Step 2 — Run it manually

1. Go to your repo on GitHub
2. Click the **Actions** tab
3. Click **Generate Snake Animation** in the left sidebar
4. Click **Run workflow** → **Run workflow**
5. Wait about 30 seconds for it to complete

## Step 3 — Verify

Visit this URL — if you see a snake SVG, it worked!

```
https://raw.githubusercontent.com/roshanchourasia001/roshanchourasia001/output/github-contribution-grid-snake-dark.svg
```

The snake now auto-updates every day automatically.
