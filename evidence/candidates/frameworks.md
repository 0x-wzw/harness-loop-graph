# Framework candidates — Harness / Loop / Graph (Sharingan Stage 1)
# Extractor: framework-extractor. Source: source-article.txt (@0xWhitemon, 2026-11-08).
# All source_quote values are verbatim from the acquired text; source_chapter cites the article's own headings.
# No mechanism detail is invented; gaps are recorded in missing_conditions.

- id: f01
  title: Three-layer taxonomy (harness / loop / graph) as a diagnostic lens
  type: framework
  source_chapter: "The 30-Second Version; The Real Shift"
  source_quote: |
    "HARNESS   what the agent CAN do        environment
    LOOP      how it knows it's RIGHT      evidence
    GRAPH     what happens NEXT            flow
    If you remember one line from this article, make it this one: environment, then feedback, then flow."
    "PROMPT    -> instruction / CONTEXT   -> working view / HARNESS   -> environment / LOOP      -> evidence / GRAPH     -> coordination."
  summary: |
    A three-layer thinking model for agent systems: harness = environment (what the agent can do),
    loop = evidence (how it knows it is right), graph = flow (what happens next). Each layer owns a
    distinct failure class, so an unreliable agent is a layering error to be classified before any
    change, not a mystery and not automatically a model defect. Mnemonic: environment -> feedback -> flow.
  inputs: an observed agent failure; a proposed system change
  outputs: classification of which layer owns the failure; ordered fix priority
  steps: map symptoms to layers -> decide owning layer -> apply that layer's fix before deeper ones
  missing_conditions: |
    Source admits concept boundaries are soft (overlap with tool use, eval loops, DAG schedulers);
    gives no formal boundary rule, no tie-breaker for cross-layer edge cases, and no empirical validation.
  tags: [mental-model, taxonomy, diagnosis, agent-systems]

- id: f02
  title: The six parts of a real harness (build checklist)
  type: framework
  source_chapter: "Part 1. Harness > The 6 Parts of a Real Harness"
  source_quote: |
    "The cleanest definition I know: remove the model from your architecture diagram, and everything still on the page is the harness."
    "1. Contract... 2. Map... 3. Tools... 4. Memory... 5. Walls... 6. Traces."
  summary: |
    Checklist of the environment around the model: (1) Contract with a finish line, (2) Map as a short
    root index, (3) Tools that are narrow with clear contracts/failure states/permissions, (4) Memory in
    files not chat, (5) Walls as policy outside the model, (6) Traces so every run is legible. The harness
    makes the agent capable; changing the harness, not the weights, is what changes capability.
  inputs: a model plus the surrounding environment to be specified
  outputs: a harness with six specified parts
  steps: define contract -> provide map -> add narrow tools -> persist memory to files -> enforce walls -> leave traces
  missing_conditions: |
    Source gives no mandatory ordering, no minimum viable subset, no inter-part dependencies,
    and no criterion for when the harness is "enough."
  tags: [checklist, harness, workflow]

- id: f03
  title: Contract with done_when (definition of done that cannot be self-reported)
  type: framework
  source_chapter: "Part 1. Harness > The 6 Parts of a Real Harness (1. Contract)"
  source_quote: |
    "Before the agent acts, turn the request into something with a finish line."
    "goal: fix login redirect loop (#482) / inputs: issue, repo, logs / output: reviewable pull request /
    constraints: no schema changes, touch only auth/ / done_when: new test reproduces the bug / same test
    passes after the fix / full suite is green."
    "The most important field here is done_when. Without it the agent will quietly solve an easier version of the task and tell you it's done."
  summary: |
    Convert a request into a structured contract with goal, inputs, output, constraints and an explicit
    done_when. done_when is a set of checkable conditions (test reproduces, test passes after fix, suite
    green) that prevent the agent from solving an easier version and declaring success.
  inputs: a raw request or ticket
  outputs: a contract with goal, inputs, output, constraints, done_when
  steps: write goal -> list inputs -> define output -> set constraints -> state done_when as verifiable conditions
  missing_conditions: |
    Source supplies one worked example only; no rule for open-ended tasks where done_when cannot be made
    deterministic, no guidance on number of conditions, and no conflict-arbitration rule.
  tags: [contract, definition-of-done, harness]

