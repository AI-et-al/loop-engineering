# Dependency Sweeper Starter

Clone-and-run scaffold for the **Dependency Sweeper** pattern (L2 assisted with strong verifier gates).

Use this when you want the loop to keep your dependency surface clean and free of known high-severity vulnerabilities without you doing the boring patch/minor bumps by hand.

## Quick Start

1. Copy into your project:

   ```bash
   cp -r starters/dependency-sweeper/.grok/skills/dependency-triage .grok/skills/   # if you have a custom triage skill
   cp starters/dependency-sweeper/dependency-sweeper-state.md.example dependency-sweeper-state.md
   cp starters/dependency-sweeper/LOOP.md.example LOOP.md   # optional
   ```

2. Customize the state file with your project name and any initial denylist (e.g. your core framework during a big migration).

3. Start (example with Grok):

   ```
   /loop 6h Run dependency-triage on package manifests and lockfiles. For patch-level or low-risk CVE fixes: create minimal worktree update + verify with tests. Escalate majors, high-sev, and anything on the denylist. Update dependency-sweeper-state.md. Never auto-merge risky changes.
   ```

4. After a week of good triage quality, wire the minimal-fix + verifier from `templates/`.

5. Run `node tools/loop-audit/dist/cli.js .` regularly.

## What's Included

| File | Purpose |
|------|---------|
| `dependency-sweeper-state.md.example` | State spine (in-flight updates, human decisions) |
| `README.md` | This file |
| (recommended) Add your own `dependency-triage` skill modeled on `templates/SKILL.md.*` + the pattern doc |

## Next Steps

- Read the full pattern: [patterns/dependency-sweeper.md](../../patterns/dependency-sweeper.md)
- [Loop Design Checklist](../../docs/loop-design-checklist.md)
- Add `.github/workflows` that reacts to Dependabot PRs or scheduled scans (dogfood example in the root of this reference repo)
- After the loop is stable, consider wiring OSV-Scanner / `npm audit` / Dependabot webhooks as additional discovery sources.

**Safety note**: This pattern is deliberately biased toward *small safe patches only*. Majors and high-severity items must stay behind an explicit human gate.
