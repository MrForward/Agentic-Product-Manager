# Agentic Product Manager

**Turn a one-line idea into a product decision — in under 3 minutes.**

> Most AI PM tools generate documents. This one generates decisions.

[![Open Source](https://img.shields.io/badge/open%20source-MIT-teal.svg)](#license)
[![Stack](https://img.shields.io/badge/stack-LangGraph%20%2B%20any%20LLM-purple.svg)](https://langgraph.com)
[![Python](https://img.shields.io/badge/python-3.11%2B-blue.svg)](https://python.org)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

---

<!-- SCREENSHOT: Add a demo GIF here showing the full pipeline run (idea → verdict) -->
<!-- Recommended: 800x600px, ~30 seconds showing all 3 stages completing -->
<!-- Tools: CleanShot X, Kap, or LICEcap -->

---

## Who this is for

**You're a solo founder, indie hacker, or early-stage builder.** You have an idea. You have a weekend. You don't have a product team, a PM, or $300/month for enterprise tooling.

You need one thing before you write a single line of code: *should I actually build this?*

Agentic PM answers that question honestly — including telling you no.

---

## The problem with every other tool

Every AI PRD generator, Notion AI template, and "PM copilot" on Product Hunt shares the same flaw: **they assume you already know what to build.**

You give them an idea. They give you a beautiful PRD. It looks great. It's completely useless — because the document was never the bottleneck. **The thinking was.**

Agentic PM flips the model:
- It stress-tests your idea **before** doing anything else
- It checks real market data — not hallucinated competitors
- It tells you the truth, even if the truth is *don't build this*
- The PRD is the **last** thing it produces, not the first

---

## How it works

```
Your idea (one sentence)
        ↓
Question generator — 3 tailored stress-test questions
        ↓
Your answers (you fill them in)
        ↓
┌─────────────────────────────────┐
│  Stage 1: Stress Test           │  → Conviction score 1–10 + verdict
│  Stage 2: Market Pulse          │  → Signal: wide open / crowded / gap
│  Stage 3: Build Sequence        │  → Week 1, Month 1, Quarter 1 plan
└─────────────────────────────────┘
        ↓
Your decision — download as markdown
```

<!-- SCREENSHOT: Add the workflow diagram image here -->
<!-- Export workflow-diagram.png from docs/ once generated -->

---

### Stage 1 — Stress Test
Three questions generated specifically for your idea — not generic ones. You answer them, the agent evaluates and returns:

- **Conviction score** — 1 to 10
- **Verdict** — `Build it` / `Pivot the angle` / `Don't build this`
- **Strengths** — what your answers reveal as genuine signal
- **Risks** — the gaps and blind spots in your thinking
- **Reasoning** — a paragraph explaining the score so you actually trust it

### Stage 2 — Market Pulse
Searches the real web — not a hallucinated list of competitors. Returns:

- **Signal** — `Wide open` / `Crowded` / `Interesting gap`
- **The gap** — the specific angle your idea could own
- **3 competitors** — what they do and what they're missing
- **Recommendation** — an opinionated 2–3 sentence positioning take

<!-- SCREENSHOT: Add a screenshot of the Market Pulse output here -->
<!-- The signal badge + competitor gap is the most shareable section -->

### Stage 3 — Build Sequence
Not RICE scores in a table. An opinionated plan for a solo builder:

| Horizon | Goal | What to build | What to **ignore** |
|---|---|---|---|
| Week 1 | Prove core value | Single flow that works | Everything else |
| Month 1 | Usable by strangers | Minimum lovable product | Polish, scale, auth |
| Quarter 1 | Worth talking about | Shareable moment | Features no one asked for |

Plus: your **North Star metric** and the **first assumption to invalidate**.

---

## Quick start

```bash
# 1. Clone
git clone https://github.com/MrForward/Agentic-Product-Manager
cd Agentic-Product-Manager

# 2. Install dependencies
pip install -r requirements.txt

# 3. Add your API keys
cp .env.example .env
# Edit .env — add your LLM API key and TAVILY_API_KEY

# 4. Run
streamlit run app.py
```

Open `http://localhost:8501` and enter your idea.

**Or with Docker:**

```bash
docker build -t agentic-pm .
docker run -p 8501:8501 --env-file .env agentic-pm
```

---

## API keys needed

| Key | Purpose | Free tier? |
|---|---|---|
| Your LLM provider key | Powers all three analysis stages | Varies by provider |
| `TAVILY_API_KEY` | Web search for Market Pulse — [tavily.com](https://tavily.com) | 1,000 searches/month free |

**Default LLM:** Claude Sonnet 4.6 (`ANTHROPIC_API_KEY`). Swap to any other provider by editing `utils/llm.py` — one file, one function.

---

## Tech stack

```
LangGraph 1.1.8      — agent orchestration
Any LLM provider     — pluggable via utils/llm.py
Tavily               — Market Pulse web search
Streamlit            — UI
Python 3.11+
Docker               — one-command local run
```

> **LLM is swappable by design.** The entire LLM layer lives behind a single `call_llm()` function in `utils/llm.py`. Change one file to run on GPT, Gemini, Mistral, or any other provider. Nothing else in the codebase is provider-specific.

---

## Project structure

```
Agentic-Product-Manager/
├── app.py                    # Streamlit entry point
├── graph/
│   ├── state.py              # State schema — the contract between nodes
│   ├── graph.py              # Graph wiring — declarative, no logic
│   └── nodes/
│       ├── stress_test.py    # Stage 1
│       ├── market_pulse.py   # Stage 2
│       └── build_sequence.py # Stage 3
├── prompts/                  # All prompts — community-editable, no Python needed
├── utils/
│   ├── llm.py                # Single call_llm() — swap your LLM here
│   ├── search.py             # Tavily wrapper
│   └── export.py             # Markdown export
├── docs/
│   ├── PM_Copilot_PRD_v1.docx
│   └── PM_Copilot_ESOD_v1.docx
├── AGENTS.md                 # Context for AI coding agents (Codex, Claude Code, Cursor)
└── Dockerfile
```

---

## Extending this project

The architecture is built for contribution. **Adding a new analysis stage takes 4 steps and touches 4 files** — `state.py`, a new node file, a new prompt file, and two lines in `graph.py`. Nothing else changes.

A `COOKBOOK.md` is coming that will cover:
- How to add a new analysis stage
- How to swap to a different LLM provider
- How to improve prompts without touching code
- How to add a new output section to the UI

Non-engineers can contribute by editing files in `prompts/` — no Python required.

---

## Roadmap

- [ ] Stage 1: Stress test
- [ ] Stage 2: Market pulse
- [ ] Stage 3: Build sequence
- [ ] Stage 4: User persona (with trigger event + current workaround)
- [ ] Stage 5: Problem hierarchy + assumptions list
- [ ] Stage 6: Full PRD generation
- [ ] Next.js frontend (browser-based, no local install required)
- [ ] Challenge mode: adversarial agent argues against your build plan

---

## Contributing

1. Fork the repo
2. Make your change — prompt improvements in `prompts/` are the highest-value contribution right now
3. Open a PR with a before/after example of output quality

If you run a real idea through and the verdict feels wrong, open an issue with the idea and the expected verdict. That's the feedback loop that makes this tool sharper over time.

---

## Why open source?

The people who need this most — solo founders at 11pm before a pitch, indie hackers on a weekend build — shouldn't need a SaaS subscription to think clearly about what to build.

The code is forkable. The prompts are improveable. The architecture is designed so contributors can extend it without understanding the whole codebase.

---

## Built by

**KC** — PM at Nielsen managing ~$20M ARR across AI product lines. Previously co-founded TinTrin (10K downloads, 2K DAU in 12 days, zero ad spend). Built this because it's the tool I needed when I was building from scratch.

[GitHub](https://github.com/MrForward) · [LinkedIn](https://linkedin.com/in/chaitanya-athukuri/) · [Portfolio](https://chaitanyaa.lol)

---

## License

MIT — use it, fork it, ship it.
