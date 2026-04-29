# PM Copilot — Agent Context

## What this project is
LangGraph + Claude Sonnet 4.6 + Tavily + Streamlit.
Three-stage pipeline: Stress Test → Market Pulse → Build Sequence.
Open-source AI agent that turns a product idea into product decisions.

## Stack (April 2026)
- langgraph>=1.1.8
- DO NOT use langgraph.prebuilt — deprecated, use langchain.agents
- Model: claude-sonnet-4-6
- Python 3.11+
- Tavily for web search
- Streamlit for UI

## Architecture rules
- Every node = one file, one function
- Zero prompts in node files — all prompts live in prompts/
- All LLM calls through utils/llm.py :: call_llm() only
- graph/state.py is the contract — never bypass it
- graph/graph.py is declarative — no logic, just edges

## Full spec
- PRD: docs/PM_Copilot_PRD_v1.docx
- ESOD: docs/PM_Copilot_ESOD_v1.docx

## Current task
[Update this each session]# PM Copilot — Agent Context

## What this project is
LangGraph + Claude Sonnet 4.6 + Tavily + Streamlit.
Three-stage pipeline: Stress Test → Market Pulse → Build Sequence.
Open-source AI agent that turns a product idea into product decisions.

## Stack (April 2026)
- langgraph>=1.1.8
- DO NOT use langgraph.prebuilt — deprecated, use langchain.agents
- Model: claude-sonnet-4-6 (NOT claude-sonnet-4-20250514 — retiring June 2026)
- Python 3.11+
- Tavily for web search
- Streamlit for UI

## Architecture rules
- Every node = one file, one function
- Zero prompts in node files — all prompts live in prompts/
- All LLM calls through utils/llm.py :: call_llm() only
- graph/state.py is the contract — never bypass it
- graph/graph.py is declarative — no logic, just edges

## Full spec
- PRD: docs/PM_Copilot_PRD_v1.docx
- ESOD: docs/PM_Copilot_ESOD_v1.docx

## Current task
[Update this each session]
