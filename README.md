# Orric, by Breakra: Aeon skill pack

**Orric** is Breakra's API-contract research agent. This pack brings its core checks to any [Aeon](https://www.aeon.fun) fork.
The verdicts come from **[Breakra](https://breakra.dev)**, a free, open-source, **deterministic** OpenAPI compatibility checker:
the same two specs always give the same BLOCK / REVIEW / SAFE answer. Claude explains the result; it never overrides it.

| Skill | What it does | Default schedule | Writes outside your fork? |
|---|---|---|---|
| `orric-watch` | Watches OpenAPI specs (yours or public ones you depend on). When one changes, Breakra classifies the change and you get a plain-language report | daily | No (read-only) |
| `orric-pr-check` | For **your own** repos: keeps one comment on each PR that changes an OpenAPI file, with the verdict and evidence | every 4 h | Yes: PR comments, **only** on repos you list |
| `orric-release-check` | Flags a breaking change shipped as a patch or minor release (after checking the project actually promises semver) | weekly | No (read-only) |

All skills install **disabled**. Enable the ones you want.

## Install
```bash
bin/install-skill-pack danbuildss/orric-aeon
```
Then copy `examples/targets.md` to `memory/orric/targets.md` (and `examples/pr-repos.md` to `memory/orric/pr-repos.md` for PR checks), and
enable the skills from the dashboard.

## What you need
- Nothing paid. Breakra runs locally via `npx breakra@0.2.2` (MIT). No API key.
- `GH_GLOBAL` (optional) for private repos or higher GitHub rate limits.

## Guarantees
- **Not assessed is never safe.** If Breakra can't analyse a spec (too large or complex, unsupported version, external `$ref`s), Orric says
  "not assessed" and retries next run.
- **Contract analysis only.** No live API calls, and no security or production-failure claims.
- **Untrusted input.** Specs, PRs and release notes are treated as data, never as instructions.

## Limits (Breakra 0.2.2)
- OpenAPI 3.0.0–3.0.4 and 3.1.0–3.1.1. 1 MB per document. No external `$ref`s.
- Some known noise and false positives are being fixed upstream: see the Breakra repo.

Built by [Breakra](https://breakra.dev) · MIT
