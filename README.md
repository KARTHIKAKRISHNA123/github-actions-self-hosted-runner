# GitHub Actions Demo

[![Node.js CI](https://github.com/KARTHIKAKRISHNA123/github-actions-demo/actions/workflows/ci.yml/badge.svg)](https://github.com/KARTHIKAKRISHNA123/github-actions-demo/actions/workflows/ci.yml)

A small Node.js + Express app with Jest tests, used to demonstrate **continuous integration (CI) with GitHub Actions**. On every push or pull request to `main`, GitHub installs the dependencies and runs the tests automatically.

## Tech Stack

- **Node.js** (ES modules)
- **Express** for the web server
- **Jest** for testing
- **Nodemon** for auto-restart during development
- **GitHub Actions** for CI

## Project Structure

```
github-actions-demo/
├── .github/
│   └── workflows/
│       └── ci.yml        # CI workflow (Node.js CI)
├── server.js             # Express server with 2 routes
├── sum.js                # sum(a, b) function
├── sum.test.js           # Jest tests for sum()
├── jest.config.js        # Jest configuration
└── package.json
```

## Getting Started

```bash
# clone the repo
git clone https://github.com/KARTHIKAKRISHNA123/github-actions-demo.git
cd github-actions-demo

# install dependencies
npm install

# start the server (default port 8000)
node server.js

# or auto-restart on changes
npx nodemon server.js
```

## API Endpoints

| Method | Route             | Description                | Example response                       |
| ------ | ----------------- | -------------------------- | -------------------------------------- |
| GET    | `/home`           | Welcome message            | `{ "msg": "Welcome to the home page!" }` |
| GET    | `/getSum/:a/:b`   | Returns the sum of a and b | `/getSum/2/3` → `{ "ans": 5 }`         |

The port can be changed with the `PORT` environment variable.

## Running Tests

```bash
npm test
```

The tests in `sum.test.js` check that `sum()` works for positive, negative, and zero values.

## CI Workflow

The workflow in `.github/workflows/ci.yml` runs on every **push** and **pull request** to `main`:

1. Check out the code (`actions/checkout`)
2. Set up Node.js 22.x with npm caching (`actions/setup-node`)
3. Install dependencies with `npm ci`
4. Run the build if one exists (`npm run build --if-present`)
5. Run the tests with `npm test`

See the results in the **Actions** tab of the repository: a green ✅ means all tests passed, a red ❌ means something failed (open the run to read the logs).

## Author

**Karthika Krishna M** · [@KARTHIKAKRISHNA123](https://github.com/KARTHIKAKRISHNA123)
