---
name: update-github-info
on:
  schedule:
    - cron: "0 9 * * *"
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
engine: copilot
model: gpt-4.1
tools:
  github:
    toolsets: [context, repos, pull_requests]
  web-fetch:
  edit:
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com   
safe-outputs:
  create-pull-request:
    max: 1
    draft: true
    reviewers: [Mona]
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Keep the GitHub Info website current with concise, practical updates from official GitHub sources.

## Instructions

1. Read `notes/mona-notes.md` and `site/content/github-info.md` before making changes.
2. Read any repository guidance or reference files you need with GitHub repository API tools. Do not use the terminal, GitHub CLI, or sandboxed commands for that repository reading.
3. Fetch and read `https://github.blog/latest/` with the web-fetch tool.
4. Fetch and read `https://github.blog/changelog/` with the web-fetch tool.
5. Fetch and read `https://awesome-copilot.github.com/workflows/` with the web-fetch tool.
6. Select at least one useful, current item that fits Mona's editorial angle and make a concrete update on every run. Keep summaries short and practical, avoid duplicating existing entries, and mention the official source for every new or refreshed item. If there is no new item, refresh an existing entry with a current source-backed detail; do not finish without modifying the content file.
7. Update only `site/content/github-info.md` with the selected information. Preserve its existing structure and editorial tone.
8. Request the `create-pull-request` safe output with a concise title and body summarizing the sources and changes. The pull request body must include a `Sources` section with the exact URLs `https://github.blog/latest/`, `https://github.blog/changelog/`, and `https://awesome-copilot.github.com/workflows/`, plus a brief explanation of which source informed each change. Open the pull request for Mona to review; do not write directly to the default branch.
