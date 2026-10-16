# Continuation Handoff

## Resume point

This bundle contains planning and engineering-governance documents only. No
product source code, infrastructure, proof of concept, or benchmark has been
created.

Start by reading:

1. `AGENTS.md`
2. `implementation-plan-nishant-tution.md`
3. `HLD.md`
4. `LLD.md`
5. `project-progress-checklist.md`
6. `docs/planning/gate-zero-closure-plan.md`

The next recommended activity is a Gate 0 decision workshop and decision
register. Do not start implementation merely because the repository has been
moved or opened in a new account.

Suggested first prompt:

> Read AGENTS.md, the four root planning documents, and
> docs/planning/gate-zero-closure-plan.md. Continue at Gate 0. Present the
> unresolved decisions in dependency order and ask me to approve them in small
> groups. Do not implement product code, infrastructure, prototypes, or
> benchmarks without separate explicit approval.

## Move to another Linux, macOS, or WSL system

Copy both the archive and its `.sha256` file, then verify and extract:

```bash
sha256sum -c secure-coaching-content-portal-transfer.tar.gz.sha256
mkdir -p ~/personal
tar -xzf secure-coaching-content-portal-transfer.tar.gz -C ~/personal
cd ~/personal/secure-coaching-content-portal
```

Install Cursor CLI if necessary:

```bash
curl https://cursor.com/install -fsS | bash
export PATH="$HOME/.local/bin:$PATH"
agent --version
```

Authenticate with the account that should own the new session:

```bash
agent status
agent login
agent status
```

Start from the extracted project root:

```bash
cd ~/personal/secure-coaching-content-portal
agent
```

Alternatively, specify the workspace explicitly:

```bash
agent --workspace ~/personal/secure-coaching-content-portal
```

Cursor automatically discovers root and nested `AGENTS.md` files and project
rules under `.cursor/rules/**/*.mdc`. The archive therefore must preserve the
hidden `.cursor` directory.

## Windows PowerShell

```powershell
irm 'https://cursor.com/install?win32=true' | iex
agent login
Set-Location 'C:\path\to\secure-coaching-content-portal'
agent
```

## After extraction

Confirm that these hidden rules are present:

```bash
ls -la .cursor/rules
```

The local Git repository is initialized on `main`, with
`https://github.com/itzRJ/Secure-Coaching-Content-Portal.git` as `origin`.
Branch protection, GitHub Actions workflows, and implementation remain future
explicitly approved work.
