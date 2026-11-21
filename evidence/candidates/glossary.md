# GLOSSARY — Harness / Loop / Graph (Sharingan RIA-TV++ Stage 1)

Source: @0xWhitemon, "Harness, Loop, Graph: The 3 Layers That Decide If Your AI
Agent Works" (2026-11-08), `source-article.txt` (355 lines). Line numbers cite
`source-article.txt`. Headings are the article's own.

> Note on terminology: the word "graph" here means a dependency graph of bounded
> jobs, NOT a knowledge graph; "evidence" means machine-checkable proof, NOT a
> log message. Keep author usage, not dictionary usage.

- id: g01
  term: Harness
  type: term
  source_chapter: "The 30-Second Version; Part 1. Harness (L18-28, L40-49)"
  author_definition: |
    "The harness is everything around the model that lets it do real work. The
    cleanest definition I know: remove the model from your architecture diagram,
    and everything still on the page is the harness." Six parts: contract, map,
    tools, memory, walls, traces. Axis: "HARNESS what the agent CAN do / environment".
  key_distinction: |
    ≠ "the prompt" or "the model" — neither is part of the harness.
    ≠ "framework" — it is the whole world around the model (terminal, tests,
       browser, project memory, permissions), not a library.
    = environment; the thing that makes the agent capable, not correct.
  why_it_matters: |
    Downstream skills must diagnose harness failures (missing tools, stale
    state, no permissions) before touching prompts or model choice.
  tags: [term, core-concept, layer]

- id: g02
  term: Loop
  type: term
  source_chapter: "The 30-Second Version; Part 2. Loop; What It Is (L22-26, L120-122, L210)"
  author_definition: |
    "Loop engineering starts when you design that cycle on purpose. Not 'ask
    again', not 'retry', but a real work-and-feedback system with a goal,
    evidence and a way to stop." "A loop is just a graph with one node and an
    edge back to itself." Axis: "LOOP how it knows it's RIGHT / evidence".
  key_distinction: |
    ≠ "retry loop" — a bare retry with no goal/evidence/stop is a cost leak.
    ≠ a separate technology from graph — a graph generalizes the loop.
    = evidence-driven cycle; makes the agent honest.
  why_it_matters: |
    Skills must never emit "keep trying" as a loop; every loop needs a check
    that can fail and an exit.
  tags: [term, core-concept, layer]

- id: g03
  term: Graph
  type: term
  source_chapter: "The 30-Second Version; Part 3. Graph / What It Is (L26, L196-210)"
  author_definition: |
    "A graph is three things. Nodes are bounded jobs with one input and one
    output. Edges are real dependencies, where one node's output feeds another
    node's input. State is whatever survives between nodes." Axis: "GRAPH what
    happens NEXT / flow." "Needed once several loops have to hand work off to
    each other."
  key_distinction: |
    ≠ knowledge graph / graph database — it is a dependency graph of work.
    ≠ always necessary — "most tasks don't need one"; collapse to a single
       loop if nothing is lost.
    = coordination / flow; makes the agent organized.
  why_it_matters: |
    Prevents skills from building twelve-node orchestration for one-step jobs.
  tags: [term, core-concept, layer]

- id: g04
  term: Contract / done_when
  type: term
  source_chapter: "Part 1. Harness > 1. Contract (L54-64)"
  author_definition: |
    "Before the agent acts, turn the request into something with a finish line."
    Fields: goal, inputs, output, constraints, done_when. "The most important
    field here is done_when. Without it the agent will quietly solve an easier
    version of the task and tell you it's done."
  key_distinction: |
    ≠ "goal" — goal is direction; done_when is the testable finish line.
    ≠ a wish ("should pass") — it must be checkable (new test reproduces bug,
       same test passes after fix, full suite green).
  why_it_matters: |
    Any skill that delegates work must emit a contract with an explicit,
    machine-verifiable done_when or the agent will self-declare success.
  tags: [term, harness-part, success-criteria]

- id: g05
  term: Map (vs manual)
  type: term
  source_chapter: "Part 1. Harness > 2. Map (L66-74)"
  author_definition: |
    "Don't dump every doc into the context window. Give the agent a short root
    file that tells it where things live, and let it load the details only when
    the task needs them." "Context isn't storage, it's an attention budget. A
    map saves it, a giant manual eats it before the agent writes a single line."
  key_distinction: |
    ≠ documentation dump / onboarding manual — a map is an index (AGENTS.md
       pointing to docs/architecture.md etc.), loaded on demand.
    = attention-budget preservation.
  why_it_matters: |
    Skills should produce a root index, not paste full docs into the prompt.
  tags: [term, harness-part, context]

