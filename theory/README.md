# ACD Theoretical Foundations

The [ACD Field Guide](../docs/) deliberately stays at a practitioner level — three layers (Input / Loop / Prior shaping), concrete patterns, working tools. This directory is for readers who want to know *why* the layers are structured this way.

## The deeper claim

ACD's three-layer structure is not arbitrary. It reflects a structural theory of what robustness *is* in agent systems: **the depth of an attractor basin in the model's hidden-state landscape**. Each ACD layer corresponds to a distinct mechanism for shaping basin geometry.

| ACD layer | Mechanism | Theoretical correlate |
|---|---|---|
| **Input shaping** (system prompts) | Initial position in landscape | Where you place the agent |
| **Loop shaping** (context re-injection, memory, behavioral arcs) | Restoring force during inference | How the basin keeps the agent |
| **Prior shaping** (fine-tuning) | Basin topology itself | What the landscape looks like |

This connection is developed in the **AFEL (Agent Free Energy Landscape)** framework.

## Reading order

1. **[The Shape of Agent Robustness — Post 1](https://www.lesswrong.com/)** *(LessWrong, link pending)* — the readable introduction
2. **[AFEL Pre-Registration v1.0](https://osf.io/)** *(OSF, link pending)* — 26 falsifiable predictions with explicit invalidation criteria, timestamp-locked 2026-04-10
3. **[Disposition Engineering for Agents](#)** *(in development)* — how AFEL's basin structure maps onto Heil-style dispositional realism

## Status

This is **active research**, not settled science. The framework has:
- 26 numbered predictions
- 13 with retrospective evidence (cross-validated by 5 independent research groups)
- 0 falsified
- 1 partially falsified and revised (P23d → P23d*, dimension-dependent)

We are explicit about confidence: the framework is **falsifiable** and **worth testing**, not proven. ACD users do not need to accept AFEL to use ACD's three-layer structure productively — the practitioner layer stands on its own. AFEL is for those who want to know what's underneath.

## Why this lives in the ACD repo

ACD is the engineering practice; AFEL is its structural theory. The same author. Same intellectual lineage. Discoverable here because anyone serious enough to want the theory should not have to find it.

## Contact

For substantive theoretical correspondence: zico@agentcharacterdesign.com (subject prefix `[AFEL]`).
