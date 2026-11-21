# Counter-Examples — Harness / Loop / Graph (Sharingan Stage 1)

Extractor: `counter-example-extractor.md`. Source: `source-article.txt` (@0xWhitemon,
"Harness, Loop, Graph", 2026-11-08) and `BOOK_OVERVIEW.md` (critique section for the
source-level gaps ce14–ce17). Quotes are verbatim from the acquired text; headings are
cited as `§...`. No mechanism detail is added beyond what the source states.

```yaml
- id: ce01
  title: The prompt-rewriting treadmill (fix the wording, not the layer)
  type: counter-example
  source_chapter: "Opening (before §The 30-Second Version); §Every Failure Should Upgrade the System"
  source_quote: |
    "Your agent fails, so you rewrite the prompt. It fails again, so you switch the model.
     It fails a third time, so you add "IMPORTANT" in caps and hope for the best.
     Most people have been stuck in this cycle for a year now."
    "The problem is almost never the prompt, and most of the time it isn't the model either.
     The problem is the system around the model."
    "Notice there's no "prompt" row. ... Next quarter's model will read your prompt differently,
     but a test reads the same way forever."
  failure_mode: |
    Treating every agent failure as a prompt or model defect and iterating on wording
    instead of first identifying which layer (harness / loop / graph) owns the symptom.
  mechanism: |
    Prompt edits are not durable: the author's claim is that failures belong to the
    surrounding system, and a lesson filed in the owning layer (a tool, a CI check, a
    graph gate) survives a model swap while a prompt does not. The failure ledger
    deliberately has no "prompt" row. (Asserted by the author, not empirically shown —
    see ce14.)
  warning_signs:
    - rewriting the prompt after every failure
    - switching models to fix a behavioral defect
    - adding "IMPORTANT" / all-caps emphasis
    - a cycle that has persisted for a year
    - the failure ledger has no owning layer
  bound_to:
    - "prompt-engineering advice"
    - "layer-triage / symptom-to-layer routing"
    - "write the rule twice (guide + check)"
  tags: [counter-example, prompt-treadmill, layer-triage]

- id: ce02
  title: The same model writes and grades its own work
  type: counter-example
  source_chapter: "§Part 2 · What Breaks Next; §5 Mistakes That Kill Agent Systems · #2"
  source_quote: |
    "One agent does all of it in a line, inside one context. The second audit reads the
     first one's notes and just repeats them. The whole thing is slow, serial and holds
     one opinion, and on top of that the same agent grades its own work. No amount of
     loop tuning fixes this, because the problem isn't inside any step. It's between them."
    "The same model writes and grades. Self-review shares the same blind spots as the
     original work. Use tests first, a reviewer in a separate context second, and a human
     for anything you can't undo."
  failure_mode: |
    Letting the agent that produced the artifact also verify it; self-review inherits the
    original work's blind spots, so the check cannot reject the error it was meant to catch.
  mechanism: |
    The defect lives between steps, not inside a step, so loop tuning cannot fix it. The
    source's remedy is an evidence ladder: deterministic tests first, an independent
    reviewer in a separate context second, a human for irreversible actions.
  warning_signs:
    - one agent runs the whole ticket serially in one context
    - "looks good" / "I'm confident" accepted as proof
    - grader saw the author's notes or shared its context
    - no independent second opinion
  bound_to:
    - "loop tuning / retry engineering"
    - "self-review as evidence"
    - "independent-evidence rule"
  tags: [counter-example, self-grading, blind-spots, independent-review]

- id: ce03
  title: '"Keep trying" is not a loop — it is a cost leak'
  type: counter-example
  source_chapter: "§5 Mistakes That Kill Agent Systems · #3; §Part 2 · Exits"
  source_quote: |
    ""Keep trying" as a loop. That isn't a loop, it's an open tab on your credit card.
     Every loop needs a goal, real evidence, a retry cap and an exit."
    "A loop without exits isn't persistence, it's a cost leak."
  failure_mode: |
    Configuring "retry until it works" as the whole strategy: no goal condition, no
    verifiable evidence, no retry cap, no exit, so budget is consumed without learning.
  mechanism: |
    A loop is only a work-and-feedback system when it has a trigger, goal, state, action,
    evidence, feedback and a stop. Without a cap and an exit, retries are indistinguishable
    from an unbounded paid call; persistence and cost leak have the same observable shape.
  warning_signs:
    - "retry" is the entire strategy
    - no stated goal / green condition
    - no retry cap or token budget
    - no escalate branch
    - retries burn budget on the same error
  bound_to:
    - "loop design"
    - "retry policies"
    - "budget guards"
  tags: [counter-example, cost-leak, no-exit, retry-cap]

- id: ce04
  title: The harness as a junk drawer (more tools = more wrong choices)
  type: counter-example
  source_chapter: "§5 Mistakes That Kill Agent Systems · #4; §Part 1 · 3. Tools"
  source_quote: |
    "The harness as a junk drawer. More tools don't make a better agent, they make more
     wrong choices. A good harness isn't crowded, it's precise."
    "Every tool you add is one more way for the model to be wrong, so ten narrow tools beat
     forty overlapping ones. Each tool needs a clear input, a predictable output, an
     explicit failure state and a permission level."
  failure_mode: |
    Equipping the agent with as many tools as possible, including overlapping ones with
    vague contracts, thereby multiplying the ways it can act incorrectly.
  mechanism: |
    Each tool is an additional choice point for the model; overlapping tools create
    ambiguous selection. Narrowing each tool's input, output, failure state and permission
    reduces the error surface — precision, not quantity, is the goal.
  warning_signs:
    - dozens of overlapping tools
    - a tool without an explicit failure state or permission level
    - "add one more tool" as the response to a failure
    - tools that can deploy or delete without approval
  bound_to:
    - "tool design"
    - "harness construction"
    - "permission policy"
  tags: [counter-example, tool-sprawl, harness, choice-overload]

- id: ce05
  title: Building the graph too early
  type: counter-example
  source_chapter: "§5 Mistakes That Kill Agent Systems · #1; §Part 3 · When Not to Use a Graph"
  source_quote: |
    "Building the graph too early. People draw a twelve-node diagram before they've
     watched the agent do the job once. Start with a harness and one loop, collect traces,
     and formalize only what actually deserves it."
    "Most tasks don't need one. If you can collapse your five nodes back into a single loop
     and lose nothing, do it. ... Just don't reach for it until the work forces you to."
  failure_mode: |
    Formalizing a multi-node orchestration before observing the agent perform the job and
    collecting traces, producing structure not grounded in real failure boundaries.
  mechanism: |
    Nodes should be split where things actually fail separately; without traces, the split
    is guessed, which manufactures fake dependencies and serial work. The source's order
    is harness → one loop → traces → formalize only what deserves it, with a collapse test
    before committing to a graph.
  warning_signs:
    - a twelve-node diagram before the first trace
    - graph built before a single working loop
    - nodes that collapse back into one loop with no loss
    - structure modeled on imagined rather than observed failures
  bound_to:
    - "graph / orchestration skill"
    - "node-splitting rule"
    - "early-start dependency audit"
  tags: [counter-example, premature-structure, graph, trace-first]

- id: ce06
  title: Blaming the model for a layer defect
  type: counter-example
  source_chapter: "§5 Mistakes That Kill Agent Systems · #5; §The Checklist (closing line)"
  source_quote: |
    "Blaming the model. No model can compensate for broken APIs, stale state, vague tool
     schemas or missing exits. Fix the layer that owns the failure."
    "If several of these are a no, a smarter model won't save you. It'll just make the
     failure faster and more expensive."
  failure_mode: |
    Upgrading or swapping the model in response to failures whose real cause is the
    environment, evidence or flow layer.
  mechanism: |
    Model capability cannot substitute for well-specified tools, fresh state, valid schemas
    or stop conditions; a stronger model amplifies an existing layer defect, increasing
    both speed of failure and cost. The prescribed move is symptom-to-layer triage first.
  warning_signs:
    - switching to a smarter/larger model after failures
    - no attempt to locate which layer owns the symptom
    - several checklist items answered "no"
    - broken APIs / stale state / vague tool schemas still present
  bound_to:
    - "model selection"
    - "layer-triage"
    - "checklist-based debugging"
  tags: [counter-example, blame-the-model, layer-triage, cost]

- id: ce07
  title: '"Done" as self-report is not a stop condition'
  type: counter-example
  source_chapter: "§Part 2 · Anatomy of a Loop (rule); §Part 2 · Not All Evidence Is Equal; §Part 1 · What Breaks Next"
  source_quote: |
    "Don't loop on confidence, loop on evidence. "The agent says it's done" is not a stop
     condition. Tests passing is."
    "A check is only as strong as the weakest thing it accepts as proof. If your loop
     accepts "the model says it's done", it's a self-report loop no matter how many steps
     it has."
    "It finishes with "Fixed! All tests should pass now." Notice the word "should"."
  failure_mode: |
    Accepting the agent's own claim of completion as the loop's green condition, including
    hedged claims like "should pass", so the loop ends without verifiable evidence.
  mechanism: |
    The evidence hierarchy ranks self-report ("looks good", "I'm confident", "should pass")
    weakest; the check is only as strong as the weakest proof it accepts, so adding steps
    to a self-report loop changes nothing about its validity.
  warning_signs:
    - "should pass" / "looks good" / "I'm confident"
    - "done" with no gate behind it
    - no deterministic, observable or independent evidence
    - "done" means nothing until a human checks
  bound_to:
    - "completion / done_when definitions"
    - "stop conditions"
    - "evidence hierarchy"
  tags: [counter-example, self-report, false-done, evidence-hierarchy]

- id: ce08
  title: Loops without exits, and the same-result-twice trap
  type: counter-example
  source_chapter: "§Part 2 · Exits; §The Checklist (Loop); §Which Layer Is Broken?"
  source_quote: |
    "When the agent gets the exact same result twice, it has stopped learning from the loop
     and more attempts won't help. The missing piece is something it can't see, or the task
     was framed wrong. A loop can fix the work, but it can't fix the question."
    "return escalate_to_human(state)"
    "There's a retry cap and a token budget. Same result twice means escalate."
    "retries burn budget on the same error → loop (feedback + exits)"
  failure_mode: |
    Continuing to retry after the loop has produced identical evidence twice, instead of
    recognizing that no new information is arriving and escalating.
  mechanism: |
    Identical results mean the agent has stopped learning; further attempts replay the same
    work. The missing piece is either invisible to it or the task was framed wrong — "a
    loop can fix the work, but it can't fix the question" — so a dead-end check and an
    escalate branch are required structural exits.
  warning_signs:
    - same error repeated with no new feedback
    - no dead-ends set, no retry cap, no escalate branch
    - attempt three quietly repeats attempt one
    - retrying when the task framing may be wrong
  bound_to:
    - "loop design"
    - "escalation policy"
    - "feedback with DEAD ENDS"
  tags: [counter-example, no-exit, escalate, same-result-twice]

- id: ce09
  title: Fake arrows in workflow diagrams
  type: counter-example
  source_chapter: "§Part 3 · The Early-Start Test"
  source_quote: |
    "Most arrows in a workflow diagram aren't real dependencies. They're habits, just the
     order someone happened to think of the steps. So for every arrow, ask what would break
     if B started before A finished. If the answer is "nothing", delete the arrow and run
     them in parallel."
    "Can the billing audit start before the fix lands? Yes, so it runs in parallel. Can the
     PR open before the fix lands? No, so that arrow is real."
  failure_mode: |
    Treating the order in which steps were conceived as a real data dependency, so
    independent work is serialized behind edges that carry no actual constraint.
  mechanism: |
    An edge is legitimate only when one node's output feeds another's input; the early-start
    test (what breaks if B starts before A finishes?) separates real dependencies from
    habitual ordering, and "nothing" means delete the edge and parallelize.
  warning_signs:
    - an arrow with no answer to "what breaks if B starts first?"
    - dependencies that are just the order someone listed the steps
    - serial steps sharing no data
    - no parallel execution of independent audits
  bound_to:
    - "graph dependency audit"
    - "early-start test"
    - "parallelization"
  tags: [counter-example, fake-dependency, workflow, early-start-test]

- id: ce10
  title: Rerunning passed nodes (good work is a free chance to break it)
  type: counter-example
  source_chapter: "§Part 3 · 4 Cuts That Decide If a Graph Helps · Freeze what passed; §Which Layer Is Broken?"
  source_quote: |
    "Freeze what passed. Once a node gets through its gate, its output is read-only. When
     something fails, rerun only that node with its feedback. Rerunning good work is just a
     free chance to break it."
    "one failure means everything reruns → graph (gates)"
  failure_mode: |
    Re-executing the entire pipeline after a single node fails, instead of rerunning only
    the failed node with its feedback while keeping passed outputs frozen.
  mechanism: |
    Already-verified work carries no upside on rerun but reintroduces variance, so a
    whole-pipeline retry can break previously green work. Per-node gates plus read-only
    outputs scope the retry to the failing node.
  warning_signs:
    - one failure triggers a full rerun
    - passed nodes' outputs remain mutable
    - no per-node gate
    - no targeted rerun with feedback
  bound_to:
    - "graph gates"
    - "freeze-what-passed rule"
    - "retry scoping"
  tags: [counter-example, rerun, gates, freeze-passed]

- id: ce11
  title: Gating by model confidence instead of cost of undo
  type: counter-example
  source_chapter: "§Where You Sit in All This; §The Checklist (Graph)"
  source_quote: |
    "You're the slowest and most expensive node in the graph, so put yourself only where a
     mistake can't be taken back. Gate on the price of undo, not on the model's confidence."
    "The last tier has no score attached. Not 0.95, not 0.99. There's no number for the model
     to beat, so there's nothing to argue with."
    "Gates are priced by undo, not confidence."
  failure_mode: |
    Using a confidence threshold to decide where a human must approve, including letting
    irreversible actions auto-ship because the model scored highly.
  mechanism: |
    A numeric score invites argument and has no correct cutoff; undo cost is a structural,
    non-negotiable property. The source's tiers: one-click undo ships on green; cleanup
    undo requires green + trace + second opinion; no undo (migrations, deletes, emails,
    money) requires a human signature with no score at all.
  warning_signs:
    - confidence-threshold gates (0.95 / 0.99)
    - human review on trivial reversible work
    - irreversible actions auto-shipping
    - the model judging its own risk
  bound_to:
    - "human-in-the-loop gating"
    - "approval policy"
    - "confidence thresholds"
  tags: [counter-example, undo-cost, confidence-gate, human-approval]

- id: ce12
  title: '"Be careful" in a prompt is a hope, not a structural rule'
  type: counter-example
  source_chapter: "§Every Failure Should Upgrade the System; §Part 1 · 5. Walls; §Part 1 · The \"Write It Twice\" Trick"
  source_quote: |
    ""Be careful not to duplicate work" in a prompt is a hope, while a split rule in the
     scheduler is structure. Next quarter's model will read your prompt differently, but a
     test reads the same way forever."
    ""Please don't touch migrations" is a wish. A permission the agent doesn't have is a
     wall. Never let the same system invent the plan, approve the risk and execute the
     side effect."
    "Write every important rule twice: once as guidance the agent can understand, and once
     as a check it can't get around."
  failure_mode: |
    Storing important rules only as prose the agent is asked to follow, with no
    enforceable check or permission outside the model backing them up.
  mechanism: |
    Prose compliance depends on the current model and drifts across model versions; a CI
    check, lint rule or denied permission is invariant. Encoding each rule as guide +
    unskippable check converts past mistakes into infrastructure, so the model ignoring
    the guide on any given day does not reintroduce the failure.
  warning_signs:
    - important rules live only in prose / AGENTS.md
    - no CI or lint enforcement behind a rule
    - "please don't" phrasing for hard constraints
    - the same system plans, approves and executes
  bound_to:
    - "rule durability"
    - "write-it-twice pattern"
    - "walls / permissions"
  tags: [counter-example, prompt-as-hope, structural-rule, write-it-twice]

- id: ce13
  title: The second audit that just repeats the first agent's notes
  type: counter-example
  source_chapter: "§Part 2 · What Breaks Next; §Part 3 · 4 Cuts · Give every worker its own context; §Every Failure Should Upgrade the System"
  source_quote: |
    "The second audit reads the first one's notes and just repeats them. The whole thing is
     slow, serial and holds one opinion, and on top of that the same agent grades its own work."
    "Four agents sharing one context aren't a team, they're one agent wearing four hats.
     The first opinion written down becomes everyone's opinion."
    "two audits overlapped → split rule in scope node → graph"
  failure_mode: |
    Running a second audit in the same context as the first, so it echoes the first
    opinion instead of independently checking it, while remaining slow and serial.
  mechanism: |
    A shared context anchors every worker on the first written opinion, so additional
    "workers" add latency but no independent judgment. The fix is a graph cut: give each
    worker its own context and split scopes so overlap is impossible, with a separate
    reviewer for grading.
  warning_signs:
    - sequential audits in one shared context
    - second review restates the first agent's notes
    - overlapping worker scopes
    - grader read the author's notes before judging
  bound_to:
    - "multi-agent orchestration"
    - "independent review"
    - "scope splitting / own-context rule"
  tags: [counter-example, anchoring, shared-context, audit-overlap]

- id: ce14
  title: Source-level gap — no empirical validation behind the taxonomy
  type: counter-example
  source_chapter: "BOOK_OVERVIEW.md · Critique (Adler step 3)"
  source_quote: |
    "Attribute-driven, not empirical: no controlled evaluation, no ablation, no failure
     rates. "Same model, same prompt, completely different results" is asserted."
  failure_mode: |
    Treating the three-layer taxonomy and its checklist as empirically validated causal
    rules rather than an argued, attribute-driven framework.
  mechanism: |
    The source provides no controlled evaluation, ablation or failure-rate data, so claims
    like "fixing the right layer saves a week" are asserted, not measured. Under Sharingan
    verification this keeps derived rules in reference/needs-review, not verified causal.
  warning_signs:
    - citing the article for failure-rate or causal-gain claims
    - presenting the checklist as tested rather than proposed
  bound_to:
    - "all positive skills derived from this source"
    - "claim strength / verification status"
  tags: [counter-example, source-gap, no-empirical-validation]

- id: ce15
  title: Source-level gap — second-hand Karpathy claims
  type: counter-example
  source_chapter: "BOOK_OVERVIEW.md · Source chain / Critique; §Why This Suddenly Matters"
  source_quote: |
    "The Karpathy video itself was NOT transcribed; claims about what Karpathy demonstrated
     are source-reported by the article/tweet, not independently viewed."
    "Source is an X article from a small account; claims about Karpathy are second-hand."
    "At the end of last year Karpathy posted the most honest description of where we all are:"
  failure_mode: |
    Borrowing authority from the Karpathy name for the taxonomy, when the underlying
    70-minute video was never viewed or transcribed and the article quotes no content from it.
  mechanism: |
    The article asserts that Karpathy "posted the most honest description" and reproduces
    a list of terms, but the trigger tweet is promotional and the video unseen; the
    attribution is a chain of hearsay, not direct evidence.
  warning_signs:
    - authority claim resting on an unseen video
    - no transcript, link or quoted content for the attributed list
    - promoter tweet used as a source
  bound_to:
    - "any skill citing Karpathy as validation"
    - "provenance / attribution checks"
  tags: [counter-example, source-gap, second-hand-claim, provenance]

- id: ce16
  title: Source-level gap — name-dropped examples without links
  type: counter-example
  source_chapter: "BOOK_OVERVIEW.md · Critique; §Part 1 Harness; §Part 3 Graph"
  source_quote: |
    "Examples (Codex zero-hand-written-code, Mitchell Hashimoto) are name-dropped without
     links or verifiable detail in the acquired text."
    "OpenAI ran into exactly this when they built a product with Codex and zero hand-written
     code. ... Even Mitchell Hashimoto, the guy behind Terraform and Ghostty, says a generic
     agent harness beats every custom chat box he's tried."
    "In July one short question from Peter Steinberger got 3.1M views ... Rohit put it well
     ... tip number five from the guy who built Claude Code."
  failure_mode: |
    Treating named authorities and metrics as supporting evidence when the acquired text
    supplies no links, quotations or verifiable detail for them.
  mechanism: |
    Authority-by-association: Codex, Hashimoto, Steinberger (3.1M views), Rohit and the
    Claude Code tip are invoked without citations, so they function rhetorically rather
    than as checkable cases and cannot seed a verified case candidate.
  warning_signs:
    - a named example with no link or quote
    - a view/impact metric with no source
    - "X put it well" standing in for an argument
  bound_to:
    - "case extraction from this source"
    - "evidence provenance"
  tags: [counter-example, source-gap, name-dropping, unverifiable]

- id: ce17
  title: Source-level gap — "write the check" undefined for open-ended tasks
  type: counter-example
  source_chapter: "BOOK_OVERVIEW.md · Critique; §Part 2 · Write the Check Before the Code; §Part 3 · 4 Cuts"
  source_quote: |
    ""Write the check before the code" is sound but under-specified for open-ended tasks
     where no deterministic check exists."
    "Before the agent touches a single file, write down what green means, and include a test
     that fails on the current code. A test that already passes before the fix proves nothing.
     ... if you can't write the check, you don't actually understand the task yet."
    "Use a model only where a different answer could also be right."
  failure_mode: |
    Applying "write the check before the code" universally, including to open-ended work
    where no deterministic test exists, then either inventing a fake check or concluding
    the task is not understood.
  mechanism: |
    The evidence hierarchy's strongest tiers (exit 0, schema validates, build compiles)
    presuppose a deterministically checkable spec. The source never defines what "green"
    means when multiple correct answers are legitimate, so the completion rule has an
    unstated precondition and the "if you can't write the check" inference fails there.
  warning_signs:
    - open-ended task with no deterministic test available
    - a contrived check created only to satisfy the rule
    - "if you can't write the check you don't understand" applied to genuine ambiguity
  bound_to:
    - "write-check-before-code"
    - "evidence hierarchy"
    - "stop conditions / done_when"
  tags: [counter-example, source-gap, undefined-precondition, open-ended-tasks]
```
