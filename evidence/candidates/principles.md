# Principle Candidates — Harness / Loop / Graph (Sharingan Stage 1)

Source: `source-article.txt` (@0xWhitemon, "Harness, Loop, Graph: The 3 Layers That Decide If Your AI Agent Works"). `tweet.json` (@0xoctocat) is a pointer only — no methodology. `source` fields cite article heading names.

```yaml
- id: p01
  title: Three Layers — Harness / Loop / Graph
  type: principle
  source_chapter: "The 30-Second Version" (also "The Real Shift")
  source_quote: |
    "HARNESS what the agent CAN do environment / LOOP how it knows it's RIGHT evidence /
    GRAPH what happens NEXT flow." "If you remember one line from this article, make it
    this one: environment, then feedback, then flow."
  summary: |
    Three layers fix three different failure classes; fixing the wrong one burns a week
    debugging a layer that was fine. Mnemonic: environment -> feedback -> flow. Closing
    form: prompt=instruction, context=working view, harness=environment, loop=evidence,
    graph=coordination; "harness makes capable, loop makes honest, graph makes organized."
  tags: [principle, taxonomy, three-axis-table]

- id: p02
  title: Harness Definition — Remove the Model
  type: rule
  source_chapter: "Part 1. Harness"
  source_quote: |
    "remove the model from your architecture diagram, and everything still on the page
    is the harness."
  summary: |
    Operational boundary test for what counts as harness: everything except the model
    weights. Same model + better environment ships features; the weights didn't change.
  tags: [rule, definition, harness]

- id: p03
  title: The 6 Parts of a Real Harness
  type: checklist
  source_chapter: "The 6 Parts of a Real Harness"
  source_quote: |
    "1. Contract ... 2. Map ... 3. Tools ... 4. Memory ... 5. Walls ... 6. Traces."
  summary: |
    A real harness = Contract (finish line, done_when), Map (short root index), Tools
    (narrow contracts + permissions), Memory (files/git, not chat), Walls (policy outside
    model), Traces (readable run log). Six-item design checklist.
  tags: [checklist, harness]

- id: p04
  title: Define Success (done_when) Before the Run
  type: principle
  source_chapter: "The 6 Parts of a Real Harness" (1. Contract)
  source_quote: |
    "The most important field here is done_when. Without it the agent will quietly solve
    an easier version of the task and tell you it's done."
  summary: |
    Contract fields: goal, inputs, output, constraints, done_when. Checklist form:
    "Success is defined before the run starts." A finish line prevents solving an easier
    task and declaring done.
  tags: [principle, done-when, contract]

- id: p05
  title: Context Is an Attention Budget — Map, Not Manual
  type: maxim
  source_chapter: "The 6 Parts of a Real Harness" (2. Map)
  source_quote: |
    "Context isn't storage, it's an attention budget. A map saves it, a giant manual eats
    it before the agent writes a single line." "Don't dump every doc into the context
    window. Give the agent a short root file that tells it where things live."
  summary: |
    Treat context as scarce attention; use a short root index (AGENTS.md) pointing to
    detail docs loaded on demand. Checklist: "The root guide is a map, not a manual."
  tags: [maxim, context, attention-budget]

- id: p06
  title: Ten Narrow Tools Beat Forty Overlapping
  type: rule
  source_chapter: "The 6 Parts of a Real Harness" (3. Tools)
  source_quote: |
    "Every tool you add is one more way for the model to be wrong, so ten narrow tools
    beat forty overlapping ones. Each tool needs a clear input, a predictable output, an
    explicit failure state and a permission level."
  summary: |
    Tool-count threshold rule; per-tool contract = input, output, failure state,
    permission. Checklist: "Every tool has a clear contract and failure state"; "The
    agent runs in a sandbox or worktree." More tools = more wrong choices, not better.
  tags: [rule, tools, harness]

- id: p07
  title: Memory — Context Is RAM, Harness Is Disk
  type: principle
  source_chapter: "The 6 Parts of a Real Harness" (4. Memory)
  source_quote: |
    "The context window is RAM and the harness is the disk. Decisions, dead ends and open
    risks go into files and git commits, not into the chat."
  summary: |
    Persist decisions/dead ends/open risks in files (PROGRESS.md: goal, tried, known,
    next, never). Checklist: "Decisions live in files, not in the chat." Survives crash,
    reset, handoff; next session inherits actual state.
  tags: [principle, memory, harness]

- id: p08
  title: Walls — Separate Plan, Approve, Execute
  type: rule
  source_chapter: "The 6 Parts of a Real Harness" (5. Walls)
  source_quote: |
    "\"Please don't touch migrations\" is a wish. A permission the agent doesn't have is
    a wall. ... Never let the same system invent the plan, approve the risk and execute
    the side effect."
  summary: |
    A request in prose is not a boundary; an enforced permission is. Hard rule against
    one system both proposing, approving and executing a side effect.
  tags: [rule, permissions, walls]

- id: p09
  title: Traces — Every Run Leaves a Readable Trail
  type: checklist
  source_chapter: "The 6 Parts of a Real Harness" (6. Traces)
  source_quote: |
    "Every run should leave a trail you can actually read: what context was loaded, which
    tools were called, what changed, which tests ran, how many retries, how much it cost.
    Without traces a failure is a mystery. With traces it's input for the next fix."
  summary: |
    Trace fields: context loaded, tools called, changes, tests run, retries, cost.
    Checklist: "Every tool call is traced." Turns failures into fix input.
  tags: [checklist, traces, observability]

- id: p10
  title: Write Every Important Rule Twice
  type: principle
  source_chapter: "The \"Write It Twice\" Trick"
  source_quote: |
    "The fix is to write every important rule twice: once as guidance the agent can
    understand, and once as a check it can't get around." "GUIDE (AGENTS.md) ... UI code
    may not query the database directly / CHECK (CI) ... lint fails if src/ui/** imports
    src/db/**."
  summary: |
    Guidance explains the reason; the check holds even when the model ignores guidance.
    Converts past mistakes into infrastructure — "the harness remembers it." No prompt
    row later: a prompt is a hope, a scheduler/CI rule is structure.
  tags: [principle, write-twice, enforcement]

- id: p11
  title: Anatomy of a Loop — Seven Fields
  type: checklist
  source_chapter: "Anatomy of a Loop"
  source_quote: |
    "TRIGGER what starts a cycle ... GOAL the exact condition we want, not \"keep
    improving\" ... STATE what the next cycle needs to know ... ACTION what the agent is
    allowed to do ... EVIDENCE how we know it worked ... FEEDBACK what exactly failed ...
    STOP when it ends, no matter what."
  summary: |
    Loop engineering = designing the work-and-feedback cycle on purpose (not "ask again"/
    "retry"): goal, evidence and a way to stop. Seven-field design checklist.
  tags: [checklist, loop, anatomy]

- id: p12
  title: Don't Loop on Confidence, Loop on Evidence
  type: maxim
  source_chapter: "Anatomy of a Loop"
  source_quote: |
    "The most important rule of loop engineering fits in one line: don't loop on
    confidence, loop on evidence. \"The agent says it's done\" is not a stop condition.
    Tests passing is."
  summary: |
    Load-bearing one-line rule; only rejectable evidence may close a loop, never
    self-reported completion or a confidence score.
  tags: [maxim, loop, evidence]

- id: p13
  title: Evidence Hierarchy — Strongest to Weakest
  type: principle
  source_chapter: "Not All Evidence Is Equal"
  source_quote: |
    "STRONGEST deterministic tests exit 0, schema validates, build compiles / observable
    the trace shows it really ran the test / independent a reviewer in a separate
    context / WEAKEST self-report \"looks good\", \"I'm confident\", \"should pass\"."
  summary: |
    Four-tier evidence ranking used to grade any stop condition: deterministic >
    observable > independent > self-report. Mirrors "use tests first, a reviewer in a
    separate context second, a human for anything you can't undo."
  tags: [principle, evidence-hierarchy, threshold]

- id: p14
  title: A Check Is Only as Strong as the Weakest Proof It Accepts
  type: rule
  source_chapter: "Not All Evidence Is Equal"
  source_quote: |
    "A check is only as strong as the weakest thing it accepts as proof. If your loop
    accepts \"the model says it's done\", it's a self-report loop no matter how many steps
    it has."
  summary: |
    Strength of a check is set by its weakest accepted evidence, not its step count or
    complexity. Reject self-report as proof.
  tags: [rule, evidence, check-strength]

- id: p15
  title: Write the Check Before the Code
  type: principle
  source_chapter: "Write the Check Before the Code"
  source_quote: |
    "Before the agent touches a single file, write down what green means, and include a
    test that fails on the current code. A test that already passes before the fix proves
    nothing. ... if you can't write the check, you don't actually understand the task yet.
    Writing the check is writing the spec."
  summary: |
    Define green + a currently-failing test up front. Checklist: "Green is written before
    the code"; "The check fails at least once on purpose." Inability to write the check
    = not yet understanding the task (critique: under-specified for open-ended tasks).
  tags: [principle, test-first, spec]

- id: p16
  title: Feedback as EXPECTED vs SAW, Not Verdicts
  type: template
  source_chapter: "Feedback, Not Verdicts"
  source_quote: |
    "Real feedback says what was expected, what actually happened, where to look, and what
    has already been tried: FAILED test_expired_session_redirect / EXPECTED 302 -> /login
    / SAW 302 -> /dashboard (auth/refresh.py:61) / FENCE auth/refresh.py only / DEAD ENDS
    middleware reorder. \"EXPECTED vs SAW turns a red light into a direction.\""
  summary: |
    Feedback template fields = FAILED, EXPECTED, SAW (with location), FENCE, DEAD ENDS.
    A bare "Red" is a verdict, not direction; DEAD ENDS stops attempt three reverting to
    attempt one. Checklist: "Feedback says expected vs saw."
  tags: [template, feedback, expected-vs-saw]

- id: p17
  title: Loop Exits — Retry Cap, Same-Result-Twice, Escalate
  type: rule
  source_chapter: "Exits"
  source_quote: |
    "A loop without exits isn't persistence, it's a cost leak." "When the agent gets the
    exact same result twice, it has stopped learning from the loop and more attempts won't
    help." "if evidence.saw in state.dead_ends: # same result twice -> break ...
    return escalate_to_human(state)"
  summary: |
    Exit thresholds: fixed retry cap (for attempt in range(3)), same-result-twice ->
    break, then escalate_to_human. "A loop can fix the work, but it can't fix the
    question." Checklist: "There's a retry cap and a token budget"; "Same result twice
    means escalate."
  tags: [rule, exits, escalation, threshold]

- id: p18
  title: Graph = Nodes, Edges, State; a Loop Is a One-Node Graph
  type: principle
  source_chapter: "What It Is" (Part 3)
  source_quote: |
    "A graph is three things. Nodes are bounded jobs with one input and one output. Edges
    are real dependencies, where one node's output feeds another node's input. State is
    whatever survives between nodes." "a loop is just a graph with one node and an edge
    back to itself."
  summary: |
    Graph = NODE (one bounded job, one in/out) + EDGE (real dependency) + STATE (survives
    between nodes). Doesn't replace loops; needed only when several loops hand work off.
  tags: [principle, graph, definition]

- id: p19
  title: The Early-Start Test
  type: rule
  source_chapter: "The Early-Start Test"
  source_quote: |
    "for every arrow, ask what would break if B started before A finished. If the answer
    is \"nothing\", delete the arrow and run them in parallel."
  summary: |
    Prune fake dependencies (habits, not real dependencies). Example: billing audit can
    start before the fix (parallel); PR cannot open before the fix (real arrow).
    Checklist: "Every arrow passed the early-start test."
  tags: [rule, graph, dependency-audit]

- id: p20
  title: Split Where Things Fail Separately
  type: rule
  source_chapter: "4 Cuts That Decide If a Graph Helps"
  source_quote: |
    "Split where things fail separately. If two steps can break for different reasons,
    they're two nodes. If they always break together, they're one."
  summary: |
    Node-boundary rule keyed on distinct failure reasons, not on task topic.
  tags: [rule, graph, split-rule]

- id: p21
  title: Give Every Worker Its Own Context
  type: rule
  source_chapter: "4 Cuts That Decide If a Graph Helps"
  source_quote: |
    "Give every worker its own context. Four agents sharing one context aren't a team,
    they're one agent wearing four hats. The first opinion written down becomes everyone's
    opinion."
  summary: |
    Separate context per worker prevents one agent's first opinion anchoring all others.
    Checklist: "Each worker has its own context."
  tags: [rule, graph, context]

- id: p22
  title: If the Answer Should Never Change, It's Code
  type: rule
  source_chapter: "4 Cuts That Decide If a Graph Helps"
  source_quote: |
    "If the answer should never change, it's code. Merging, sorting, deduping and counting
    are plain functions. Use a model only where a different answer could also be right."
  summary: |
    Deterministic work stays code; spend model calls only where multiple answers could be
    valid.
  tags: [rule, graph, deterministic]

- id: p23
  title: Freeze What Passed
  type: rule
  source_chapter: "4 Cuts That Decide If a Graph Helps"
  source_quote: |
    "Freeze what passed. Once a node gets through its gate, its output is read-only. When
    something fails, rerun only that node with its feedback. Rerunning good work is just a
    free chance to break it."
  summary: |
    Passed nodes are immutable; rerun only the failing node with its feedback.
    Checklist: "Passed nodes are frozen."
  tags: [rule, graph, gates, rerun]

- id: p24
  title: When Not to Use a Graph
  type: rule
  source_chapter: "When Not to Use a Graph"
  source_quote: |
    "Most tasks don't need one. If you can collapse your five nodes back into a single
    loop and lose nothing, do it. ... Just don't reach for it until the work forces you
    to."
  summary: |
    Collapse-to-loop test before adding orchestration. Checklists: "You tried to keep it
    a single loop first." Naming is new (LangGraph/Google ADK did nodes before), the move
    is real but not mandatory.
  tags: [rule, graph, restraint]

- id: p25
  title: Gate by Price of Undo, Not Model Confidence
  type: principle
  source_chapter: "Where You Sit in All This"
  source_quote: |
    "Gate on the price of undo, not on the model's confidence: ONE-CLICK UNDO docs, tests,
    one function ships on green / CLEANUP UNDO shared helpers, auth, schemas green + trace
    + second opinion / NO UNDO migrations, deletes, emails, $ a human signs." "The last
    tier has no score attached. Not 0.95, not 0.99."
  summary: |
    Three-tier human-gating threshold table by reversibility. No-undo tier has no score
    for the model to beat, so nothing to argue with. Checklist: "Gates are priced by undo,
    not confidence." Human = slowest, most expensive node — place only where mistakes
    can't be taken back.
  tags: [principle, gating, undo-cost, threshold]

- id: p26
  title: Symptom -> Layer Triage Table
  type: checklist
  source_chapter: "Which Layer Is Broken?"
  source_quote: |
    "Before you change anything, find your first symptom from the top of this list. That's
    your next fix, not the one after it." "you copy-paste between chat and terminal ->
    harness (tools) / it retries things it already tried -> harness (memory) / \"done\"
    means nothing -> loop (the check) / retries burn budget on same error -> loop
    (feedback + exits) / every step right, whole thing slow -> graph (shape) / one failure
    means everything reruns -> graph (gates) / same mistake every week -> all layers."
  summary: |
    Ordered symptom-to-layer mapping for triage; pick the topmost matching symptom as the
    next fix. Seven symptom rows spanning harness/loopgraph/all.
  tags: [checklist, triage, symptom-table]

- id: p27
  title: Every Failure Should Upgrade the System (Failure -> Lesson Ledger)
  type: template
  source_chapter: "Every Failure Should Upgrade the System"
  source_quote: |
    "Most people fix the output. Good teams fix the class of failure, and the trick is
    filing each lesson in the layer that owns it." "couldn't see production logs ->
    read-only log tool -> harness / retried last week's dead approach -> line in the
    \"never\" list -> harness / \"fixed\" with no reproducing test -> required check in CI
    -> loop / same error 6 times -> same-result-twice exit -> loop / two audits overlapped
    -> split rule in scope node -> graph."
  summary: |
    Ledger template columns: FAILURE, LESSON BECOMES, LAYER. "Notice there's no 'prompt'
    row" — prompt fixes are hopes, structure fixes persist; "a test reads the same way
    forever."
  tags: [template, learning, ledger]

- id: p28
  title: 5 Mistakes That Kill Agent Systems
  type: checklist
  source_chapter: "5 Mistakes That Kill Agent Systems"
  source_quote: |
    "1. Building the graph too early ... Start with a harness and one loop, collect
    traces ... 2. The same model writes and grades ... 3. \"Keep trying\" as a loop ...
    an open tab on your credit card ... 4. The harness as a junk drawer ... 5. Blaming the
    model."
  summary: |
    Five anti-patterns: graph too early; self-review shares blind spots (tests first,
    separate-context reviewer second, human for irreversible); "keep trying" isn't a loop;
    crowded harness = more wrong choices; fix the layer that owns the failure.
  tags: [checklist, anti-patterns, mistakes]

- id: p29
  title: The Checklist — Harness / Loop / Graph
  type: checklist
  source_chapter: "The Checklist"
  source_quote: |
    "Harness: Success is defined before the run starts / The root guide is a map, not a
    manual / Every tool has a clear contract and failure state / Decisions live in files,
    not in the chat / The agent runs in a sandbox or worktree / Every tool call is traced.
    Loop: Green written before the code / check fails at least once on purpose / feedback
    says expected vs saw / retry cap and token budget / same result twice means escalate.
    Graph: tried single loop first / arrows passed early-start test / own context per
    worker / passed nodes frozen / gates priced by undo."
  summary: |
    Consolidated 16-item pre-flight checklist across the three layers. "If several of
    these are a no, a smarter model won't save you. It'll just make the failure faster and
    more expensive."
  tags: [checklist, preflight, harness-loop-graph]
```
