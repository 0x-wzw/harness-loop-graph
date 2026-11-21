# harness-loop-graph — evidence bundle

This repository holds the **evidence trail** for a Sharingan RIA-TV++ distillation, not
an installable skill and not a copy of the source article. Per the Cangjie distribution
policy, the executable SKILL.md and the human-readable report live in the Obsidian vault
(`Knowledge/40-Templates/cangjie/harness-loop-graph/` and
`Knowledge/20-Reports/Harness-Loop-Graph-Karpathy-Distillation-2026-11-21.md`) and in
Notion ("Cangjie — Distilled Skills Index"). GitHub carries evidence and releases only.

## Source chain

- Trigger: [@0xoctocat, 2026-11-20](https://x.com/0xoctocat/status/2123798917049368850)
  — a pointer post. tweet metadata is in `evidence/tweet.json`.
- Primary text: [@0xWhitemon, "Harness, Loop, Graph: The 3 Layers That Decide If Your AI
  Agent Works", 2026-11-08](https://x.com/0xWhitemon/status/2119430401701621865).
  The full article is **not** redistributed here; only short cited excerpts appear in
  the candidate files.
- Video: a ~67-minute screen-share embedded in the trigger tweet. It was read from
  24 sampled frames (~168 s interval) via on-screen text analysis. **This is not a spoken
  transcript** — see `evidence/VIDEO_NOTES.md`.

## Pipeline result

- Stage 0: Adler overview with 7 critical tasks (`evidence/BOOK_OVERVIEW.md`).
- Stage 1: five parallel extractors, **88 candidates** (`evidence/candidates/`).
- Stage 1.5: **13 verified units** plus reference / needs-review routing
  (`evidence/verified.md`, `coverage-audit.md`, `needs-review.md`, `references.md`).
- Stage 1.6: proposed **7 promoted skills + 1 source router** at the soft budget of 8
  (`evidence/promotion-gate.json`). This is a proposal, not a compiled pack.
- No compiled pack, no pressure test and no Tier-1 claim were produced for this source.

The core model distilled: **harness = environment** (what the agent can do), **loop =
evidence** (how it knows it is right), **graph = flow** (what happens next). Repair in
that order.

## Evidence quality — read this before trusting the conclusions

- The source is a practitioner essay, not a controlled study: no ablation, no failure
  rates. Causal language is reported, not demonstrated.
- Claims about Karpathy are second-hand. The embedded video was not transcribed; frame
  sampling can miss short demonstrations and timestamps are approximate.
- Several examples in the article are name-dropped without links.
- "Write the check before the code" has no defined procedure for open-ended tasks with
  no deterministic check — held in `needs-review.md`.

## Layout

```
evidence/BOOK_OVERVIEW.md      Stage 0 overview and critical tasks
evidence/candidates/*.md       five extractor outputs (never edited after verification)
evidence/verified.md           V1/V2/V3 records and decisions
evidence/coverage-audit.md     critical task → candidate → destination
evidence/needs-review.md       concrete gaps and how to resolve them
evidence/references.md         where non-executable material was mapped
evidence/promotion-gate.json   Stage 1.6 proposal
evidence/DIGEST.md             distilled human-readable notes
evidence/VIDEO_NOTES.md        frame-grounded video analysis (not a transcript)
evidence/PIPELINE_STATE.md     stage status and destinations
evidence/tweet.json            trigger-tweet metadata from fxtwitter
```

## License

Repository contents are MIT licensed. Third-party source material remains the property
of its respective authors; only short quoted excerpts used for verification are included,
with source links above.
