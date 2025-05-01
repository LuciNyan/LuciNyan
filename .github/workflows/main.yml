name: generate-and-upload-card

on:
  # run automatically every 24 hours
  schedule:
    - cron: "0 */24 * * *"

  # allows to manually run the job at any time
  workflow_dispatch:

  # run on every push on the master branch
  push:
    branches:
    - master

jobs:
  generate:
    permissions:
      contents: write
    runs-on: ubuntu-latest
    timeout-minutes: 5

    steps:
      - name: generate github stats card
        uses: LuciNyan/pixel-profile/action@main
        with:
          outputs: |
            dist/github-stats?username=LuciNyan&screen_effect=false&theme=fuji&dithering=true&hide=avatar
            dist/github-stats-dark?username=LuciNyan&theme=crt

      # push the content of <build_dir> to a branch
      # the content will be available at https://raw.githubusercontent.com/<github_user>/<repository>/<target_branch>/<file> , or as github page
      - name: push github-contribution-grid-snake.svg to the output branch
        uses: crazy-max/ghaction-github-pages@v3.1.0
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
