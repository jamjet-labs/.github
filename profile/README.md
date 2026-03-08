<div align="center">

<img src="https://jamjet.dev/logo-pixel.png" width="32" height="64" alt="JamJet" />

# JamJet

**The agent-native runtime for production AI.**

Durable execution &nbsp;·&nbsp; Native MCP + A2A &nbsp;·&nbsp; Rust core &nbsp;·&nbsp; Python SDK

[![PyPI](https://img.shields.io/pypi/v/jamjet?color=%23f5c518&labelColor=%230a0a0a&label=jamjet)](https://pypi.org/project/jamjet/)
[![License](https://img.shields.io/badge/license-Apache--2.0-%23f5c518?labelColor=%230a0a0a)](https://github.com/jamjet-labs/jamjet/blob/main/LICENSE)
[![Docs](https://img.shields.io/badge/docs-jamjet.dev-%23f5c518?labelColor=%230a0a0a)](https://jamjet.dev)

</div>

---

## What is JamJet?

JamJet is a **durable, graph-based workflow runtime** for AI agents. Crash at step 7 of 12 — resume from step 7. Every step transition is an event you can inspect, replay, and test against. The Rust core handles durability and performance. The Python SDK handles everything developers actually touch.

```python
from pydantic import BaseModel
from jamjet import Workflow

wf = Workflow("research-agent")

@wf.state
class State(BaseModel):
    query: str
    answer: str = ""

@wf.step
async def think(state: State) -> State:
    # your LLM call here — any model, any provider
    return state.model_copy(update={"answer": "..."})

# Local execution — no server needed
result = wf.run_sync(State(query="What is JamJet?"))

# Production — durable, crash-safe
# jamjet dev && jamjet run workflow.yaml --input '{"query": "..."}'
```

---

## The stack

| Protocol | What it means |
|---|---|
| **MCP native** | Connect any MCP server in one line — Brave Search, GitHub, Postgres, your own |
| **A2A native** | Agents call other agents across machines and orgs via the open A2A standard |
| **Rust runtime** | ~1ms framework overhead. Durable by default. No Python GIL contention at scale |
| **Eval harness** | 4 scorer types, JSONL datasets, CI exit codes — test your agents like software |

---

## Repositories

<table>
<tr>
<td width="50%">

### 🦀 [jamjet](https://github.com/jamjet-labs/jamjet)
Rust runtime core + Python SDK. The main project — workflow IR, durable executor, MCP client, A2A server, eval harness, and CLI.

</td>
<td width="50%">

### 📦 [examples](https://github.com/jamjet-labs/examples)
8 production-ready workflows: hello-agent, research-agent, code-reviewer, orchestrator, approval-workflow, support-bot, data-pipeline, sql-agent.

</td>
</tr>
<tr>
<td width="50%">

### 📊 [jamjet-benchmarks](https://github.com/jamjet-labs/jamjet-benchmarks)
Head-to-head benchmarks vs LangGraph, migration guides from LangGraph / CrewAI / raw OpenAI SDK, and a full feature matrix.

</td>
<td width="50%">

### 🌐 [jamjet.dev](https://github.com/jamjet-labs/jamjet.dev)
Documentation, blog, benchmarks page, and migration guides — built with Astro + Starlight.

</td>
</tr>
</table>

---

## By the numbers

| | |
|---|---|
| **~1ms** | Framework overhead vs raw LLM call (benchmarked · [see results](https://jamjet.dev/benchmarks)) |
| **4** | Built-in eval scorer types — assertion, latency, cost, LLM-as-judge |
| **4** | Project templates — `jamjet init --template <name>` |
| **8** | Ready-to-run workflow examples |
| **Apache 2.0** | License — use it, fork it, build on it |

---

## Get started

```bash
pip install jamjet
jamjet init my-agent --template hello-agent
cd my-agent && jamjet dev
```

**→ [Full quickstart](https://jamjet.dev/quickstart) · [Examples](https://github.com/jamjet-labs/examples) · [Benchmarks](https://jamjet.dev/benchmarks)**