- id: f04
  title: Map vs manual (context as an attention budget)
  type: framework
  source_chapter: "Part 1. Harness > The 6 Parts of a Real Harness (2. Map)"
  source_quote: |
    "Don't dump every doc into the context window. Give the agent a short root file that tells it where things live, and let it load the details only when the task needs them."
    "Context isn't storage, it's an attention budget. A map saves it, a giant manual eats it before the agent writes a single line."
  summary: |
    Replace a giant manual with a short root index (e.g., AGENTS.md) that points to detail docs by topic
    (architecture, tests, security, commands). The agent loads details lazily only when the task needs them,
    preserving the context attention budget. A map saves attention; a manual consumes it before work starts.
  inputs: a documentation set; a task
  outputs: a short root map file with topic -> detail-file pointers
  steps: create root index -> list topic-to-file pointers -> let agent load detail files on demand
  missing_conditions: |
    Source gives no map size limit, no freshness/maintenance procedure, and no handling for topics that
    do not fit the pointer format.
  tags: [context-management, harness, map]

- id: f05
  title: Write it twice — guidance plus an unarguable check
  type: framework
  source_chapter: "Part 1. Harness > The 'Write It Twice' Trick"
  source_quote: |
    "The fix is to write every important rule twice: once as guidance the agent can understand, and once as a check it can't get around."
    "GUIDE (AGENTS.md) UI code may not query the database directly / CHECK (CI) lint fails if src/ui/** imports src/db/**."
    "The guide explains the reason. The check holds even on the day the model ignores the guide. Over time this turns past mistakes into infrastructure."
  summary: |
    For every important rule, write it in two places: a GUIDE in agent-readable prose that explains the
    reason, and a CHECK enforced by CI that the agent cannot argue with. The check holds even when the
    model ignores the guide, converting past mistakes into durable infrastructure so the next agent need
    not remember the incident.
  inputs: an important rule the model might ignore
  outputs: a guide entry plus an enforceable automated check
  steps: state rule as prose guidance -> encode same rule as an automated check -> let check hold when guidance is ignored
  missing_conditions: |
    Source does not cover rules that cannot be mechanically checked, the cost of maintaining checks,
    or false-positive handling in the check.
  tags: [durability, enforcement, harness, infrastructure]

- id: f06
  title: Anatomy of a loop (seven-part work-and-feedback cycle)
  type: framework
  source_chapter: "Part 2. Loop > Anatomy of a Loop"
  source_quote: |
    "Loop engineering starts when you design that cycle on purpose. Not 'ask again', not 'retry', but a real work-and-feedback system with a goal, evidence and a way to stop."
    "TRIGGER what starts a cycle / GOAL the exact condition we want, not 'keep improving' / STATE what the next cycle needs to know / ACTION what the agent is allowed to do / EVIDENCE how we know it worked / FEEDBACK what exactly failed / STOP when it ends, no matter what."
  summary: |
    Design the agent cycle deliberately with seven parts: trigger, goal, state, action, evidence, feedback,
    stop. This distinguishes an intentional loop from "ask again" or "retry": the loop has an exact goal,
    a way to know it worked, and a way to end regardless of confidence.
  inputs: a task and an evidence source
  outputs: a fully specified loop cycle
  steps: define trigger -> define exact goal -> define carried state -> bound action -> define evidence -> define feedback -> define stop
  missing_conditions: |
    Source assigns roles but gives no default values, no state schema, and no worked wiring of all seven
    fields (executable pseudo-code appears only under "Exits" and omits trigger/goal/action).
  tags: [loop, workflow, design]

- id: f07
  title: Evidence hierarchy (loop on evidence, not confidence)
  type: framework
  source_chapter: "Part 2. Loop > Not All Evidence Is Equal"
  source_quote: |
    "STRONGEST deterministic tests exit 0, schema validates, build compiles / observable the trace shows it really ran the test / independent a reviewer in a separate context / WEAKEST self-report 'looks good', 'I'm confident', 'should pass'."
    "A check is only as strong as the weakest thing it accepts as proof. If your loop accepts 'the model says it's done', it's a self-report loop no matter how many steps it has."
    "don't loop on confidence, loop on evidence. 'The agent says it's done' is not a stop condition. Tests passing is."
  summary: |
    Rank evidence strongest-to-weakest: deterministic (tests exit 0, schema validates, build compiles),
    observable (trace shows it really ran), independent (reviewer in a separate context), weakest self-report
    ("looks good"/"should pass"). A check is capped by the weakest proof it accepts; self-report can never be
    the stop condition.
  inputs: a claimed result and the checks available
  outputs: an evidence-strength classification and acceptable stop condition
  steps: identify proof the loop accepts -> rank on hierarchy -> reject self-report as a stop condition -> prefer deterministic/observable/independent proof
  missing_conditions: |
    No scoring rubric, no rule for tasks lacking a deterministic check, and no guidance on combining
    multiple evidence types.
  tags: [evidence, verification, loop, hierarchy]

