# argus-codescan (npm)

Security scanner for **React, Next.js, and Node** projects. Works on **Windows, macOS, and Linux** — no Python, no Homebrew, no manual tool installs.

npm: https://www.npmjs.com/package/argus-codescan

## Install

```bash
npm install -D argus-codescan
```

## Usage

```bash
npx argus-codescan scan sca .       # dependencies (npm audit)
npx argus-codescan scan sast .      # source code (JS/TS)
npx argus-codescan scan secrets .   # API keys, tokens
npx argus-codescan scan all .       # everything
npx argus-codescan tools            # show bundled scanners
```

Every scan **writes a CSV report** automatically. Set a custom path:

```bash
npx argus-codescan scan all . --output ./reports/security.csv
npx argus-codescan scan sast . --no-csv          # skip CSV file
npx argus-codescan scan all . --format json      # JSON to terminal
npx argus-codescan scan all . --fail-on high     # exit 1 for CI
```

## React / Next.js project setup

Add to `package.json`:

```json
{
  "devDependencies": {
    "argus-codescan": "^0.4.4"
  },
  "scripts": {
    "security:scan": "argus-codescan scan sca . --output ./reports/deps.csv",
    "security:code": "argus-codescan scan sast . --output ./reports/code.csv",
    "security:secrets": "argus-codescan scan secrets . --output ./reports/secrets.csv",
    "security:all": "argus-codescan scan all . --output ./reports/full.csv"
  }
}
```

Then run:

```bash
npm run security:all
```

## What runs automatically (bundled)

| Scanner | What it checks |
|---------|----------------|
| **argus-native** | JS/TS patterns — SQLi, XSS, injection, weak crypto |
| **eslint-security** | JavaScript / JSX security rules |
| **opengrep** | Auto-downloads on first SAST scan (Semgrep-compatible, no pip) |
| **argus-secrets** | Hardcoded API keys, passwords, private keys |
| **npm audit** | Dependency vulnerabilities |

## Java, PHP, Flutter, Terraform?

Use the **Python** package instead (npm is for Node/React only):

```bash
pip install argus-languages
argus-languages scan /path/to/flutter-app
```

Or the full suite:

```bash
pip install argus-scan
argus scan code /path/to/project
```

## Optional (not required)

- **Gitleaks** — deeper secret scanning if installed from [gitleaks.io](https://github.com/gitleaks/gitleaks)
- **semgrep** (pip) — used instead of opengrep if already on PATH

The package works fully without these.
