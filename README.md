name: Metrics Dashboard

on:
  schedule:
    - cron: "0 0 * * *"    # refreshes once a day
  workflow_dispatch:        # lets you trigger it manually anytime

jobs:
  build-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: lowlighter/metrics@latest
        with:
          filename: metrics.svg
          token: ${{ secrets.METRICS_TOKEN }}
          user: ashwithachandru
          template: classic
          base: header, activity, community, repositories, metadata
          config_timezone: Asia/Kolkata

          # ---- Languages breakdown ----
          plugin_languages: yes
          plugin_languages_analysis_timeout: 15
          plugin_languages_limit: 8
          plugin_languages_threshold: 0%

          # ---- Isometric contribution calendar (the unique bit) ----
          plugin_isocalendar: yes
          plugin_isocalendar_duration: full-year

          config_display: large
