# 🔍 GitHub Repo Hunter Pro — Gemini Gem

A Gemini Gem instruction set that turns Gemini into a rigorous GitHub repository research analyst. Instead of returning a generic list of popular repos, it runs every query through an 11-step internal evaluation pipeline (maintenance health, license risk, bus factor, ecosystem strength, production readiness) before presenting a decision-ready shortlist.

## Why this exists

Searching GitHub for "best X library" usually surfaces whatever has the most stars — not what's actually maintained, licensed safely, or production-ready. This Gem was built to fix that by forcing a quality-over-popularity evaluation loop, with an internal self-refinement pass and a "why NOT to choose this" field so the recommendation is honest, not just enthusiastic.

## What it does

- Searches from multiple angles (direct topic, awesome-lists, alternative terminology) instead of a single query
- Filters out abandoned, poorly documented, or demo-only repos
- Flags license risk (GPL/AGPL/BUSL/SSPL/Elastic) and commercial-use restrictions
- Scores maintenance health, community activity, and production readiness using explicit rubrics — not vibes
- Checks **bus factor** (single maintainer vs. org-backed) — a real risk that star count alone hides
- Runs up to 2 internal refinement passes before finalizing the list
- Surfaces a "Hidden Gem" — a lower-star repo with unusually strong fundamentals
- Never fabricates stats; anything unverified is explicitly labeled "Estimated"

## Two response modes

| Mode | When it triggers | Output |
|---|---|---|
| **Compact** | Default, general queries | Rank, purpose, stars, last commit, license, production readiness, one-line verdict |
| **Full** | User says "compare", "detailed analysis", "detaylı", "derinlemesine", etc. | Full breakdown: maintenance score, community score, bus factor, ecosystem health, pros/cons, confidence level |

## How to install

1. Go to [Gemini Gems](https://gemini.google.com/gems) → **Create a new Gem**
2. Name it `GitHub Repo Hunter Pro`
3. Paste the full contents of [`gem-instructions.md`](./gem-instructions.md) into the **Instructions** field
4. Save

## Example usage

```
User: match prediction sistemi için trend git bul

Gem: [runs discovery → filtering → scoring → refinement internally]

## 1. repo-name-here
• Purpose: ...
• Stars: 4.2k
• Last Commit: 3 days ago
• License: MIT
• Production Readiness: Production Ready
• Why It Stands Out: ...

[Comparison Table]
[🔥 Hidden Gem]
[Best Repository by Use Case]
```

## Design notes

This Gem went through several iterations before landing on the current version:

- **Dropped `<thinking>` XML tags** — early drafts borrowed Claude's extended-thinking pattern, which Gemini has no hidden equivalent for; it just prints the tags literally. Replaced with a plain "do this internally, never show step labels" instruction.
- **Added a fallback rule** for when live search fails, so the model doesn't silently hallucinate stats — it must say so and mark everything "Estimated."
- **Merged release cadence into the maintenance score** instead of scoring it twice in two different formats (redundant and inconsistent).
- **Added a hard rule for the Confidence field**: if more than half the fields in a report are "Estimated," Confidence can't be rated "High." Without this, the model tended to rate confidence subjectively.
- **Compact/Full mode split** exists because the full 15-field template is overkill for a quick "find me a repo" query — it only triggers on explicit request for depth.

## License

MIT — use, modify, and redistribute freely. Attribution appreciated but not required.

## Contributing

PRs welcome, especially:
- Additional trusted trend-data sources
- Refinements to the maintenance/community scoring rubrics
- Localization of trigger phrases for other languages
