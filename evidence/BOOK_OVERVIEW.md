# BOOK_OVERVIEW — Harness / Loop / Graph (Sharingan Stage 0)

Source chain:
- Trigger tweet: https://x.com/0xoctocat/status/2123798917049368850 (@0xoctocat,
  2026-11-20, 278K views) — promotional pointer to a 70-minute Karpathy screen-share
  and to a guide. Text only; no methodology of its own.
- Primary source distilled here: @0xWhitemon, "Harness, Loop, Graph: The 3 Layers
  That Decide If Your AI Agent Works" (https://x.com/0xWhitemon/status/2119430401701621865,
  2026-11-08), full text acquired via Jina Reader into `source-article.txt` (355 lines).
- Assumption stated: the tweet is a pointer, so the linked article is the primary
  source. The Karpathy video itself was NOT transcribed; claims about what Karpathy
  demonstrated are source-reported by the article/tweet, not independently viewed.

## Structure (Adler step 1)
1. Failure framing: agents fail and people tweak prompts/models. The problem is the
   system around the model; in 2026 it got three names: harness, loop, graph.
2. Axis table: HARNESS = what the agent can do (environment); LOOP = how it knows it's
   right (evidence); GRAPH = what happens next (flow). Mnemonic: environment → feedback → flow.
3. Part 1 Harness — six parts: contract (with `done_when`), map (AGENTS.md as index,
   not manual), tools (narrow contracts, permissions), memory (files not chat),
   walls (policy outside model), traces. "Write it twice": guide + CI check.
4. Part 2 Loop — anatomy: trigger/goal/state/action/evidence/feedback/stop. Evidence
   hierarchy deterministic > observable > independent > self-report. Write the check
   before the code; feedback as EXPECTED vs SAW + fence + dead ends; exits including
   same-result-twice escalation.
5. Part 3 Graph — nodes (bounded job, one in/one out), edges (real dependency), state.
   Early-start test; four cuts (split where failures differ, own context per worker,
   deterministic work stays code, freeze what passed); when not to use a graph.
6. Human placement — gate by undo cost (one-click undo ships on green, cleanup undo
   needs trace + second opinion, no-undo needs a human signature).
7. Symptom→layer table, failure→lesson ledger, five mistakes, checklist, closing
   thesis (prompt=instruction, context=view, harness=environment, loop=evidence,
   graph=coordination).

## Interpretation (Adler step 2)
The durable thesis: agent unreliability is a layering error, not a model error. Each
layer owns a different failure class, so debugging must first identify which layer
owns the symptom. Three transferable mechanisms: (a) encode completion as evidence a
check can reject, never self-report; (b) write each important rule twice — as guidance
and as an enforceable check; (c) treat orchestration as a dependency graph whose edges
must pass the early-start test, and place humans by cost of undo rather than model
confidence.

## Critique (Adler step 3)
- Attribute-driven, not empirical: no controlled evaluation, no ablation, no failure
  rates. "Same model, same prompt, completely different results" is asserted.
- Concept boundaries are soft: harness/loop/graph overlap with established ideas
  (tool use, eval loops, DAG schedulers); the naming is new, the underlying moves are not.
- Examples (Codex zero-hand-written-code, Mitchell Hashimoto) are name-dropped without
  links or verifiable detail in the acquired text.
- "Write the check before the code" is sound but under-specified for open-ended tasks
  where no deterministic check exists.
- The three-layer taxonomy does not cover model selection, data, or cost/quality tradeoffs.
- Source is an X article from a small account; claims about Karpathy are second-hand.

## Application (Adler step 4)
Useful to an agent operator: a symptom→layer triage table, a loop design checklist with
real stop conditions, a graph dependency audit, and a human-gating rule priced by undo.
These are process patterns, not code.

## Critical tasks for coverage audit
1. Diagnose which layer owns a given agent failure.
2. Define a completion condition that cannot be satisfied by self-report.
3. Make a rule durable when the model may ignore guidance.
4. Design a feedback message that gives direction, not a verdict.
5. Decide when to escalate instead of retrying.
6. Decide whether a multi-node graph is warranted, and prune fake dependencies.
7. Place human approval gates where mistakes are irreversible.
