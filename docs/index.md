---
title: Home
---

# Agent Character Design — Field Guide

*A discipline for designing AI agent personalities, behavior arcs, and interaction rhythms that stay coherent over time.*

## The Three Levels

| Level | Mechanism | What it buys you |
|---|---|---|
| **1 — Input shaping** | System prompts | Initial character — drifts under long conversations |
| **2 — Loop shaping** | Context re-injection, behavioral memory, drift detection | Stable character across thousands of turns |
| **3 — Prior shaping** | Fine-tuning, RLHF | Baked-in disposition — expensive, rare |

Most AI persona work stops at Level 1. This Field Guide is about Level 2.

## Read the Field Guide

- [Chapter 1 — What Is Agent Character Design?](chapter-01-what-is-acd.html) (15 min)
- [Chapter 2 — Persona Architecture](chapter-02-persona-architecture.html) (20 min)
- Chapter 3 — Behavior Arcs *(in progress)*
- Chapter 4 — Interaction Rhythms *(planned)*
- Chapter 5 — Case Study: Colive *(planned)*
- Chapter 6 — Measurement & Drift Detection *(planned)*

## Tools

- **[acd-persona-generator-mcp](https://github.com/agent-character-design/acd-persona-generator-mcp)** — MCP server. Generate Level 2 persona specs. Assess existing prompts. Upgrade Level 1 → Level 2.

## Source

This is a living spec. Full repo: [github.com/agent-character-design/agent-character-design](https://github.com/agent-character-design/agent-character-design)

Contribute, disagree, fork: [CONTRIBUTING.md](https://github.com/agent-character-design/agent-character-design/blob/main/CONTRIBUTING.md)

## License

Content: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) · Code: MIT
