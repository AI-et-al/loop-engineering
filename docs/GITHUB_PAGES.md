# Enable GitHub Pages

1. Repo **Settings** → **Pages**
2. **Source**: Deploy from branch `main`
3. **Folder**: `/docs`
4. Save — showcase at `https://cobusgreyling.github.io/loop-engineering/`

The homepage (`docs/index.md`) is the full interactive showcase with patterns, primitives, quick-start, and an anatomy diagram.

The root `README.md` and `LOOP.md` now describe how this reference dogfoods its own patterns via `.github/workflows/audit.yml` + `validate-patterns.yml`.

First deploy may take 1–2 minutes. After enabling, the daily scheduled audit workflow will also keep the published site "honest" about the reference's own loop readiness.

**Pro tip**: once live, run `node tools/loop-audit/dist/cli.js . --suggest` locally and improve the score over time — the workflows will reflect it.