- id: f08
  title: Write the check before the code (check is the spec)
  type: framework
  source_chapter: "Part 2. Loop > Write the Check Before the Code"
  source_quote: |
    "Before the agent touches a single file, write down what green means, and include a test that fails on the current code. A test that already passes before the fix proves nothing."
    "if you can't write the check, you don't actually understand the task yet. Writing the check is writing the spec."
  summary: |
    Before any code change, define "green" and add a test that fails on the current code; a test already
    green proves nothing. Inability to write the check signals the task is not yet understood — writing the
    check is writing the spec.
  inputs: a task description and the current code
  outputs: a failing check that defines green, functioning as the spec
  steps: write down what green means -> add a test failing on current code -> confirm it fails -> only then allow code changes
  missing_conditions: |
    Source explicitly concedes this is under-specified for open-ended tasks where no deterministic check
    exists; no fallback procedure is given.
  tags: [TDD, spec, verification, loop]

- id: f09
  title: Feedback, not verdicts (EXPECTED vs SAW message shape)
  type: framework
  source_chapter: "Part 2. Loop > Feedback, Not Verdicts"
  source_quote: |
    "'Red' is a verdict, and it tells the agent almost nothing. Real feedback says what was expected, what actually happened, where to look, and what has already been tried."
    "FAILED test_expired_session_redirect / EXPECTED 302 -> /login / SAW 302 -> /dashboard (auth/refresh.py:61) / FENCE auth/refresh.py only / DEAD ENDS middleware reorder."
    "EXPECTED vs SAW turns a red light into a direction. DEAD ENDS stops attempt three from quietly turning back into attempt one."
  summary: |
    Make loop feedback directional rather than a verdict. Report: FAILED test, EXPECTED value, SAW value
    with a location, a FENCE bounding the next change, and DEAD ENDS already tried. EXPECTED vs SAW gives
    direction; DEAD ENDS prevents attempt three from repeating attempt one.
  inputs: a failing check result and prior attempts
  outputs: a structured directional feedback message
  steps: name failed test -> state expected -> state saw with location -> fence the next change -> list dead ends
  missing_conditions: |
    One example only; no enforced schema in code, no rule for producing EXPECTED when the spec is absent,
    and no guidance on populating DEAD ENDS automatically.
  tags: [feedback, loop, debugging]

- id: f10
  title: Loop exits and the same-result-twice rule
  type: framework
  source_chapter: "Part 2. Loop > Exits"
  source_quote: |
    "A loop without exits isn't persistence, it's a cost leak."
    "for attempt in range(3): artifact = build(state); evidence = verify(artifact) # tests, not vibes; if evidence.passed: return artifact; if evidence.saw in state.dead_ends: # same result twice; break; state.dead_ends.append(evidence.saw); state.repair = evidence.gap; return escalate_to_human(state)."
    "When the agent gets the exact same result twice, it has stopped learning from the loop and more attempts won't help. The missing piece is something it can't see, or the task was framed wrong. A loop can fix the work, but it can't fix the question."
  summary: |
    Give every loop explicit exits: a retry cap, a token budget, and a same-result-twice rule. Each attempt
    builds then verifies with evidence; return on pass; if the observed result was already seen in dead_ends,
    break and escalate to a human. Same result twice means the loop has stopped learning, so escalate rather
    than retry.
  inputs: bounded attempts, verify(artifact), state.dead_ends
  outputs: a passed artifact or an escalated state
  steps: cap attempts -> build artifact -> verify with evidence -> return if passed -> break if saw is in dead_ends -> append saw, set repair=gap -> escalate to human
  missing_conditions: |
    Source does not specify retry-cap or budget numbers, the escalation channel/handoff format,
    or how to distinguish genuinely identical results from superficially identical ones.
  tags: [loop, exit, escalation, cost-control]

