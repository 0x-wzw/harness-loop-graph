# verified.md — Harness / Loop / Graph (Sharingan Stage 1.5, task-first v2)

Merged from 88 raw candidates (frameworks 17, principles 29, cases 14,
counter-examples 17, glossary 20). Source: `source-article.txt` (X article
@0xWhitemon, 2026-11-08) with `##`/`###` headings as locators; `tweet.json`
is a pointer only. Stage-0 critical tasks: 7.

```yaml
- id: u01
  title: Three-layer diagnosis — route the symptom to the owning layer before changing anything
  merged_from: [f01, f16, p01, p26, g01, g02, g03, g20, c11, ce01, ce06]
  V1: PASS — "The 30-Second Version" and "Which Layer Is Broken?" state the three axes and a symptom->layer table
  V2: PASS (walkthrough) — input: "agent says done but it isn't"; route to loop (check), not prompt; output: named layer + fix
  V3: PASS — prevents a week spent debugging a layer that was fine
  decision: verified
  boundary: taxonomy asserted, no empirical validation; Karpathy framing second-hand

- id: u02
  title: Harness contract with done_when — define the finish line before the run
  merged_from: [f02, f03, p03, p04, g04, c06]
  V1: PASS — "The 6 Parts" gives goal/inputs/output/constraints/done_when fields and says without done_when the agent solves an easier task
  V2: PASS (walkthrough) — new input: fix a checkout bug; write done_when = reproducing test fails before, passes after, suite green
  V3: PASS — removes self-reported completion as an accepted outcome
  decision: verified
  boundary: domain-specific done_when wording is not given; craft locally

- id: u03
  title: Map, not manual — context is an attention budget
  merged_from: [f04, p05, g05, c07]
  V1: PASS — "2. Map" states a short root file pointing to detail docs, and the attention-budget rule
  V2: PASS (walkthrough) — new repo: AGENTS.md with 4 pointers; agent loads docs/testing.md only for a test task
  V3: PASS — saves context before the first edit
  decision: verified

- id: u04
  title: Write it twice — guidance plus an unarguable check
  merged_from: [f05, p10, g10, c14, ce12]
  V1: PASS — "The Write It Twice Trick" shows AGENTS.md rule plus CI lint that fails if src/ui imports src/db
  V2: PASS (walkthrough) — new rule "no direct DB access from UI": write guide line + lint assertion; check fails on a violating import
  V3: PASS — turns past mistakes into infrastructure rather than memory
  decision: verified

- id: u05
  title: Loop design — seven fields with evidence and stop
  merged_from: [f06, f07, p11, p12, p13, p14, g11, g12]
  V1: PASS — "Anatomy of a Loop" lists trigger/goal/state/action/evidence/feedback/stop; "Not All Evidence Is Equal" ranks proof types
  V2: PASS (walkthrough) — design a loop for a failing test: goal=green test, evidence=exit 0 + trace, stop=3 attempts
  V3: PASS — converts 'retry' into a bounded system with rejectable completion
  decision: verified

- id: u06
  title: Write the check before the code — the check is the spec
  merged_from: [f08, p15, ce17]
  V1: PASS — "Write the Check Before the Code" states green must be defined before edits and the test must fail on current code
  V2: PASS (walkthrough) — new task: define a failing test first; if no check can be written, stop and ask
  V3: PASS — prevents vacuous passes and surfaces task misunderstanding early
  decision: verified
  boundary: undefined for open-ended tasks with no deterministic check -> keep as needs_review sub-gap

- id: u07
  title: Feedback as EXPECTED vs SAW, with fence and dead ends
  merged_from: [f09, p16, g13, g14, c09]
  V1: PASS — "Feedback, Not Verdicts" gives FAILED/EXPECTED/SAW/FENCE/DEAD ENDS format
  V2: PASS (walkthrough) — rewrite bare 'red' into expected 302->/login, saw 302->/dashboard at auth/refresh.py:61
  V3: PASS — turns a verdict into a direction and prevents repeated approaches
  decision: verified

- id: u08
  title: Loop exits — retry cap, same-result-twice, escalate
  merged_from: [f10, p17, g15, c10, ce03, ce08]
  V1: PASS — "Exits" gives the Python pattern and states identical result twice means the loop stopped learning
  V2: PASS (walkthrough) — 3-attempt loop; same error twice -> break and escalate instead of third retry
  V3: PASS — stops cost leaks and repeated dead ends
  decision: verified

- id: u09
  title: Graph = nodes/edges/state; loop is a one-node graph
  merged_from: [f11, p18, g16]
  V1: PASS — "What It Is" defines node (one bounded job), edge (real dependency), state (survives between nodes)
  V2: PASS (walkthrough) — given two jobs, decide whether an edge is real by what breaks if B starts early
  V3: PASS — gives a shared vocabulary for coordination failures
  decision: verified

- id: u10
  title: Early-start test — delete fake arrows
  merged_from: [f12, p19, g17, ce09]
  V1: PASS — "The Early-Start Test" states: ask what breaks if B starts before A; if nothing, delete the arrow
  V2: PASS (walkthrough) — billing audit before fix: nothing breaks -> parallel; PR before fix: breaks -> keep edge
  V3: PASS — removes habitual sequencing and shortens critical path
  decision: verified

- id: u11
  title: Four graph cuts — split failures, own context, code when invariant, freeze passed
  merged_from: [f13, p20, p21, p22, p23, g18, ce10, ce13]
  V1: PASS — "4 Cuts" states all four rules with rationale
  V2: PASS (walkthrough) — two steps failing for different reasons -> two nodes; passed node stays read-only; deterministic merge stays a function
  V3: PASS — prevents cross-contamination and needless rework
  decision: verified

- id: u12
  title: Human gates priced by cost of undo, not model confidence
  merged_from: [f15, p25, g19, ce11]
  V1: PASS — "Where You Sit in All This" gives the three tiers (one-click undo / cleanup undo / no undo) and says irreversible tier has no score
  V2: PASS (walkthrough) — schema migration -> human signs; docs change -> ships on green
  V3: PASS — removes argument with probabilities and puts people where mistakes are costly
  decision: verified

- id: u13
  title: Failure-to-lesson ledger — file each failure in the layer that owns it
  merged_from: [f17, p27, ce01, ce06, ce12]
  V1: PASS — "Every Failure Should Upgrade the System" gives failure->lesson->layer table and notes there is no prompt row
  V2: PASS (walkthrough) — 'touched a file it shouldn't' -> remove permission (harness), not a prompt warning
  V3: PASS — makes systems improve instead of repeating incidents
  decision: verified
```

## reference (source value, not independently executable)
- c01–c05 (Codex zero-hand-written-code, Mitchell Hashimoto, Karpathy's list, Claude
  Code loop command, Steinberger's 3.1M question): source-reported name-drops, no links
  or verifiable detail in the acquired text. Map to overview; never as evidence.
- c08 PROGRESS.md sample, c12 ledger, c13 checklist, c14 write-twice example: concrete
  templates; map to capability E sections / overview.
- p28 "5 mistakes" and ce02/ce04/ce05: fully covered by u01/u05/u08/u11; keep in
  overview pitfalls, no duplicate capability.

## needs_review (do not compile as active)
- ce14: no empirical validation, ablation or failure rates behind the taxonomy — treat
  all causal language as source-reported.
- ce15: Karpathy claims are second-hand (article and tweet); the 70-minute video was not
  transcribed in this run.
- ce16: several examples are name-dropped without links; do not restate as verified fact.
- ce17: "write the check before the code" has no defined procedure for open-ended tasks
  with no deterministic check — sub-gap under u06.
