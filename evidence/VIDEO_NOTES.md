# Karpathy video — frame-grounded distillation (NOT a full transcript)

Source: 67-minute screen-share embedded in @0xoctocat's tweet,
mp4 `media.all[0].url` from `tweet.json` (37 MB, 480×270, 4027.7 s).

**Evidence status:** This is a *frame-sampled* reading, not a word-for-word transcript.
24 frames were extracted at ~168 s intervals, assembled into two contact sheets, and
read by image analysis. On-screen text was transcribed where legible; illegible text is
marked. Audio transcription was attempted but is not yet available (the video-analysis
backend has no video endpoint; on-device Swift Speech compilation is still running).
Do not treat quoted fragments below as a complete or exact transcript.

## Observed on-screen evidence (timestamps approximate)

| ~time | What is visible | Legible on-screen text / action |
|---|---|---|
| 0:00 | ChatGPT conversation | "Write a 600 word blog post about why I…" — long-form drafting request |
| 2:48 | Table headed "Overview of content in my life" | Work / Personal columns, current tools and tasks; prompt setting up a personal system ("You are the CEO of a…") |
| 5:36 | Chat with agent-style actions | "When I click a… I want you to actually…" — asking the assistant to perform actions, not just answer |
| 8:24 | Card UI titled "Adam Smith's Framework" | "What is Adam Smith's Utility?" with buttons **Ignore / Reject / Accept / Accept all** — per-item human approval |
| 11:12 | Numbered assistant output | Structure of an implementation answer (numbered steps, "Constitutional AI" visible) |
| 14:00 | Hand-drawn mind map | Central node with branches — concept mapping on screen |
| 16:48 / 19:36 | Terminal with code + a 3×3 grid | Grid labelled "Next player: X" — building a tic-tac-toe game by prompting |
| 22:24 / 28:00 / 36:24 / 47:36 / 64:24 | Recurring hand-drawn LLM diagram (shown repeatedly) | "Large Language Models (LLMs): … probabilistic … parameters store knowledge of the internet through the use of massive datasets"; **Tools**: Web Browsing (ChatGPT), Python (Code Interpreter / Advanced Data Analysis), DALL·E (image generation); **context window** with User / file uploaded / copy-paste; **Modalities**: Audio input (Conversations, Whispers, etc.), Image input (DALL·E, Computer Vision), Video input |
| 25:12 | Fresh ChatGPT screen | "What can I help with?" with suggestion chips (create image, summarise text, write, code) |
| 30:48 | Personalised greeting | "Good morning, Andj Karpathy. It's Monday, November 3." with chips including **Deep Research** and reading suggestions — a daily-briefing pattern |
| 33:36 | NotebookLM | Source "Evo 2: A Foundation Model for Genomic Sequence Analysis"; Studio tools: **Audio Overview, Video Overview, Mind Map, Report, Flashcards, Quiz** |
| 39:12 | "Supplementary Facts" table | "Requirement: Facts provided by the user's question" — fact extraction from a source |
| 42:00 | Structured prompt, numbered | "You are an educational content creator… 1. Read the attached article carefully… 2. Identify 5–10 key facts…" and "Structure of Final Response: 1. Engaging Hook … 4. Key Takeaways" |
| 44:48 | Generated image | Colourful cartoon character — image generation / style transfer |
| 50:24 | "Custom GPT" configuration modal | Fields: Name, Description, Instructions, Conversation starters |
| 53:12 / 56:00 | Long answer with **HIDE REASONING** toggle | Reasoning-model trace over a comparison table ("BBC, Discovery etc.") |
| 58:48 | Personal document prompt | "You are the executor of my estate. In the event of my death…" with numbered personal/financial instructions |
| 61:36 | Tic-tac-toe prompt | "You are an expert at the game of Tic Tac Toe… represent the board as a 3×3 grid…" with "Next player: X" |

## Distilled method (source-grounded)

1. **Mental model first.** An LLM is a probabilistic text generator whose knowledge comes
   from pretraining; what you can actually *do* with it comes from the context window
   plus tools (web, Python/code interpreter, image generation) and input modalities
   (audio, image, video). Most practical gains come from arranging context and tools,
   not from model lore.
2. **Build an explicit personal system.** Map the domains of your life (work/personal),
   the tools you use and the tasks you repeat, then hand that map to the model and have
   it propose a system. Treat the assistant as an operator with a remit, not a chatbot.
3. **Prefer actions over answers.** Prompts repeatedly ask the assistant to *do*
   something — draft, fetch, generate, run code — and to present the result as an
   artefact the user can accept or reject.
4. **Human approval as a UI pattern.** Framework cards come with Ignore / Reject /
   Accept / Accept all. Keep a per-item decision point instead of accepting a generated
   plan wholesale.
5. **Structured prompts with an output contract.** The educational-content prompt gives
   a role, numbered steps ("read the article", "identify 5–10 key facts") and a fixed
   final structure (hook → body → key takeaways). Specify the shape of the answer.
6. **Ground research in sources.** NotebookLM with an attached paper produces audio and
   video overviews, a mind map, a report, flashcards and a quiz. Fact-extraction prompts
   separate "facts provided by the question" from added knowledge.
7. **Package repeated workflows.** Custom GPT configuration (name, description,
   instructions, conversation starters) turns a prompt pattern into a reusable entry.
8. **Make the daily loop concrete.** A morning briefing with the actual date and
   suggested tasks (deep research, reading) is a trigger → context → action pattern.
9. **Show the work when it matters.** Reasoning models expose a trace with a HIDE
   REASONING control; use visible reasoning for judgement calls, hidden for presentation.
10. **Artefacts over prose.** Coding a tic-tac-toe game and generating an image are
    demonstrations of the same rule: define the state (3×3 grid, next player), then let
    the model operate on it.

## Anti-patterns (from the observed contrast)

- Treating the model as an all-knowing oracle instead of a probabilistic generator with
  a bounded context and extendable tools.
- Asking for information when an artefact (file, game, image, structured brief) is the
  real deliverable.
- Accepting a generated framework wholesale when per-item accept/reject is available.
- Unstructured "write something about X" requests when an explicit output contract is
  possible.
- Re-deriving context each session instead of packaging a custom GPT or a personal map.

## Confidence and gaps

- Frame sampling can miss short demonstrations; timestamps are approximate (±168 s).
- Many text fragments are partially legible at 480×270; exact wording is not guaranteed.
- No spoken narration was transcribed. The tweet's caption claims "the way the top 1%
  actually work" — that is promotional framing, not an evidenced claim.
- Claims about Karpathy's identity/role come from the tweet, not independently verified.
