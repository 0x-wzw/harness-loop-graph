# Distilled notes — Harness / Loop / Graph

Source: @0xoctocat [tweet](https://x.com/0xoctocat/status/2123798917049368850)
(2026-11-20, pointer) → @0xWhitemon [article](https://x.com/0xWhitemon/status/2119430401701621865)
(2026-11-08, primary). Distilled with Sharingan RIA-TV++ v2.5 through Stage 1.6.
All claims below are source-reported unless marked as our own inference.

## The one-line model

**Harness = what the agent can do (environment). Loop = how it knows it's right
(evidence). Graph = what happens next (flow).** Order of repair: environment →
feedback → flow. An unreliable agent is usually a layering error, not a model error.

## 1. Harness (environment)

Definition: remove the model from the architecture diagram; everything left is the
harness. Six parts:

1. **Contract** — goal, inputs, output, constraints, `done_when`. The critical field is
   `done_when`: without it the agent solves an easier task and reports success.
2. **Map** — a short root file (AGENTS.md) pointing to detail docs. Context is an
   attention budget: a map saves it, a giant manual consumes it before the first edit.
3. **Tools** — ten narrow tools beat forty overlapping ones. Each needs a clear input,
   predictable output, explicit failure state and a permission level.
4. **Memory** — context window is RAM, harness is disk. Decisions, dead ends and open
   risks go into files and git commits (PROGRESS.md), not chat; this is what survives a
   crash, reset or handoff.
5. **Walls** — a permission the agent does not have. Never let the same system invent
   the plan, approve the risk and execute the side effect.
6. **Traces** — every run leaves a readable record: context loaded, tools called,
   changes, tests, retries, cost. Without traces a failure is a mystery.

**Write it twice.** Every important rule appears as guidance the agent reads *and* as a
check it cannot argue with (e.g. AGENTS.md says UI may not query the DB; CI lint fails
if `src/ui/**` imports `src/db/**`). The guide explains why; the check holds on the day
the model ignores the guide. Past failures become infrastructure.

## 2. Loop (evidence)

Seven fields: **trigger, goal, state, action, evidence, feedback, stop**.

- **Don't loop on confidence, loop on evidence.** "The agent says it's done" is not a
  stop condition; tests passing is.
- Evidence strength: **deterministic** (exit 0, schema validates) > **observable** (trace
  shows the test ran) > **independent** (reviewer in a separate context) > **self-report**
  ("looks good", "should pass"). A check is only as strong as the weakest proof it accepts.
- **Write the check before the code**, and make sure it fails on current code. A test
  that already passes proves nothing. If you cannot write the check, you do not yet
  understand the task.
- **Feedback, not verdicts.** Useful feedback has FAILED / EXPECTED / SAW / FENCE /
  DEAD ENDS. "Red" alone tells the agent nothing; expected-vs-saw gives direction.
- **Exits.** Retry cap plus a same-result-twice rule: if the agent gets the identical
  result twice it has stopped learning — break and escalate. A loop without exits is a
  cost leak.

## 3. Graph (flow)

A graph is **nodes** (one bounded job, one input, one output), **edges** (real
dependencies where one output feeds another input) and **state** (what survives between
nodes). A loop is just a graph with one node and an edge back to itself.

- **Early-start test:** for each arrow ask what breaks if B starts before A. If nothing,
  delete the arrow and run in parallel. Most arrows are habits, not dependencies.
- **Four cuts:** split where things fail for different reasons; give each worker its own
  context (four agents sharing one context are one agent in four hats); if the answer
  should never change it is code, not a model call; freeze what passed — rerun only the
  failing node with feedback.
- **When not to use one:** if the graph collapses back to a single loop with no loss,
  do that. Do not draw twelve nodes before watching the agent do the job once.

## 4. Human gates

Gate by **cost of undo**, not model confidence:

| Undo cost | Gate |
|---|---|
| One-click (docs, tests, one function) | ships on green |
| Cleanup (shared helpers, auth, schemas) | green + trace + second opinion |
| No undo (migrations, deletes, emails, money) | human signs |

The irreversible tier has no score — nothing for the model to argue with.

## 5. Triage table (from the article)

| Symptom | Fix the layer |
|---|---|
| copy-pasting between chat and terminal | harness (tools) |
| retries things already tried | harness (memory) |
| "done" means nothing until checked | loop (the check) |
| retries burn budget on the same error | loop (feedback + exits) |
| each step right, whole thing slow | graph (shape) |
| one failure reruns everything | graph (gates) |
| same mistake returns weekly | all layers (learning) |

**Failure → lesson:** every failure should be filed in the layer that owns it — an
unauthorized file touch becomes a removed permission (harness), not a prompt warning;
a "fixed" with no test becomes a required CI check (loop); overlapping audits become a
split rule (graph). There is no "prompt" row in the ledger.

## 6. Anti-patterns

- Prompt-rewriting treadmill: changing words instead of fixing a layer.
- Same model writes and grades its own work — shared blind spots.
- "Keep trying" as a loop — an open tab on your credit card.
- Harness as a junk drawer — more tools, more wrong choices.
- Graph too early, before any traces exist.
- Blaming the model for broken APIs, stale state or missing exits.
- Prompts like "be careful not to duplicate work" — a hope, not a structure.

## 7. Honest limits (our critique, not the article's)

- The taxonomy is **not empirically validated** — no ablations, failure rates or
  controlled comparisons in the source. Treat causal language as a claim.
- Karpathy references are **second-hand**: the tweet promotes a 70-minute video that
  was not transcribed in this run, and the article cites Karpathy's list without a link.
- Several examples (Codex zero-hand-written-code, Mitchell Hashimoto, Steinberger's
  3.1M-view question) are name-dropped without verifiable detail.
- "Write the check before the code" is under-specified for open-ended tasks where no
  deterministic check exists — held as `needs_review`.
- The three layers do not cover model selection, data quality or cost/quality tradeoffs.

## Stage 1.6 proposal (not yet compiled or installed)

13 verified units from 88 candidates. Proposed 7 promoted + 1 source router (soft
budget 8): layer diagnosis, contract/done_when, write-it-twice, loop design, feedback
format, loop exits, undo-priced gates. Graph vocabulary and the four cuts stay as router
cards; map-vs-manual, check-before-code and the failure ledger are retained as cards.

Full artifacts: `BOOK_OVERVIEW.md`, `candidates/*.md`, `verified.md`,
`coverage-audit.md`, `needs-review.md`, `references.md`, `promotion-gate.json` in
`/Users/admin/.hermes/cache/scratch/harness-loop-graph/`.
