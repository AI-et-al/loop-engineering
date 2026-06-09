# loop-audit

CLI that scores a project's **Loop Readiness** (0–100) and suggests next steps.

## Install & Run

```bash
cd tools/loop-audit
npm install
npm run build
node dist/cli.js /path/to/your/project
```

Or from repo root after build:

```bash
node tools/loop-audit/dist/cli.js starters/minimal-loop
```

## Options

```bash
loop-audit .              # human-readable (default)
loop-audit . --json       # machine-readable
loop-audit . --md         # markdown report
loop-audit . --suggest    # show copy-from-template commands for what's missing (highly recommended)
```

Exit code `2` if score < 40 (useful for CI gates once your project is loop-ready).

The reference repo itself now ships `.github/workflows/audit.yml` that runs this on the starters + root on every PR/push.

## Signals Checked (v1.1+)

| Signal                  | Notes |
|-------------------------|-------|
| State file              | STATE.md or pattern-specific |
| Triage skill            | loop-triage / ci-triage / pr-review-triage etc. |
| Verifier skill          | maker/checker split |
| LOOP.md / config        | Cadence, limits, handoff |
| AGENTS.md / CLAUDE.md   | Project conventions |
| Safety docs             | safety.md + LOOP.md mentions of gates |
| .github/ + workflows    | Dogfooding / automation |
| MCP / connectors        | Mentions or config files |
| Worktree evidence       | Isolation patterns in docs |
| patterns/registry.yaml  | Machine index for tooling |

Weights favor state + triage + verifier + safety + .github dogfooding.

## Levels

| Level | Meaning |
|-------|---------|
| L0 | Draft — document intent |
| L1 | Report-only loops |
| L2 | Assisted auto-fix with verifier |
| L3 | Unattended-capable (with human gates) |

See [docs/loop-design-checklist.md](../../docs/loop-design-checklist.md).