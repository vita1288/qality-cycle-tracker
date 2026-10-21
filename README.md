# QAlity Plus Cycle Tracker (Playwright + TypeScript)

Track your own test executions in a **QAlity Plus** (Jira) test cycle — automatically.

The Playwright test pulls a test cycle from the QAlity Plus REST API, keeps only the executions assigned to one tester, resolves Jira keys and summaries, and produces:

- a console summary
- a Markdown report (`reports/cycle-<id>-<tester>.md`)
- an HTML dashboard with run history (`reports/qality-dashboard.html`)


## Features
- **Cycle lookup by name** – set `SPRINT_FILTER` (e.g. `Sprint 24`); no cycle ID needed, so it keeps working every sprint
- **Per-tester view** – filters executions by Jira assignee (display name or accountId)
- **Dashboard** – pass rate, execution progress vs. previous runs, share of the cycle, "needs attention" list, search and status filters
- **CI-friendly** – optional `FAIL_ON_FAILED=true` turns failed executions into a failing test

## Setup
```bash
npm install
npx playwright install
cp .env.example .env   # fill in your Jira + QAlity Plus tokens
npm test
npm run report         # Playwright HTML report
```
Open `reports/qality-dashboard.html` for the dashboard.

## Environment variables
| Variable | Required | Description |
|---|---|---|
| `JIRA_BASE_URL` | ✅ | Your Atlassian site, e.g. `https://your-site.atlassian.net` |
| `JIRA_EMAIL` | ✅ | Atlassian account email |
| `JIRA_API_TOKEN` | ✅ | Atlassian API token |
| `QALITY_TOKEN` | ✅ | QAlity Plus API token (Jira → Apps → QAlity Plus API Tokens) |
| `ASSIGNEE_NAME` | ✅* | Tester's Jira display name (*or `ASSIGNEE_ACCOUNT_ID`) |
| `SPRINT_FILTER` / `QALITY_CYCLE_NAME` | ✅* | Cycle name to look up (*or `QALITY_CYCLE_ID`) |
| `QALITY_APP_PATH` | – | QAlity Plus app path on your site, for "open cycle" links |
| `FAIL_ON_FAILED` | – | `true` → fail when any execution is Failed |

## Tech
Playwright Test · TypeScript · Jira Cloud REST API · QAlity Plus REST API

## Author
Jovita Sutanto — QA Engineer