- id: f11
  title: Graph = nodes, edges, state (and a loop as a one-node graph)
  type: framework
  source_chapter: "Part 3. Graph > What It Is"
  source_quote: |
    "A graph is three things. Nodes are bounded jobs with one input and one output. Edges are real dependencies, where one node's output feeds another node's input. State is whatever survives between nodes."
    "NODE one bounded job, one input in, one output out / EDGE a real dependency, this output feeds that input / STATE what survives between nodes."
    "a loop is just a graph with one node and an edge back to itself. The graph doesn't replace your loops. It's what you need once several loops have to hand work off to each other."
  summary: |
    Model multi-step work as a graph: NODE = one bounded job (one input, one output), EDGE = a real dependency
    (one output feeds another input), STATE = what survives between nodes. A loop is a one-node graph with a
    self-edge; a graph becomes necessary when multiple loops must hand work off to each other.
  inputs: a multi-step task
  outputs: nodes, real dependency edges, shared state
  steps: identify bounded jobs -> map output-to-input dependencies -> define state that survives between nodes
  missing_conditions: |
    No formal node-granularity rule, no state consistency/concurrency rules, and no cycle handling beyond
    the one-node self-loop analogy.
  tags: [graph, orchestration, mental-model]

- id: f12
  title: The early-start test (prune fake dependencies)
  type: framework
  source_chapter: "Part 3. Graph > The Early-Start Test"
  source_quote: |
    "Most arrows in a workflow diagram aren't real dependencies. They're habits, just the order someone happened to think of the steps. So for every arrow, ask what would break if B started before A finished. If the answer is 'nothing', delete the arrow and run them in parallel."
    "Can the billing audit start before the fix lands? Yes, so it runs in parallel. Can the PR open before the fix lands? No, so that arrow is real."
  summary: |
    For every arrow in a workflow, ask what would break if the downstream step (B) started before the
    upstream step (A) finished. If nothing breaks, the arrow is a habit rather than a dependency: delete it
    and run the steps in parallel.
  inputs: a workflow diagram with arrows
  outputs: a pruned dependency graph with parallelized steps
  steps: for each arrow -> ask what breaks if B starts before A finishes -> if nothing, delete arrow and parallelize
  missing_conditions: |
    No rule for partial or conditional dependencies, and no procedure for verifying "nothing breaks"
    beyond the rhetorical question.
  tags: [graph, dependency-audit, parallelism]

- id: f13
  title: Four cuts that decide if a graph helps
  type: framework
  source_chapter: "Part 3. Graph > 4 Cuts That Decide If a Graph Helps"
  source_quote: |
    "Split where things fail separately. If two steps can break for different reasons, they're two nodes. If they always break together, they're one."
    "Give every worker its own context. Four agents sharing one context aren't a team, they're one agent wearing four hats."
    "If the answer should never change, it's code. Merging, sorting, deduping and counting are plain functions. Use a model only where a different answer could also be right."
    "Freeze what passed. Once a node gets through its gate, its output is read-only. When something fails, rerun only that node with its feedback."
  summary: |
    Four structural rules for a graph: (1) split nodes where failures have different causes, merge where
    they co-occur; (2) give each worker its own context; (3) keep deterministic work (merge/sort/dedupe/count)
    as code, use a model only where a different answer could also be right; (4) freeze passed nodes as
    read-only and rerun only the failing node with feedback.
  inputs: candidate steps of a workflow
  outputs: node boundaries, per-worker contexts, code-vs-model split, freeze policy
  steps: split by failure independence -> isolate each worker's context -> keep deterministic work as code -> freeze passed outputs and rerun only failures
  missing_conditions: |
    Source does not quantify "different reasons," gives no shared-context merge strategy, and covers no
    recovery path when a previously frozen output later proves wrong.
  tags: [graph, design-rules, orchestration]

- id: f14
  title: When not to use a graph (collapse-to-single-loop test)
  type: framework
  source_chapter: "Part 3. Graph > When Not to Use a Graph; 5 Mistakes That Kill Agent Systems"
  source_quote: |
    "Most tasks don't need one. If you can collapse your five nodes back into a single loop and lose nothing, do it."
    "Just don't reach for it until the work forces you to."
    "Building the graph too early. People draw a twelve-node diagram before they've watched the agent do the job once. Start with a harness and one loop, collect traces, and formalize only what actually deserves it."
  summary: |
    Decision test: most tasks do not need a graph. Try a single loop first; if the nodes collapse back into
    one loop without losing anything, keep the loop. Introduce a graph only when the work forces it. Avoid
    designing the graph before watching the agent do the job once — start with a harness and one loop,
    collect traces, and formalize only what deserves it.
  inputs: a proposed multi-node graph; observed traces
  outputs: keep-or-collapse decision and sequencing of when to add a graph
  steps: run a single loop first -> check whether collapsing loses anything -> if nothing lost keep the loop -> else add graph after traces justify it
  missing_conditions: |
    No objective criterion for "lose nothing" or "the work forces you to"; the decision is judgment-based
    and unquantified.
  tags: [graph, decision, minimalism]

