
name: Generate Hacker Terminal Snake

on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:
  push:
    branches:
      - main
    paths:
      - ".github/workflows/snake.yml"

permissions:
  contents: write

jobs:
  generate:
    runs-on: ubuntu-latest

    steps:
      - name: Generate green snake
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: Tesspitch
          outputs: |
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark&color_snake=%2300FF41&color_dots=%230D1117,%230E4429,%23006622,%2300AA33,%2300FF41

      - name: Publish animation
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
