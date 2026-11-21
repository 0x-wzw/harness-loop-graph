# Cases — Harness / Loop / Graph (Sharingan Stage 1, case extractor)

Source: `source-article.txt` (@0xWhitemon, "Harness, Loop, Graph: The 3 Layers That Decide If Your AI Agent Works", 2026-11-08). `tweet.json` (@0xoctocat) is a pointer only; `BOOK_OVERVIEW.md` records that the Karpathy video was NOT transcribed and that several name-drops lack links/detail. No outcomes are invented: article-silent results are marked "未说明/未给出".

Convention: `example_kind` describes the material *as it appears in the article*. `evidence_status` = `source-reported` (author asserts a third party's case) vs `demonstrated-in-text` (concrete artifact/table/code actually printed).

```yaml
- id: c01
  title: "OpenAI built a product with Codex and zero hand-written code"
  type: case
  example_kind: reported_case
  evidence_status: source-reported
  source_chapter: "Part 1. Harness"
  source_quote: |
    "OpenAI ran into exactly this when they built a product with Codex and zero
    hand-written code. Early progress was slow, and it wasn't because the model
    was weak. The environment was underspecified. Their fix wasn't 'try harder'.
    They asked which capability was missing, then made it visible and enforceable
    for the agent."
  summary: |
    作者转述 OpenAI 用 Codex、零手写代码构建产品的经历：早期进展慢，原因不是模型弱，
    而是环境（harness）未被充分说明；修复方式是识别缺失能力并让它对 agent 可见、可执行。
  bound_to:
    - "harness = environment（模型之外的系统才决定能不能干活）"
    - "underspecified environment 是失败的根因，而非模型能力"
  outcome: |
    未说明。文章未给出任何量化结果、链接或可核实细节（BOOK_OVERVIEW.md 明确指出此为
    name-drop，无链接/细节）。仅陈述"修复方式"的定性描述。
  caveat: "Source-reported name-drop; no link, no verifiable detail, no measured outcome."
  tags: [case, harness, openai, codex, name-drop, source-reported]

- id: c02
  title: "Mitchell Hashimoto: generic agent harness beats custom chat boxes"
  type: case
  example_kind: reported_case
  evidence_status: source-reported
  source_chapter: "Part 1. Harness"
  source_quote: |
    "Even Mitchell Hashimoto, the guy behind Terraform and Ghostty, says a
    generic agent harness beats every custom chat box he's tried:"
  summary: |
    作者引用 Mitchell Hashimoto（Terraform / Ghostty 作者）的说法：通用 agent harness
    胜过他试过的所有定制聊天框，用以支撑"harness 才是关键层"的论点。
  bound_to:
    - "harness = environment，通用 harness 优于定制 chat UI"
  outcome: |
    未说明。文章未给出原话出处、链接、对比条件或结果；引号后直接接"6 Parts"图。
  caveat: "Source-reported appeal to authority; no link, no quote source, no detail or outcome."
  tags: [case, harness, mitchell-hashimoto, name-drop, source-reported]

- id: c03
  title: "Karpathy's list: agents, subagents, prompts, contexts, memory, ..."
  type: case
  example_kind: reported_case
  evidence_status: source-reported
  source_chapter: "Why This Suddenly Matters"
  source_quote: |
    "At the end of last year Karpathy posted the most honest description of
    where we all are: ... Read his list again: agents, subagents, prompts,
    contexts, memory, modes, permissions, tools, plugins, skills, hooks, MCP.
    That isn't one thing. It's three layers mashed into a single sentence."
  summary: |
    作者借 Karpathy 列举的一串概念（agents/subagents/prompts/contexts/memory/modes/
    permissions/tools/plugins/skills/hooks/MCP）说明：这些看似一个东西，实则是三层被
    压进一句话；拆开后"AI agent 不可靠"变成普通工程问题。
  bound_to:
    - "三层分类法（harness/loop/graph）的动机"
    - "把 agent 不可靠从神秘问题化归为分层工程问题"
  outcome: |
    未说明。Karpathy 的原始视频/帖子未被转录（BOOK_OVERVIEW.md 说明），列表内容为文章
    转述，非独立核验；tweet.json 是另一条宣传性 pointer（70 分钟录屏），同样无逐字稿。
  caveat: "Second-hand; video not transcribed; the enumerated list is quoted by the article, not verified from source."
  tags: [case, karpathy, taxonomy, source-reported, second-hand]

- id: c04
  title: "Claude Code shipped the loop as a command"
  type: case
  example_kind: reported_case
  evidence_status: source-reported
  source_chapter: "Part 2. Loop"
  source_quote: |
    "It went mainstream fast. Claude Code even shipped it as a command:"
    ... "Look at tip number five from the guy who built Claude Code.
    That's loop engineering in one sentence:"
  summary: |
    作者称 loop 已主流化，Claude Code 甚至把它做成一个命令，并以"造 Claude Code 的人的
    第五条建议"作为 loop engineering 的一句话注解，用来给 loop 层背书。
  bound_to:
    - "loop 工程化已被主流工具采纳（evidence-based stop 的实践佐证）"
  outcome: |
    未说明。文章没有给出该命令名、第五条建议的具体内容、链接或演示——两处均后接图片/空段。
  caveat: "Source-reported; the command and 'tip number five' content are absent from the acquired text (image-only)."
  tags: [case, loop, claude-code, name-drop, source-reported]

- id: c05
  title: "Peter Steinberger's 3.1M-view question"
  type: case
  example_kind: reported_case
  evidence_status: source-reported
  source_chapter: "Part 3. Graph"
  source_quote: |
    "In July one short question from Peter Steinberger got 3.1M views: ...
    The timeline answered within hours:"
  summary: |
    作者以 Peter Steinberger 七月的一个短问题获得 310 万浏览、时间线数小时内给出解答一事，
    引出 graph 层（多节点的协调）话题。
  bound_to:
    - "graph / 协调层的引入与关注度佐证"
  outcome: |
    部分陈述：文章称"3.1M views"及"时间线数小时内回答"，但问题原文与回答内容均为图片，
    未在正文给出；无法核验其与我方方法论的因果关系。
  caveat: "Source-reported; question text and answers are image-only, absent from acquired text."
  tags: [case, graph, peter-steinberger, name-drop, source-reported]

- id: c06
  title: "Login redirect loop #482 — the contract"
  type: case
  example_kind: worked_example
  evidence_status: demonstrated-in-text
  source_chapter: "Part 1. Harness > The 6 Parts of a Real Harness > 1. Contract"
  source_quote: |
    "goal:        fix login redirect loop (#482)
    inputs:      issue, repo, logs
    output:      reviewable pull request
    constraints: no schema changes, touch only auth/
    done_when:   new test reproduces the bug
                 same test passes after the fix
                 full suite is green"
  summary: |
    具体的任务契约示例：把"修 bug"转成带终点线的结构，最关键字段是 done_when；没有它
    agent 会悄悄改成一个更容易的版本然后宣称完成。贯穿后文（PROGRESS.md、feedback、graph
    的 billing/admin 检查）作为同一个示例任务的锚。
  bound_to:
    - "contract：先把请求变成带完成条件的契约"
    - "done_when 必须可被测试拒绝，不能是自报告"
  outcome: |
    worked_example，无真实结果；文章未说明该 PR 是否真的修好（"未说明"）。
  tags: [case, harness, contract, worked-example, done_when]

- id: c07
  title: "AGENTS.md as a map, not a manual"
  type: case
  example_kind: worked_example
  evidence_status: demonstrated-in-text
  source_chapter: "Part 1. Harness > The 6 Parts of a Real Harness > 2. Map"
  source_quote: |
    "AGENTS.md
    -> architecture   docs/architecture.md
    -> tests          docs/testing.md
    -> security       docs/security.md
    -> commands       docs/commands.md"
  summary: |
    根文件示例：不把所有文档塞进上下文，而是给一个短索引，按需加载细节。论点：
    "context isn't storage, it's an attention budget"，map 节省注意力，巨型 manual 耗尽它。
  bound_to:
    - "map 而非 manual：节省注意力预算"
  outcome: |
    worked_example，无真实结果（"未说明"）。
  tags: [case, harness, map, agents-md, worked-example]

- id: c08
  title: "PROGRESS.md — decisions live in files, not chat"
  type: case
  example_kind: worked_example
  evidence_status: demonstrated-in-text
  source_chapter: "Part 1. Harness > The 6 Parts of a Real Harness > 4. Memory"
  source_quote: |
    "PROGRESS.md
    goal    fix #482 login redirect loop
    tried   reorder auth middleware -> still red
    known   only happens with expired session cookie
    next    inspect auth/refresh.py
    never   touch migrations/"
  summary: |
    持久记忆文件示例：记录 goal/tried/known/next/never，使 agent 在崩溃、上下文重置或
    交接后继承真实工作状态，而不是模糊的对话摘要。与 c06 的 #482 是同一示例任务。
  bound_to:
    - "memory：上下文是 RAM，harness 是磁盘；决策/死路/未决风险写入文件"
    - "让 agent 跨会话存活（dead ends -> never list）"
  outcome: |
    worked_example，无真实结果（"未说明"）。
  tags: [case, harness, memory, progress-md, worked-example]

- id: c09
  title: "Feedback example — test_expired_session_redirect (EXPECTED vs SAW)"
  type: case
  example_kind: worked_example
  evidence_status: demonstrated-in-text
  source_chapter: "Part 2. Loop > Feedback, Not Verdicts"
  source_quote: |
    "FAILED      test_expired_session_redirect
    EXPECTED    302 -> /login
    SAW         302 -> /dashboard  (auth/refresh.py:61)
    FENCE       auth/refresh.py only
    DEAD ENDS   middleware reorder"
  summary: |
    把"红灯"变成方向的具体反馈消息：说明期望、实际、定位、围栏与已试过的死路。
    论点：DEAD ENDS 让第三次尝试不会悄悄退回第一次。与 c08 的 expired session cookie
    线索一致。
  bound_to:
    - "feedback as direction, not verdict（EXPECTED vs SAW + fence + dead ends）"
  outcome: |
    worked_example，无真实结果（"未说明"）；未给出该测试是否随后通过。
  tags: [case, loop, feedback, worked-example, expected-vs-saw]

- id: c10
  title: "Python retry loop with same-result-twice exit"
  type: case
  example_kind: worked_example
  evidence_status: demonstrated-in-text
  source_chapter: "Part 2. Loop > Exits"
  source_quote: |
    "for attempt in range(3):
        artifact = build(state)
        evidence = verify(artifact)          # tests, not vibes
        if evidence.passed:
            return artifact
        if evidence.saw in state.dead_ends:  # same result twice
            break
        state.dead_ends.append(evidence.saw)
        state.repair = evidence.gap
    return escalate_to_human(state)"
  summary: |
    伪代码/示例代码：带 goal、evidence、retry cap(=3) 与 exits 的真实循环。核心规则：
    同一结果出现两次说明 agent 停止从循环中学习，应 break 并升级给人类；
    "loop can fix the work, but it can't fix the question"。
  bound_to:
    - "exits：重试上限 + same-result-twice 升级，避免 cost leak"
    - "loop on evidence, not confidence"
  outcome: |
    worked_example（示意代码，非可运行产品代码）；无实际运行结果（"未说明"）。
  tags: [case, loop, exits, retry-cap, python, worked-example]

- id: c11
  title: "Symptom → layer triage table (Which Layer Is Broken?)"
  type: case
  example_kind: worked_example
  evidence_status: demonstrated-in-text
  source_chapter: "Which Layer Is Broken?"
  source_quote: |
    "SYMPTOM                                         FIX THE
     you copy-paste between chat and terminal        harness (tools)
     it retries things it already tried              harness (memory)
     'done' means nothing until you check            loop (the check)
     retries burn budget on the same error           loop (feedback + exits)
     every step is right, the whole thing is slow    graph (shape)
     one failure means everything reruns             graph (gates)
     the same mistake comes back every week          all layers (learning)"
  summary: |
    诊断表：把 7 个具体症状映射到应修的层。用法："find your first symptom from the top of
    this list. That's your next fix"。是分层排障方法的可执行实例集合。
  bound_to:
    - "symptom → owning layer 的诊断方法（先定位层，再动手）"
  outcome: |
    worked_example（启发式对照表，非实验结果）；作者未给出验证数据（"未说明"）。
  tags: [case, triage, symptom-layer, table, worked-example]

- id: c12
  title: "Failure → lesson ledger (Every Failure Should Upgrade the System)"
  type: case
  example_kind: worked_example
  evidence_status: demonstrated-in-text
  source_chapter: "Every Failure Should Upgrade the System"
  source_quote: |
    "FAILURE                               LESSON BECOMES               LAYER
     couldn't see production logs          read-only log tool           harness
     retried last week's dead approach     line in the 'never' list     harness
     touched a file it shouldn't           permission it no longer has  harness
     'fixed' with no reproducing test      required check in CI         loop
     same error 6 times in a row           same-result-twice exit       loop
     two audits overlapped                 split rule in scope node     graph
     typo and auth change got same review  undo-price gate             graph"
  summary: |
    失败归档台账实例：8 个具体失败各对应一条被写进某层的结构性教训（无 prompt 行）。
    论点："a split rule in the scheduler is structure"，prompt 只是希望，测试永远一致。
  bound_to:
    - "每次失败都升级系统，并把教训归档到拥有它的层"
    - "structure over hope（无 prompt 行）"
  outcome: |
    worked_example（示例台账，非实测统计）；无量化结果（"未说明"）。
  tags: [case, learning, failure-lesson, table, worked-example]

- id: c13
  title: "Build checklist (Harness / Loop / Graph)"
  type: case
  example_kind: worked_example
  evidence_status: demonstrated-in-text
  source_chapter: "The Checklist"
  source_quote: |
    "Harness: Success is defined before the run starts; root guide is a map, not a
    manual; every tool has a clear contract and failure state; decisions live in
    files; agent runs in a sandbox/worktree; every tool call is traced.
     Loop: Green is written before the code; the check fails at least once on
    purpose; feedback says expected vs saw; retry cap and token budget; same
    result twice means escalate.
     Graph: You tried to keep it a single loop first; every arrow passed the
    early-start test; each worker has its own context; passed nodes are frozen;
    gates priced by undo, not confidence."
  summary: |
    三层落地检查清单（各 5-6 项），把契约/map/工具契约/文件记忆/沙箱/追踪、green-first/
    故意失败/expected-vs-saw/上限/升级、单循环优先/早启动测试/独立上下文/冻结/gate 定价
    编成可勾选条目。结尾："If several are a no, a smarter model won't save you."
  bound_to:
    - "三层可执行检查表（诊断 + 验收）"
  outcome: |
    worked_example（检查清单，作者主张而非验证数据）（"未说明"）。
  tags: [case, checklist, harness, loop, graph, worked-example]

- id: c14
  title: "\"Write it twice\" — AGENTS.md guide + CI lint check"
  type: case
  example_kind: worked_example
  evidence_status: demonstrated-in-text
  source_chapter: "The \"Write It Twice\" Trick"
  source_quote: |
    "GUIDE  (AGENTS.md, the agent reads it)
    UI code may not query the database directly
    CHECK  (CI, the agent can't argue with it)
    lint fails if src/ui/** imports src/db/**"
  summary: |
    同一条规则写两遍的具体例子：一次写成 agent 能懂的指引（说明理由），一次写成它绕不过的
    CI 检查（即使模型忽视指引也成立）。论点：把过去的失误变成基础设施，harness 替它记住。
  bound_to:
    - "write every important rule twice：guidance + enforceable check"
  outcome: |
    worked_example，无真实事件或度量结果（"未说明"）。
  tags: [case, harness, write-it-twice, ci, worked-example]
```

## Coverage notes
- Checked every heading in `source-article.txt` (30-Second Version → If You Read This Far).
- Name-drops with NO link/detail in the acquired text: OpenAI/Codex (c01), Mitchell Hashimoto (c02), Karpathy list/video (c03), Claude Code command + "tip #5" (c04), Peter Steinberger question (c05); Anthropic "sells this whole layer as a product" (Part 1) is an unelaborated assertion, not extracted as a case.
- Image-only content (30-second diagram, 6 parts, loop anatomy, evidence ladder, Steinberger Q, trace image, checklist image) is not in the acquired text; only captioned/body text is cited.
- No case is a firsthand experience of the author; example_kind is reported_case (source-reported) or worked_example (article-printed). No outcome was inferred beyond what the text states.