- id: g06
  term: Tool contract / failure state
  type: term
  source_chapter: "Part 1. Harness > 3. Tools (L76-83)"
  author_definition: |
    "Every tool you add is one more way for the model to be wrong, so ten narrow
    tools beat forty overlapping ones. Each tool needs a clear input, a
    predictable output, an explicit failure state and a permission level."
  key_distinction: |
    ≠ "more tools = more capable" — more tools mean more wrong choices; a good
       harness is precise, not crowded.
    ≠ happy-path-only spec — failure state and permission level are mandatory.
  why_it_matters: |
    Tool-design skills must specify input/output/failure/permission and prefer
    narrow, non-overlapping tools.
  tags: [term, harness-part, tools]

- id: g07
  term: Memory-as-disk
  type: term
  source_chapter: "Part 1. Harness > 4. Memory (L85-94)"
  author_definition: |
    "The context window is RAM and the harness is the disk. Decisions, dead
    ends and open risks go into files and git commits, not into the chat."
    PROGRESS.md stores goal / tried / known / next / never so the next session
    "inherits the actual state of the work instead of a blurry summary of the
    conversation."
  key_distinction: |
    ≠ conversation history / chat summary — durable state lives in files
       (PROGRESS.md, git commits).
    ≠ the model's parametric memory — this is external, inspectable storage.
  why_it_matters: |
    Skills must persist state to disk so crashes/context resets/handoffs
    survive; never rely on the chat transcript as memory.
  tags: [term, harness-part, memory]

- id: g08
  term: Walls
  type: term
  source_chapter: "Part 1. Harness > 5. Walls (L96)"
  author_definition: |
    "'Please don't touch migrations' is a wish. A permission the agent doesn't
    have is a wall. The model can suggest an action, but a policy outside the
    model decides whether it runs. Never let the same system invent the plan,
    approve the risk and execute the side effect."
  key_distinction: |
    ≠ instructions / guardrail prose — a wall is an enforced external policy.
    = separation of plan, approval and execution across systems.
  why_it_matters: |
    Skills must encode prohibitions as permissions enforcement, not as
    "please don't" text in the prompt.
  tags: [term, harness-part, permissions]

- id: g09
  term: Traces
  type: term
  source_chapter: "Part 1. Harness > 6. Traces (L98); L286"
  author_definition: |
    "Every run should leave a trail you can actually read: what context was
    loaded, which tools were called, what changed, which tests ran, how many
    retries, how much it cost. Without traces a failure is a mystery. With
    traces it's input for the next fix."
  key_distinction: |
    ≠ raw logs — a trace is a readable, decision-relevant record of the run.
    = raw material for loop feedback and for formalizing a graph later.
  why_it_matters: |
    Skills should require trace capture before attempting graph design
    ("start with a harness and one loop, collect traces").
  tags: [term, harness-part, observability]

