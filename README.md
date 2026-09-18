# Awesome Agent APIs

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

A catalog of API tools an agent can call — 660+ generative-media models available
through [muapi](https://muapi.ai) out of the box, plus a growing set of third-party
tools (SEO, enrichment, social, scraping, and more) that anyone can add with a
single PR.

This is a **reference catalog, not a live proxy**. Every entry is documentation —
what a tool does, what it costs, how to call it — not something this repo calls
for you. `models/` entries run through your own muapi key; `providers/` entries
run through the contributor's own account with that provider.

**Agents:** read [`llms.txt`](llms.txt) — one fetch teaches you how to browse and
use this whole catalog, no install or auth required.

## Why this exists

The tools worth calling from an agent are scattered across dozens of vendors, each
with its own docs, auth quirks, and pricing page — and most of the useful ones sit
behind a subscription nobody buys for a single call (Semrush $139/mo, Moz $99/mo,
Crunchbase $99/mo), or behind docs vague enough that you don't know what a call
actually costs or returns until you've already signed up. This catalog puts the
facts that matter — auth shape, real pricing, a captured example response — in one
consistent shape, so an agent (or a person) can scan it and know exactly what a
tool needs before ever opening its docs.

## Two kinds of entry

| | `models/*.yaml` | `providers/*.yaml` |
|---|---|---|
| What it is | One of muapi's own hosted generative-media models | A third-party API a contributor already uses |
| Called with | Your muapi API key | The contributor's/your own key for that provider |
| Who adds it | Auto-synced from muapi's live catalog | Anyone, via PR |
| Editable by PR? | No — see "muapi-hosted models" below | Yes — this is the open contribution path |

## Quickstart

```bash
ls providers/ models/            # browse what's catalogued
cat capabilities.yaml            # browse by category instead — media.*, seo.*, people.*, ...
cat providers/<provider>.yaml    # base_url, auth, endpoints, pricing for a third-party tool
cat models/<model>.yaml          # what a muapi-hosted model does, its cost, its docs page
```

## Add a third-party tool
- [Continuum-AI-Corp/OrcaReplay](https://github.com/Continuum-AI-Corp/OrcaReplay) — record & replay AI coding-agent runs offline.

1. Copy `providers/_TEMPLATE.yaml` to `providers/<your-provider>.yaml`.
2. Fill it in against the provider's own public docs — see `CONTRIBUTING.md` for the
   full checklist, including the one non-negotiable step: **get a real key and
   confirm at least one endpoint actually works before opening the PR.** A schema
   that was never called against the real API is not accepted.
3. Run the validator locally:
   ```bash
   python3 scripts/catalog_validate.py providers/<your-provider>.yaml
   ```
4. Open a PR. A maintainer reviews the entry and, once confirmed, flips its
   `status` to `verified`.

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for the full guide, including selection
heuristics (what gets accepted vs. rejected) and common gotchas per auth style.

## muapi-hosted models (`models/`)

These entries are generated directly from muapi's own live catalog — not hand-written,
and not open to arbitrary edits, since they describe what muapi itself already runs.
Each one deliberately omits how muapi actually serves the model (no `base_url`, no
auth details, no vendor name) — only the model itself, its cost, and a link to its
docs page. Missing a model, or see one that's wrong? Open an issue rather than a PR;
the catalog is refreshed from the source of truth periodically.

## Entry statuses

- `draft` (providers only) — submitted, not yet independently verified by a maintainer.
- `verified` (providers only) — a maintainer confirmed the entry against a real key
  and a real call; `examples/<id>.json` holds a real captured response.
- `live` (models only) — currently available through muapi.

Treat `draft` entries as a starting point, not a guarantee — verify before relying
on one yourself.

## Scope (providers/)

- **In scope:** any tool with a self-serve API key (no sales call, no partner
  application) — SEO/backlinks, keyword/rank data, people/company enrichment,
  scraping, social/publishing, ads, market data, and similar.
- **Out of scope:** anything requiring a sales process, an enterprise-only tier
  with no public pricing, or a tool that's deprecated/no longer self-serve.

## Related Projects

- [MuAPI](https://muapi.ai) — Unified API for image, video, and audio generation across hundreds of AI models.
- [MuAPI agent skills docs](https://muapi.ai/docs/agent-skills) — How MuAPI's own skills/tool-catalog surface works for agents.
- [MuAPI access keys](https://muapi.ai/access-keys) — Create a key if you're pairing this catalog with MuAPI's own generative-media API.
- [awesome-jev-by-typesafe](https://github.com/Anil-matcha/awesome-jev-by-typesafe) — Typed, confidence-aware decision workflows for routing agents and API tools.

## License

MIT — see [LICENSE](LICENSE).
