# AGENTS.md

Guidance for Codex when working in this repository.

## About

Oracle knowledgebase static site published from GitHub repo `pp-nextgen-dba/oracle`.

## Local Workflow

Work from:

```powershell
cd C:\codex\oracle
```

Check status:

```powershell
git status --short --branch
```

Commit and push:

```powershell
git add .
git commit -m "Describe the Oracle update"
git push
```

## Project Structure

| Path | Purpose |
|---|---|
| `index.html` | Main Oracle knowledgebase page served by GitHub Pages |
| `reports/repo-report.html` | Repository summary report |
| `README.md` | Repository overview |

## Preferences

- Keep responses short and direct.
- Keep the site static unless a build step is clearly needed.
- Use PowerShell commands on Windows.
- Do not commit passwords, wallets, connection strings, hostnames, usernames, customer details, or server-specific information.
- For Python Oracle examples, prefer `oracledb` thin mode.
