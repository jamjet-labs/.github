<div align="center">

<img src="https://jamjet.dev/favicon.svg" width="64" height="64" alt="JamJet" />

# JamJet

### Agents that don't lose control.

**The safety layer behind your AI agents**: policy, audit, approval, recovery, cost, and memory. Open source. Apache 2.0.

[![PyPI](https://img.shields.io/pypi/v/jamjet?color=%23f5c518&labelColor=%230a0a0a&label=jamjet)](https://pypi.org/project/jamjet/)
[![Maven Central](https://img.shields.io/maven-central/v/dev.jamjet/jamjet-spring-boot-starter?color=%23f5c518&labelColor=%230a0a0a&label=maven)](https://central.sonatype.com/artifact/dev.jamjet/jamjet-spring-boot-starter)
[![Docker](https://img.shields.io/docker/pulls/jamjetdev/jamjet?color=%23f5c518&labelColor=%230a0a0a&label=docker)](https://hub.docker.com/r/jamjetdev/jamjet)
[![License](https://img.shields.io/badge/license-Apache--2.0-%23f5c518?labelColor=%230a0a0a)](https://github.com/jamjet-labs/jamjet/blob/main/LICENSE)
[![Discord](https://img.shields.io/badge/discord-join-%23f5c518?labelColor=%230a0a0a)](https://discord.gg/SAYnEj86fr)

[**jamjet.dev**](https://jamjet.dev) · [**docs**](https://docs.jamjet.dev) · [**compare**](https://jamjet.dev/compare) · [**showcase**](https://jamjet.dev/showcase) · [**blog**](https://jamjet.dev/blog)

</div>

---

## Not another agent framework

Keep your stack. Slot JamJet under it.

```
┌──────────────────────────────────────────────────────────┐
│  your agent framework                                    │
│  LangGraph · CrewAI · ADK · OpenAI Agents · Spring AI    │
└──────────────────────────────────────────────────────────┘
                            │
┌──────────────────────────────────────────────────────────┐
│  JamJet safety layer                                     │
│  policy · audit · approval · recovery · cost · memory    │
└──────────────────────────────────────────────────────────┘
                            │
┌──────────────────────────────────────────────────────────┐
│  models · tools · MCP · A2A                              │
│  Claude · OpenAI · Gemini · Postgres · your APIs         │
└──────────────────────────────────────────────────────────┘
```

The runtime sits between your agent and everything it touches. Every interaction passes through a layer that can block, wait, replay, and record. You don't have to leave LangGraph or CrewAI or whatever's already working. JamJet wraps what's there.

---

## Six failure modes. Six gates.

| # | Failure mode | What JamJet does |
|---|---|---|
| **01** | **Lost progress**: a worker dies mid-run | Replays the event log, resumes at the failed node |
| **02** | **Unsafe tool**: an agent reaches for a tool it shouldn't | 4-level policy hierarchy blocks the call before execution |
| **03** | **Skipped approval**: a high-risk action with no human gate | Run pauses, survives restarts, decision lands in audit |
| **04** | **Runaway cost**: a reflection loop that won't stop | Halts before crossing the cap |
| **05** | **Missing audit**: compliance asks what happened | Signed, exportable evidence package per run |
| **06** | **Forgotten context**: agent loses memory across sessions | Engram surfaces durable facts, not raw chat history |

---

## The repos

### Core runtime
- **[jamjet](https://github.com/jamjet-labs/jamjet)**: Rust runtime core + Python SDK. Workflow IR, durable executor, MCP client, A2A server, eval harness, CLI.

### JVM
- **[jamjet-runtime-java](https://github.com/jamjet-labs/jamjet-runtime-java)**: Pure-Java agent runtime. Durable execution, crash recovery, MCP native. No sidecar.
- **[jamjet-spring](https://github.com/jamjet-labs/jamjet-spring)**: Spring Boot starter. Drop into a Spring AI app and get crash recovery, audit, replay testing, and HITL gates.
- **[java-ai-memory](https://github.com/jamjet-labs/java-ai-memory)**: Neutral comparison of agent memory libraries for the JVM.

### Memory
- **[engram-mcp-server](https://github.com/jamjet-labs/engram-mcp-server)**: Durable memory MCP server. Temporal knowledge graph, hybrid retrieval, SQLite or PostgreSQL. Ships with the SDK; runs standalone.

### Protocols
- **[jamjet-a2a](https://github.com/jamjet-labs/jamjet-a2a)**: Standalone Rust SDK for the A2A v1.0 protocol. Client, server, coordinator, MCP bridge.

### Resources
- **[jamjet.dev](https://github.com/jamjet-labs/jamjet.dev)**: Website, blog, benchmarks, comparisons.
- **[jamjet-docs](https://github.com/jamjet-labs/jamjet-docs)**: Documentation at docs.jamjet.dev.
- **[jamjet-examples](https://github.com/jamjet-labs/jamjet-examples)**: Ready-to-run workflow examples.
- **[jamjet-benchmarks](https://github.com/jamjet-labs/jamjet-benchmarks)**: Head-to-head benchmarks vs LangGraph, migration guides, feature matrix.

---

## Recently shipped

- **Apr 25**: [Java runtime v0.1.1](https://jamjet.dev/blog/zero-sidecar-durable-agents-java/). Durable execution embedded directly in your JVM. `@DurableAgent` crash recovery, MCP native, 8.9× faster than the REST sidecar in our benchmark.
- **Apr 8**: [Engram Spring Boot Starter on Maven Central](https://central.sonatype.com/artifact/dev.jamjet/engram-spring-boot-starter). One dependency, inject `EngramClient`, done.
- **Apr 7**: [Engram v0.3.1](https://jamjet.dev/blog/engram-agent-memory/). Fact extraction, conflict detection, hybrid retrieval, consolidation. Published as `jamjet-engram` on crates.io and bundled with `dev.jamjet:jamjet-sdk`.
- **Mar 29**: [JamJet Spring Boot Starter on Maven Central](https://jamjet.dev/blog/jamjet-spring-boot-starter/). Crash recovery, audit, replay testing, and HITL gates for any Spring AI app.

---

## Get started

**Python**

```bash
pip install jamjet
jamjet init my-agent --template hello-agent
cd my-agent && jamjet dev
```

**Java / Spring**

```xml
<dependency>
  <groupId>dev.jamjet</groupId>
  <artifactId>jamjet-spring-boot-starter</artifactId>
</dependency>
```

[**→ Quickstart (60s)**](https://docs.jamjet.dev/en/docs/quickstart) · [**Compare frameworks**](https://jamjet.dev/compare) · [**Why JamJet**](https://jamjet.dev/why-jamjet)

---

<div align="center">
<sub>Open source · Apache 2.0 · <a href="https://jamjet.dev">jamjet.dev</a> · <a href="https://discord.gg/SAYnEj86fr">Discord</a> · <a href="https://twitter.com/jamjetdev">@jamjetdev</a></sub>
</div>
