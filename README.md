# GitHub Actions Self-Hosted Runner

A small Node.js + Express app with Jest tests, used to demonstrate running a CI pipeline on a **self-hosted Windows runner**.

## Tech Stack

- Node.js 22 (ES modules)
- Express 5
- Jest 30
- GitHub Actions (self-hosted runner, Windows x64)

## Project Structure

```
github-actions-self-hosted-runner/
├── .github/workflows/
│   ├── ci.yml        # Node.js CI on GitHub-hosted ubuntu-latest
│   └── cicd.yml      # Trusted Windows CI on the self-hosted runner
├── server.js         # Express server with 2 routes
├── sum.js            # sum(a, b) function
├── sum.test.js       # Jest tests for sum()
├── jest.config.js    # Jest configuration
└── package.json
```

## Getting Started

```bash
git clone https://github.com/KARTHIKAKRISHNA123/github-actions-self-hosted-runner.git
cd github-actions-self-hosted-runner
npm ci
node server.js
```

The server runs on port 8000 by default. Change it with the `PORT` environment variable.

## API Endpoints

| Method | Route           | Description                | Example                          |
| ------ | --------------- | -------------------------- | -------------------------------- |
| GET    | `/home`         | Welcome message            | `{ "msg": "Welcome to the home page!" }` |
| GET    | `/getSum/:a/:b` | Returns the sum of a and b | `/getSum/2/3` returns `{ "ans": 5 }` |

## Running Tests

```bash
npm test
```

## Self-Hosted Runner Setup

1. In the repo, go to **Settings > Actions > Runners > New self-hosted runner** and choose **Windows x64**.
2. Follow the download and extract steps shown on that page.
3. Register and start the runner (use the token from that page):

```powershell
.\config.cmd --url https://github.com/KARTHIKAKRISHNA123/github-actions-self-hosted-runner --token <TOKEN>
.\run.cmd
```

The runner should show as **Idle** with the labels `self-hosted`, `Windows` and `X64`.

Runner files and credentials (`.credentials`, `.runner`, `bin/`, `_work/`) are listed in `.gitignore`. Never commit them.

## CI Workflows

| Workflow   | Runs on                          | Trigger                  |
| ---------- | -------------------------------- | ------------------------ |
| `cicd.yml` | `[self-hosted, Windows, X64]`    | Push to `main` only      |

`cicd.yml` steps: checkout, check that Node.js 22 is installed, `npm ci`, build if present, `npm test`.

For safety it uses read-only token permissions, does not persist git credentials, pins the checkout action to a commit SHA, cancels overlapping runs and times out after 20 minutes. It does not run on pull requests, so untrusted code never executes on the runner machine.