- id: f15
  title: Human gates priced by cost of undo, not model confidence
  type: framework
  source_chapter: "Where You Sit in All This"
  source_quote: |
    "You're the slowest and most expensive node in the graph, so put yourself only where a mistake can't be taken back. Gate on the price of undo, not on the model's confidence."
    "ONE-CLICK UNDO docs, tests, one function ships on green / CLEANUP UNDO shared helpers, auth, schemas green + trace + second opinion / NO UNDO migrations, deletes, emails, $ a human signs."
    "The last tier has no score attached. Not 0.95, not 0.99. There's no number for the model to beat, so there's nothing to argue with."
  summary: |
    Place human approval gates by how reversible the action is, not by model confidence. One-click-undo work
    (docs, tests, one function) ships on green; cleanup-undo work (shared helpers, auth, schemas) needs green
    + trace + second opinion; no-undo work (migrations, deletes, emails, money) requires a human signature,
    where no score exists for the model to beat.
  inputs: an action class and its undo cost
  outputs: a gating policy for that action
  steps: classify action by undo cost -> apply green-only / green+trace+second-opinion / human-signature tier -> withhold numeric scores in the no-undo tier
  missing_conditions: |
    No rubric for classifying ambiguous actions, no rollback/abort mechanics, and no cost model defining
    "cleanup undo."
  tags: [gating, human-in-loop, risk, undo]

- id: f16
  title: Symptom -> owning-layer triage table
  type: framework
  source_chapter: "Which Layer Is Broken?"
  source_quote: |
    "Before you change anything, find your first symptom from the top of this list. That's your next fix, not the one after it."
    "SYMPTOM you copy-paste between chat and terminal -> harness (tools); it retries things it already tried -> harness (memory); 'done' means nothing until you check -> loop (the check); retries burn budget on the same error -> loop (feedback + exits); every step is right, the whole thing is slow -> graph (shape); one failure means everything reruns -> graph (gates); the same mistake comes back every week -> all layers (learning)."
  summary: |
    Triage table mapping observable symptoms to the layer that owns the fix: copy-paste between chat/terminal
    -> harness tools; repeats already-tried things -> harness memory; "done" means nothing -> loop check;
    retries burn budget on same error -> loop feedback+exits; steps right but slow -> graph shape; one failure
    reruns everything -> graph gates; recurring weekly mistake -> all layers (learning). Fix the first matching
    symptom from the top before deeper ones.
  inputs: an observed failure symptom
  outputs: the owning layer and fix target
  steps: list symptoms -> find the first matching symptom top-down -> fix that layer before the next
  missing_conditions: |
    No rule for multiple simultaneous symptoms, no severity weighting, and no verification step confirming
    the fix actually resolved the symptom.
  tags: [troubleshooting, triage, diagnosis]

- id: f17
  title: Failure -> lesson ledger (upgrade the layer that owns the class of failure)
  type: framework
  source_chapter: "Every Failure Should Upgrade the System"
  source_quote: |
    "Most people fix the output. Good teams fix the class of failure, and the trick is filing each lesson in the layer that owns it."
    "FAILURE couldn't see production logs -> read-only log tool -> harness; retried last week's dead approach -> line in the 'never' list -> harness; 'fixed' with no reproducing test -> required check in CI -> loop; same error 6 times in a row -> same-result-twice exit -> loop; two audits overlapped -> split rule in scope node -> graph."
    "Notice there's no 'prompt' row."
  summary: |
    After each failure, fix the class of failure, not just the output: file the lesson as a structural change
    in the layer that owns it. Missing visibility -> read-only log tool (harness); repeated dead approach ->
    "never" list (harness); unapproved file touch -> revoked permission (harness); "fixed" with no reproducing
    test -> required CI check (loop); same error repeatedly -> same-result-twice exit (loop); overlapping audits
    -> split rule (graph); mismatched review depth -> undo-price gate (graph). There is no "prompt" row:
    a prompt is a hope, while structure persists across model changes.
  inputs: a failure incident
  outputs: a durable structural lesson filed in the owning layer
  steps: classify the failure class -> choose the owning layer -> encode the lesson as structure (tool/check/rule/gate), not prompt text
  missing_conditions: |
    No procedure for choosing ownership when a failure spans layers, no prioritization among lessons,
    and no tracking/storage mechanism for the ledger itself.
  tags: [learning, postmortem, anti-fragility, workflow]
