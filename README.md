# PM Copilot

**Turn a one-line idea into a product decision — in under 3 minutes.**

> Most AI PM tools generate documents. PM Copilot generates decisions.

[![Open Source](https://img.shields.io/badge/open%20source-MIT-teal.svg)](LICENSE)
[![Stack](https://img.shields.io/badge/stack-LangGraph%20%2B%20Claude-purple.svg)](https://langgraph.com)
[![Python](https://img.shields.io/badge/python-3.11%2B-blue.svg)](https://python.org)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](COOKBOOK.md)

---

<!-- SCREENSHOT: Add a demo GIF here showing the full pipeline run (idea → verdict) -->
<!-- Recommended: 800x600px, ~30 seconds showing all 3 stages completing -->
<!-- Tools: CleanShot X, Kap, or LICEcap -->

---

## Who this is for

**You're a solo founder, indie hacker, or early-stage builder.** You have an idea. You have a weekend. You don't have a product team, a PM, or $300/month for enterprise tooling.

You need one thing before you write a single line of code: *should I actually build this?*

PM Copilot answers that question honestly — including telling you no.

---

## The problem with every other tool

Every AI PRD generator, Notion AI template, and "PM copilot" on Product Hunt shares the same flaw: **they assume you already know what to build.**

You give them an idea. They give you a beautiful PRD. It looks great. It's completely useless — because the document was never the bottleneck. **The thinking was.**

PM Copilot flips the model:
- The PRD is the **last** thing it produces, not the first
- It stress-tests your idea before doing anything else
- It checks real market data — not hallucinated competitors
- It tells you the truth, even if the truth is *don't build this*

---

## How it works

```
Your idea (one sentence)
        ↓
Question generator — 3 tailored stress-test questions
        ↓
Your answers (you fill them in)
        ↓
┌─────────────────────────────┐
│  Stage 1: Stress Test       │  → Conviction score 1–10 + verdict
│  Stage 2: Market Pulse      │  → Signal: wide open / crowded / gap
│  Stage 3: Build Sequence    │  → Week 1, Month 1, Quarter 1 plan
└─────────────────────────────┘
        ↓
Your decision — download as markdown
```

<!-- SCREENSHOT: Add the workflow diagram image here -->
<!-- Export the workflow diagram from the project's /docs folder -->

---

## What you get

### Stage 1 — Stress Test
Three questions generated specifically for your idea (not generic ones). You answer them. PM Copilot evaluates your answers and returns:

- **Conviction score** — 1 to 10
- **Verdict** — `Build it` / `Pivot the angle` / `Don't build this`
- **Strengths** — what your answers reveal as genuine signal
- **Risks** — the gaps and blind spots in your thinking
- **Reasoning** — a paragraph explaining the score so you actually trust it

### Stage 2 — Market Pulse
Tavily searches the real web — not a hallucinated list of competitors. Returns:

- **Signal** — `Wide open` / `Crowded` / `Interesting gap`
- **The gap** — the specific angle your idea could own
- **3 competitors** — what they do and what they're missing
- **Recommendation** — an opinionated 2–3 sentence positioning take

<!-- SCREENSHOT: Add a screenshot of the Market Pulse output here (the signal badge + competitor cards) -->
<!-- This is the most shareable output — make it look good -->

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
# Edit .env: add ANTHROPIC_API_KEY and TAVILY_API_KEY

# 4. Run
streamlit run app.py
```

Open `http://localhost:8501` and enter your idea.

**Or with Docker:**

```bash
docker build -t pm-copilot .
docker run -p 8501:8501 --env-file .env pm-copilot
```

---

## API keys needed

| Key | Where to get it | Free tier? |
|---|---|---|
| `ANTHROPIC_API_KEY` | [console.anthropic.com](https://console.anthropic.com) | $5 free credit |
| `TAVILY_API_KEY` | [tavily.com](https://tavily.com) | 1,000 free searches/month |

---

## Tech stack

```
LangGraph 1.1.8      — agent orchestration
Claude Sonnet 4.6    — all LLM calls
Tavily               — Market Pulse web search
Streamlit            — UI
Python 3.11+
Docker               — one-command local run
```

> **Note on models (April 2026):** Uses `claude-sonnet-4-6`. The old `claude-sonnet-4-20250514` string is deprecated and retiring June 2026 — don't use it.

---

## Project structure

```
pm-copilot/
├── app.py                    # Streamlit entry point
├── graph/
│   ├── state.py              # State schema — the contract between nodes
│   ├── graph.py              # Graph wiring — declarative, no logic
│   └── nodes/
│       ├── stress_test.py    # Stage 1
│       ├── market_pulse.py   # Stage 2
│       └── build_sequence.py # Stage 3
├── prompts/                  # All prompts — community-editable
├── utils/
│   ├── llm.py                # Single call_llm() — swap model here
│   ├── search.py             # Tavily wrapper
│   └── export.py             # Markdown export
├── docs/
│   ├── PM_Copilot_PRD_v1.docx
│   └── PM_Copilot_ESOD_v1.docx
├── AGENTS.md                 # Context for AI coding agents
├── COOKBOOK.md               # How to extend PM Copilot
└── Dockerfile
```

---

## Extending PM Copilot

The architecture is designed for contribution. **Adding a new node takes 4 steps and touches 4 files.**

See [COOKBOOK.md](COOKBOOK.md) for the full guide, including:
- How to add a new analysis stage
- How to swap Claude for another LLM
- How to improve prompts without touching code
- How to add a new output section to the UI

Non-engineers can contribute by editing files in `prompts/` — no Python required.

---

## Roadmap

- [x] Stage 1: Stress test
- [x] Stage 2: Market pulse
- [x] Stage 3: Build sequence
- [ ] Stage 4: User persona (with trigger event + current workaround)
- [ ] Stage 5: Problem hierarchy + assumptions list
- [ ] Stage 6: Full PRD generation
- [ ] Next.js frontend (browser-based, no local install)
- [ ] Challenge mode: adversarial agent argues against your build plan

---

## Contributing

1. Fork the repo
2. Read [COOKBOOK.md](COOKBOOK.md) — especially "How to add a node"
3. Make your change
4. Open a PR with a before/after example of output quality

The most valuable contributions right now are **prompt improvements** in the `prompts/` directory. If you run a real idea through PM Copilot and the verdict feels wrong, open an issue with the idea + expected verdict. That's the feedback loop that makes this tool sharper.

---

## Why open source?

PM Copilot is free and local because the people who need it most — solo founders at 11pm before a pitch, indie hackers on a weekend build — shouldn't need a SaaS subscription to think clearly.

The product thinking should be accessible. The code should be forkable. The prompts should be improveable by the community.

---

## Built by

**KC** — PM II at Nielsen managing $31M ARR across three AI product lines. Previously co-founded TinTrin (10K downloads, 2K DAU in 12 days, zero ad spend). Built this because it's the tool I needed when I was building from scratch.

[LinkedIn](https://linkedin.com/in/krishnachaitanya) · [Portfolio](https://chaitanyaa.lol) · [Substack](https://substack.com/@chaiaurcharcha)

---

## License

MIT — use it, fork it, ship it.
