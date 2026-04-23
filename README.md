# Agent Character Design

> A discipline for designing AI agent personalities, behavior arcs, and interaction rhythms that stay coherent over time.

**ACD** sits between prompt engineering and RLHF: the design craft for *who* an AI agent is, not just *what* it knows.

## The Three Levels

Most "AI persona" work today stops at Level 1 — a well-written system prompt. That's fragile. ACD articulates three levels:

| Level | Mechanism | What it buys you |
|---|---|---|
| **1 — Input shaping** | System prompts, personality descriptions | Initial character — drifts under long conversations |
| **2 — Loop shaping** | Context re-injection, behavioral memory, drift detection, re-grounding schedules | Stable character across thousands of turns |
| **3 — Prior shaping** | Fine-tuning, RLHF | Baked-in disposition — expensive, rare, not always needed |

Everyone ships at Level 1. Claude Code, Cursor, and the best production agent systems actually run at **Level 2**. The goal of this Field Guide is to make Level 2 design explicit, teachable, and reproducible.

## The Field Guide

This repo hosts the living spec — a practical guide to designing AI agents whose character survives real use.

| Chapter | Status | Reading time |
|---|---|---|
| [Ch. 1 — What Is Agent Character Design?](docs/chapter-01-what-is-acd.md) | ✅ Draft v0.1 | 15 min |
| [Ch. 2 — Persona Architecture](docs/chapter-02-persona-architecture.md) | ✅ Draft v0.1 | 20 min |
| Ch. 3 — Behavior Arcs | 🚧 In progress | — |
| Ch. 4 — Interaction Rhythms | 📋 Planned | — |
| Ch. 5 — Case Study: Colive | 📋 Planned | — |
| Ch. 6 — Measurement & Drift Detection | 📋 Planned | — |

Hosted docs site: https://agent-character-design.github.io/agent-character-design/ (coming soon)

## Tools

The methodology ships with working tools, not just prose:

| Tool | What it does | Status |
|---|---|---|
| [`acd-persona-generator-mcp`](https://github.com/agent-character-design/acd-persona-generator-mcp) | MCP server: assess agent level, generate Level 2 persona specs, upgrade existing personas | ✅ v0.1 released |
| `acd-behavioral-audit-mcp` | MCP server: audit an existing agent's character stability score | 🚧 In design |
| `acd-score` | Web widget: paste a system prompt → get an ACD score + upgrade suggestions | 📋 Planned |
| `acd-lint` | CLI: `acd lint agent-config.json` → pass/fail for CI/CD pipelines | 📋 Planned |

## Why this exists

In 2026:
- 40% of enterprise apps ship AI agents (Gartner)
- 88% of agent projects fail to reach production (Fortune)
- "Agent reliability lagging" named the #1 blocker for agent adoption
- Harrison Chase (LangChain) identifies "context engineering" as the dominant failure mode

Context engineering is about what the agent *knows*.
**Agent Character Design is about who the agent *is*.**

Both matter. One has a name and a growing body of knowledge. The other needs one.

This repo is an attempt to give it one.

## The Research That Backs This

ACD is not a guess — it rests on three independently developed research threads that converge on the same conclusion:

1. **Anthropic's Persona Selection Model (PSM)** — LLMs are actors selecting characters from an internal repertoire. Character stability = selecting the same character consistently. Emotional conversations accelerate drift 7.3×. Level 2 activation capping reduces drift 60%.
2. **Disposition engineering** (philosophy of mind) — behaviors aren't *states*, they're *dispositions*: tendencies-to-behave-in-certain-ways-under-certain-conditions. Same disposition, different context = different manifestation. Requires multi-track profiles, not trait labels.
3. **Colive operational experience** — a live multi-agent system running 11 goal streams for 6+ months. Every pattern in this Field Guide is one we've used or failed at.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

This is a new discipline. Early contributors shape it.

- Found a counter-example that breaks a claim? Open an issue.
- Have a Level 2 pattern from your own system? PR a case study.
- Disagree with a framing? Fork and propose.

## License

Content: [CC BY 4.0](LICENSE) — use it, cite it, build on it.
Code samples: MIT.

## Author

Built by [Zico Zhou](https://github.com/ZicoZhou10). Background: psychology, game design, and operating autonomous multi-agent systems in production.

Contact: zhouzico@gmail.com · Twitter: [@AgentCharacter](https://twitter.com/AgentCharacter) (coming soon) · Site: [agentcharacterdesign.com](https://agentcharacterdesign.com) (coming soon)

---

*If this resonates, star the repo. That's the L3 signal that tells us whether to keep investing.*
