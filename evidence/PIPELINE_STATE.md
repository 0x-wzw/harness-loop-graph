# PIPELINE_STATE — Harness / Loop / Graph (Sharingan RIA-TV++ v2.5)

source: tweet https://x.com/0xoctocat/status/2123798917049368850 (pointer)
primary: article https://x.com/0xWhitemon/status/2119430401701621865
local: /Users/admin/.hermes/cache/scratch/harness-loop-graph/

| stage | status | artifact |
|---|---|---|
| acquire | done | tweet.json, source-article.txt (355 lines) |
| 0 — Adler overview | done | BOOK_OVERVIEW.md, 7 critical tasks |
| 1 — 5 parallel extractors | done | candidates/{frameworks,principles,cases,counter-examples,glossary}.md (88 candidates) |
| 1.5 — triple verification | done | verified.md (13 verified), coverage-audit.md, needs-review.md, references.md |
| 1.6 — promotion gate | proposed | promotion-gate.json (7 promoted + 1 router proposal at soft budget 8) |
| notes deliverable | done | DIGEST.md (~7 KB) + VIDEO_NOTES.md (frame-grounded, NOT a spoken transcript) |
| 2 — RIA cards | not run | one consolidated distil-led skill authored instead of the 7+1 compiled pack |
| 3 — Zettelkasten | partial | related_skills in the vault skill |
| 4 — pressure test + Tier-1 | not run | no compiled pack produced; no Tier-1 claims made |
| 5 — published | done | Obsidian: Knowledge/20-Reports/Harness-Loop-Graph-Karpathy-Distillation-2026-11-21.md; Knowledge/40-Templates/cangjie/harness-loop-graph/SKILL.md + _INDEX.md. Notion: 6 blocks appended to "Cangjie — Distilled Skills Index" (page 41105e4a-7c41-8179-8cb3-c6814e0a8554). NOTHING pushed to GitHub. |

Constraints: cangjie distribution policy = markdown to vault + Notion only; GitHub code/releases only.
Video evidence limitation: 24 frames at ~168 s intervals, on-screen text read by image analysis;
audio transcription unavailable (video_analyze has no video endpoint; Swift Speech recognition hung).
Do not present VIDEO_NOTES.md as a word-for-word transcript.