- id: g10
  term: Write It Twice
  type: term
  source_chapter: "The 'Write It Twice' Trick (L100-110)"
  author_definition: |
    "Write every important rule twice: once as guidance the agent can
    understand, and once as a check it can't get around." GUIDE (AGENTS.md,
    reason) + CHECK (CI, lint fails if src/ui/** imports src/db/**). "Over time
    this turns past mistakes into infrastructure, so the next agent doesn't have
    to remember the incident because the harness remembers it."
  key_distinction: |
    ≠ repeating the rule in two prompts — the second copy is an enforced,
    non-negotiable check (CI/lint), not more prose.
  why_it_matters: |
    Core mechanism: when a model may ignore guidance, skills must back the
    rule with an automated check that holds regardless.
  tags: [term, mechanism, learning]

- id: g11
  term: Loop anatomy (trigger / goal / state / action / evidence / feedback / stop)
  type: term
  source_chapter: "Part 2. Loop > Anatomy of a Loop (L126-138)"
  author_definition: |
    TRIGGER "what starts a cycle (failed test, new ticket, schedule)"; GOAL
    "the exact condition we want, not 'keep improving'"; STATE "what the next
    cycle needs to know"; ACTION "what the agent is allowed to do"; EVIDENCE
    "how we know it worked"; FEEDBACK "what exactly failed"; STOP "when it ends,
    no matter what."
  key_distinction: |
    ≠ generic "plan→act→observe" — includes an explicit STOP and a
       machine-checkable EVIDENCE, both mandatory.
    = the seven-part schema a skill should emit when designing any loop.
  why_it_matters: |
    Provides the checklist fields; missing STOP = cost leak, missing EVIDENCE
    = self-report loop.
  tags: [term, loop-part, schema]

- id: g12
  term: Evidence hierarchy (deterministic > observable > independent > self-report)
  type: term
  source_chapter: "Part 2. Loop > Not All Evidence Is Equal (L140-149); L138"
  author_definition: |
    "STRONGEST deterministic — tests exit 0, schema validates, build compiles;
    observable — the trace shows it really ran the test; independent — a
    reviewer in a separate context; WEAKEST self-report — 'looks good', 'I'm
    confident', 'should pass'." "Don't loop on confidence, loop on evidence. ...
    A check is only as strong as the weakest thing it accepts as proof."
  key_distinction: |
    ≠ "the agent says it's done" — that is self-report, the weakest tier, and
       is NOT a stop condition.
    ≠ trusting a passing test blindly — observable evidence requires the trace
       to confirm the test actually ran.
  why_it_matters: |
    Skills must grade their completion proofs against this hierarchy and reject
    self-report; a self-review shares the original blind spots (L288).
  tags: [term, loop-part, evidence]

- id: g13
  term: Expected vs Saw (feedback, not verdicts)
  type: term
  source_chapter: "Part 2. Loop > Feedback, Not Verdicts (L155-165)"
  author_definition: |
    "'Red' is a verdict, and it tells the agent almost nothing. Real feedback
    says what was expected, what actually happened, where to look, and what has
    already been tried." Format: FAILED / EXPECTED (302 -> /login) / SAW
    (302 -> /dashboard, auth/refresh.py:61) / FENCE / DEAD ENDS. "EXPECTED vs
    SAW turns a red light into a direction."
  key_distinction: |
    ≠ pass/fail verdict ("red", "failed") — a verdict is information-free.
    ≠ generic error text — feedback is directional: expected, saw, location,
       fence, dead ends.
  why_it_matters: |
    Skills generating repair instructions must emit EXPECTED vs SAW with a file
    location, not just "tests failed".
  tags: [term, loop-part, feedback]

- id: g14
  term: Dead ends
  type: term
  source_chapter: "Part 2. Loop > Feedback, Not Verdicts (L163-165); Exits (L177-180)"
  author_definition: |
    DEAD ENDS is the list of approaches already tried (e.g. "middleware
    reorder"), carried in feedback/state. "DEAD ENDS stops attempt three from
    quietly turning back into attempt one." Also stored in memory (PROGRESS.md
    "tried", "never") and in the harness "never" list (L273).
  key_distinction: |
    ≠ generic failure history — it is a per-task blacklist consumed by the
       loop to prevent repeat attempts.
    ≠ a one-time note — it persists across contexts/sessions.
  why_it_matters: |
    Skills must record dead ends durably so retries don't regress to prior
    failed approaches.
  tags: [term, loop-part, memory]

- id: g15
  term: Same-result-twice exit
  type: term
  source_chapter: "Part 2. Loop > Exits (L167-184); checklist L317; ledger L276"
  author_definition: |
    "When the agent gets the exact same result twice, it has stopped learning
    from the loop and more attempts won't help. The missing piece is something
    it can't see, or the task was framed wrong. A loop can fix the work, but it
    can't fix the question." So: break and escalate_to_human(state).
  key_distinction: |
    ≠ retry cap (fixed number of tries) — this is result-based: identical
       evidence.saw triggers escape early, regardless of count.
    ≠ "keep trying harder" — extra attempts cannot fix a mis-framed task.
  why_it_matters: |
    Skills must specify escalation on repeated identical evidence, not just a
    numeric retry budget.
  tags: [term, loop-part, exit, escalation]

- id: g16
  term: Node / Edge / State (graph primitives)
  type: term
  source_chapter: "Part 3. Graph > What It Is (L202-210)"
  author_definition: |
    NODE "one bounded job, one input in, one output out"; EDGE "a real
    dependency, this output feeds that input"; STATE "what survives between
    nodes." Edges must be real dependencies, not habits (see early-start test).
  key_distinction: |
    ≠ task / subtask generically — a node is bounded with exactly one input
       and one output.
    ≠ assumed ordering — an edge exists only if B genuinely needs A's output.
  why_it_matters: |
    Graph-design skills use these three primitives and must justify each edge.
  tags: [term, graph-part, schema]

- id: g17
  term: Early-start test
  type: term
  source_chapter: "Part 3. Graph > The Early-Start Test (L214-218); checklist L322"
  author_definition: |
    "Most arrows in a workflow diagram aren't real dependencies. They're
    habits... So for every arrow, ask what would break if B started before A
    finished. If the answer is 'nothing', delete the arrow and run them in
    parallel."
  key_distinction: |
    ≠ "the order someone happened to think of the steps" — a dependency must
       have a concrete breakage if reversed.
    = a pruning test that converts serial workflows into parallel ones.
  why_it_matters: |
    Skills must audit every arrow with this test before accepting a graph; fake
    dependencies are the main source of slow serial flows.
  tags: [term, graph-part, test]

- id: g18
  term: Freeze what passed
  type: term
  source_chapter: "Part 3. Graph > 4 Cuts (L228); checklist L324"
  author_definition: |
    "Once a node gets through its gate, its output is read-only. When something
    fails, rerun only that node with its feedback. Rerunning good work is just a
    free chance to break it."
  key_distinction: |
    ≠ rerun the whole pipeline on any failure — only the failing node is
       retried; passed nodes are immutable.
    = gating that makes graph failure local instead of global ("one failure
       means everything reruns" is the symptom, graph gates the fix, L264).
  why_it_matters: |
    Skills building multi-step flows must mark passed artifacts read-only and
    retry only the failed node.
  tags: [term, graph-part, gating]

- id: g19
  term: Undo-priced gate
  type: term
  source_chapter: "Where You Sit in All This (L238-248); checklist L325; ledger L278"
  author_definition: |
    "Gate on the price of undo, not on the model's confidence": ONE-CLICK UNDO
    (docs, tests, one function) ships on green; CLEANUP UNDO (helpers, auth,
    schemas) needs green + trace + second opinion; NO UNDO (migrations, deletes,
    emails, money) needs a human signature. "The last tier has no score
    attached... there's nothing to argue with."
  key_distinction: |
    ≠ confidence threshold (0.95 / 0.99) — gating is by reversibility, not
       probability.
    ≠ "agent never needs you" — humans are placed where mistakes can't be
       taken back; a model score cannot decide that.
  why_it_matters: |
    Skills must classify actions by undo cost and route irreversible ones to a
    human gate, never by model self-confidence.
  tags: [term, gating, human-in-the-loop]

- id: g20
  term: Environment / evidence / flow (the three-layer axis)
  type: term
  source_chapter: "The 30-Second Version (L24-28); The Real Shift (L331-345)"
  author_definition: |
    "HARNESS what the agent CAN do / environment; LOOP how it knows it's RIGHT
    / evidence; GRAPH what happens NEXT / flow." Mnemonic: "environment, then
    feedback, then flow." Closing: "The harness makes the agent capable. The
    loop makes it honest. The graph makes it organized." Also PROMPT→instruction,
    CONTEXT→working view, GRAPH→coordination.
  key_distinction: |
    ≠ "three interchangeable words for agent" — each fixes a different failure
       class; fixing the wrong layer wastes a week.
    = the triage axis: identify which layer owns a symptom before changing
       anything (see symptom→layer table L258-265).
  why_it_matters: |
    Master key for all downstream skills: route every failure to the owning
    layer; "next time your agent says 'done', ask which layer said so."
  tags: [term, core-concept, axis]

## Flagged: terms used but never defined in the source
- "green" (passing state) — used throughout ("ships on green", "write down what
  green means") but never formally defined; best gloss: all required checks pass.
- "second opinion" (L245, L288) — used as a review mechanism, never defined;
  context: a reviewer in a separate context.
- "sandbox / worktree" (L80, L308) — assumed known; no definition.
- "skills / hooks / MCP / modes / subagents / plugins" (L34) — listed as parts
  of the current agent stack, none defined; treated as background vocabulary.
- "gate" — used in "its gate", "undo-price gate" without a standalone definition;
  gloss: the check a node/action must pass before proceeding.
- "Karpathy list" / "tip number five" — referenced, not reproduced; source is
  second-hand.
