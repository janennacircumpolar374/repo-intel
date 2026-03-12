# repo-intel

[![Test](https://github.com/oxnr/repo-intel/actions/workflows/test.yml/badge.svg)](https://github.com/oxnr/repo-intel/actions/workflows/test.yml)

AI-powered competitive intelligence from GitHub repos. Monitor competitor activity, releases, and strategic signals — delivered as GitHub Issues.

## Features

- **Commit velocity tracking** — detect acceleration or slowdowns
- **Release monitoring** — track shipping cadence, hotfixes, and versioning
- **Contributor analysis** — spot team growth and new contributors
- **Issue/PR throughput** — measure development health
- **Strategic signals** — HIGH/MED/LOW prioritized intelligence
- **Automated recommendations** — actionable insights per repo

## Quick Start

```yaml
# .github/workflows/repo-intel.yml
name: Competitive Intelligence
on:
  schedule:
    - cron: '0 9 * * 1'  # Every Monday at 9am
  workflow_dispatch:

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - uses: oxnr/repo-intel@v1
        with:
          repos: 'facebook/react,vercel/next.js,sveltejs/svelte'
          github-token: ${{ secrets.GITHUB_TOKEN }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `repos` | Comma-separated repos to monitor (e.g., `owner/repo`) | Yes | — |
| `github-token` | GitHub token for API access | Yes | `${{ github.token }}` |
| `output-format` | Output: `issue`, `pr-comment`, or `json` | No | `issue` |
| `period-days` | Analysis period in days | No | `7` |

## Outputs

| Output | Description |
|--------|-------------|
| `report` | Full JSON report |
| `issue-url` | URL of created issue (when `output-format: issue`) |

## Output Formats

### Issue (default)
Creates a GitHub Issue in your repo with the full intelligence digest.

### PR Comment
Posts the report as a comment on the triggering pull request.

### JSON
Outputs structured JSON for downstream consumption in your workflow.

## Live Demo

See a real report comparing React vs Vue vs Svelte: **[Demo Report](https://github.com/oxnr/repo-intel/issues/1)**

## License

MIT
