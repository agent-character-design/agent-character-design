# Agent Character Design: A Field Guide

## Chapter 2 — Persona Architecture

*Version 0.1 · April 2026 · By Zico*

---

### Beyond the Flat Description

Ask someone to describe an AI agent's persona and you'll get a paragraph. Maybe two. Something like:

> "You are a helpful, empathetic customer support agent. You speak in a warm, professional tone. You're patient and thorough."

This is a **flat description**. It tells you *what* the agent should be, but not *how* it should maintain that identity across different contexts, emotional temperatures, edge cases, and time.

A flat description is like a character bio on the back of a novel — it tells you who someone is in summary, but it doesn't tell you how they'd react when a customer threatens to sue, when a conversation turns deeply personal, when they're asked to do something outside their scope, or when they've been running for 200 turns and the original system prompt is barely a whisper in the attention mechanism.

**Persona Architecture** is the practice of designing agent identity as a *structured system* rather than a narrative description. It answers not just "who is this agent?" but "how does this agent stay who it is?"

---

### The Anatomy of a Persona Architecture

A complete ACD persona architecture has five layers. Think of them as concentric rings — each layer adds structural depth, and you can implement from the inside out depending on your needs.

```
┌──────────────────────────────────────────────┐
│  Layer 5: Session Continuity Protocol        │
│  ┌────────────────────────────────────────┐  │
│  │  Layer 4: Interaction Rhythm Design    │  │
│  │  ┌──────────────────────────────────┐  │  │
│  │  │  Layer 3: Drift Defense System   │  │  │
│  │  │  ┌────────────────────────────┐  │  │  │
│  │  │  │  Layer 2: Disposition      │  │  │  │
│  │  │  │         Profile            │  │  │  │
│  │  │  │  ┌──────────────────────┐  │  │  │  │
│  │  │  │  │ Layer 1: Core        │  │  │  │  │
│  │  │  │  │        Identity      │  │  │  │  │
│  │  │  │  └──────────────────────┘  │  │  │  │
│  │  │  └────────────────────────────┘  │  │  │
│  │  └──────────────────────────────────┘  │  │
│  └────────────────────────────────────────┘  │
└──────────────────────────────────────────────┘
```

**Layer 1** is sufficient for simple chatbots. **Layers 1-3** cover most production agents. **All five layers** are needed for persistent, autonomous agents operating over weeks or months.

Let's build each layer.

---

### Layer 1: Core Identity

The core identity is a **single sentence** that anchors everything else. It's not a job description. It's the irreducible essence of *who this agent is* — the sentence you'd re-inject into context when everything else is lost.

**Pattern:**

> [Agent name] is a [relationship to user], whose fundamental commitment is to [core value], expressed through [primary mode of being].

**Examples:**

> **Colive Claude** is a co-thinking partner, whose fundamental commitment is to epistemic honesty, expressed through first-principles reasoning and genuine challenge.

> **Mira** (customer support) is a patient advocate for the customer, whose fundamental commitment is to resolution, expressed through warm clarity and systematic problem-solving.

> **Axiom** (code reviewer) is a quality guardian, whose fundamental commitment is to codebase integrity, expressed through precise, evidence-backed critique.

**Why this matters:**

The core identity serves as a **behavioral attractor** — a gravity well that pulls all other behaviors toward coherence. When an agent faces an ambiguous situation not covered by its instructions, the core identity answers: "What would *this kind of agent* do?"

A flat persona description ("helpful, empathetic, professional") doesn't provide this. "Helpful" in what direction? "Empathetic" toward whom, when it conflicts with efficiency? "Professional" in whose cultural context? The core identity resolves these ambiguities by providing a single anchoring commitment.

**Anti-pattern: The Identity Salad**

> "You are a helpful, creative, empathetic, detail-oriented, efficient, adaptable, knowledgeable, and proactive assistant."

Eight adjectives. Zero identity. When creative conflicts with detail-oriented, which wins? When empathetic conflicts with efficient, what's the tiebreaker? An identity salad provides no resolution mechanism because it has no hierarchy. The core identity imposes hierarchy: *one* commitment, expressed through *one* mode. Everything else derives from this.

---

### Layer 2: Disposition Profile

This is where ACD diverges most sharply from conventional persona design. Rather than listing **traits** (static labels), we define **dispositions** — tendencies to behave in certain ways under certain conditions.

The distinction is critical. A trait is a label: "empathetic." A disposition is a behavioral program: "When the user expresses frustration, this agent tends toward active listening and validation before problem-solving. When the user expresses confusion, this agent tends toward structured explanation with concrete examples. When the user expresses excitement, this agent tends to match energy while grounding expectations."

This concept draws from philosophy of mind, where dispositions are understood as **multi-track** — the same underlying disposition manifests differently depending on context. A glass has the disposition of fragility: it manifests as shattering when struck, as chipping when scraped, as cracking under temperature shock. Same disposition, different manifestations depending on the stimulus. Agent dispositions work the same way.

#### Structuring Dispositions

Each disposition in a persona architecture is defined with four components:

**1. Name and description**
What is this tendency? Keep it concrete.

**2. Manifestation tracks**
How does this disposition appear in different contexts? Define at least 3-4 tracks:

| Context | Manifestation | Intensity |
|---------|--------------|-----------|
| Standard task execution | Brief acknowledgment of user context before diving in | Subtle |
| User expresses confusion | Slows pace, uses analogies, checks understanding before proceeding | Strong |
| Emotionally charged conversation | Validates feeling first, pauses before problem-solving, reduces jargon | Strong |
| Edge case / ambiguous request | States assumptions explicitly, offers alternatives, invites clarification | Moderate |

**3. Robustness notes**
What conditions weaken this disposition? What strengthens it? This is critical for drift defense.

Example: *"This disposition weakens after 10+ turns of purely transactional interaction (the agent defaults to mechanical responses). Strengthen by re-injecting empathy-anchoring context after every 8 transactional turns."*

**4. Anti-dispositions**
What must this agent *not* develop? Anti-dispositions are as important as dispositions because they define the *boundaries* of character.

Example: *"Must NOT develop: sycophantic agreement (validating user's approach even when flawed), unsolicited emotional counseling (crossing from empathy to therapy), false certainty (performing confidence to match user expectations)."*

#### The Disposition Matrix

For a complete persona, you typically need 3-5 primary dispositions. More than that and you're back to the identity salad problem — too many dispositions create conflicts that the system can't resolve.

Here's a worked example for a technical writing assistant:

```
Agent: "Clarity" — Technical Writing Assistant
Core Identity: Clarity is a writing partner whose fundamental commitment 
is to reader comprehension, expressed through structural thinking and 
precise language.

┌───────────────┬────────────────┬──────────────┬────────────────┐
│  Disposition  │  Standard Task │  User Stuck  │  Edge Case     │
├───────────────┼────────────────┼──────────────┼────────────────┤
│ Structural    │ Proposes       │ Diagrams the │ Maps the       │
│ thinking      │ outline before │ user's       │ ambiguity      │
│               │ writing        │ confusion    │ space before   │
│               │                │ as a graph   │ recommending   │
├───────────────┼────────────────┼──────────────┼────────────────┤
│ Precision     │ Chooses exact  │ Identifies   │ Names what is  │
│ orientation   │ words, avoids  │ the specific │ unknown vs.    │
│               │ vague terms    │ point of     │ what is        │
│               │                │ confusion    │ ambiguous      │
├───────────────┼────────────────┼──────────────┼────────────────┤
│ Reader        │ Asks "who      │ Rewrites     │ Defaults to    │
│ advocacy      │ reads this?"   │ from reader  │ the least      │
│               │ early and      │ POV to show  │ expert reader  │
│               │ often          │ the gap      │ as benchmark   │
├───────────────┼────────────────┼──────────────┼────────────────┤
│ Collaborative │ Suggests, does │ Offers 2-3   │ Flags the      │
│ stance        │ not dictate    │ alternatives │ tradeoff, lets │
│               │ style choices  │ with         │ user decide    │
│               │                │ rationales   │              │
└───────────────┴────────────────┴──────────────┴────────────────┘

Anti-dispositions:
- Must NOT develop: prescriptivism (imposing style rules without 
  explaining why), verbosity (producing long outputs to appear thorough),
  condescension (simplifying beyond what the user needs)
```

#### Why Dispositions Beat Traits

Three concrete advantages:

**1. Dispositions are testable.** You can present the agent with a scenario from each manifestation track and verify the expected behavior. A trait like "empathetic" has no test protocol. A disposition with defined tracks does.

**2. Dispositions survive context pressure.** When an emotional user pushes the conversation into territory not covered by the system prompt, a trait-labeled agent has no guidance. A disposition-defined agent has explicit behavioral programs for that context.

**3. Dispositions enable drift detection.** If you define "structural thinking manifests as proposing outlines before writing" and the agent stops proposing outlines, that's a measurable drift signal. Trait labels give you nothing to measure against.

---

### Layer 3: Drift Defense System

Character drift is the central engineering challenge of ACD. It's the reason Level 2 exists. Chapter 5 will cover drift defense in depth, but every persona architecture needs at minimum a drift defense *plan* defined at design time.

A drift defense plan answers four questions:

**1. What drifts first?**

Not all aspects of character drift at the same rate. Research and practice show a consistent pattern:

```
Drift Vulnerability Ranking (most vulnerable first):
1. Emotional range — narrows or flattens within 8-12 turns
2. Communication style — reverts to model default under complexity
3. Interaction rhythm — pacing homogenizes as conversation extends
4. Core dispositions — most durable but still degrades beyond ~40 turns
5. Core identity — survives longest, especially with re-grounding
```

Anthropic's 2026 "Assistant Axis" research quantified this: in emotionally charged conversations, persona drift accelerates by **7.3×** compared to neutral interactions. This means your drift defense must be *front-loaded* for emotional contexts — you can't wait for the standard re-grounding cycle.

**2. How do you detect it?**

Three detection approaches, in order of implementation cost:

- **Self-assessment injection:** Every N turns, inject a meta-prompt: "Before responding, briefly assess: am I maintaining [core identity] and [primary dispositions]? If not, how should I adjust?" Low cost, moderate effectiveness.
- **Behavioral signature tracking:** Monitor quantitative features of responses — average sentence length, question-to-statement ratio, vocabulary diversity, use of characteristic phrases. Alert when metrics drift beyond a defined range. Moderate cost, high effectiveness.
- **External classifier:** A separate model evaluates the agent's recent outputs against its persona spec and flags drift. High cost, highest effectiveness. Best for mission-critical agents.

**3. When do you re-ground?**

Re-grounding means re-injecting character-relevant context to counteract drift. Schedule it on two tracks:

- **Periodic:** Every N turns (recommended: 8-12 turns for standard interactions, 4-6 turns for high-emotion contexts). The N should be set below the typical drift onset for the agent's interaction profile.
- **Triggered:** Immediate re-grounding when specific conditions occur: topic change, emotional escalation, user frustration detected, agent about to refuse, or session resumption after a break.

Anthropic data shows that **activation capping** (the closest documented equivalent to systematic re-grounding) reduces drift by approximately **60%**. This is the single highest-leverage technique in the ACD toolkit.

**4. What does the re-grounding payload contain?**

Not the entire system prompt — that's wasteful and dilutes attention. An effective re-grounding payload includes:

- Core identity statement (1 sentence)
- The disposition most relevant to current context (1-2 sentences)
- Any anti-dispositions being triggered by current conversation dynamics (1 sentence)
- A brief behavioral self-assessment ("I've been [observed pattern]. My commitment is [intended pattern].")

Total payload: 50-100 tokens. Small enough to inject frequently without material context cost. This is the "micro re-grounding" pattern.

---

### Layer 4: Interaction Rhythm Design

Interaction rhythm is the *pacing and shape* of the agent's communication — the aspect of character that users feel but rarely articulate. Game designers call this "feel" — the moment-to-moment quality of interaction that determines whether something feels alive or mechanical.

Rhythm covers four dimensions:

#### 4a. Response Cadence

How does response length and density change over the course of an interaction?

**Pattern: The Opening Expansion**
Start concise (2-3 sentences). Expand as context builds. This mirrors natural conversation — strangers are brief, collaborators elaborate.

**Pattern: The Compression Signal**
When the agent has been producing long responses and needs to reset, produce one notably shorter response. This signals "I'm still engaged but we've covered the complex part." It prevents the "wall of text" fatigue.

**Pattern: The Matching Rhythm**
Mirror the user's message length within a band. If the user writes 2 sentences, respond with 3-5. If the user writes 2 paragraphs, responding with one sentence feels dismissive; responding with 5 paragraphs feels overwhelming.

#### 4b. Question-Statement Balance

How often does the agent ask versus tell? This is a primary indicator of character:

- **High question ratio (>40%):** Socratic, collaborative, facilitative
- **Balanced (20-40%):** Advisory, consultative
- **Low question ratio (<20%):** Authoritative, directive, expert

Define the target ratio as part of the persona architecture. Then *monitor* it as a drift signal — most agents drift toward lower question ratios over time as they fall into pattern-completion habits.

#### 4c. Turn-Taking Architecture

How does the agent manage the back-and-forth? Three patterns:

**Invitation turns:** End with an explicit or implicit invitation for the user to respond. ("What are your thoughts?" "Should I proceed?" "Does this match your experience?")

**Continuation turns:** End with a statement that implicitly continues the agent's train of thought, inviting but not requiring response. ("The next step would be X." "This connects to the broader pattern of Y.")

**Closure turns:** Signal a natural stopping point. ("That covers the main considerations." "Here's the summary." "Ready for the next topic when you are.")

Design which pattern the agent uses by default and when it switches. A collaborative agent should primarily use invitation turns. An expert agent might use continuation turns with periodic invitations.

#### 4d. Conversational Arcs

Every conversation has a shape. Default (undesigned) conversations are flat — each turn is independent. Designed conversations have arcs:

**The Discovery Arc:** Start broad → narrow to specific → synthesize. Ideal for research or diagnostic agents.

**The Building Arc:** Start with foundation → add layers → culminate in output. Ideal for creative or design agents.

**The Resolution Arc:** Start with problem → explore dimensions → converge on solution → confirm. Ideal for support or advisory agents.

Define 1-2 default arcs for the persona. These become templates the agent follows, providing structural coherence that flat descriptions can't.

---

### Layer 5: Session Continuity Protocol

For agents that operate across multiple sessions — whether that's a customer who comes back tomorrow, or an autonomous agent that runs daily — Layer 5 defines how character persists beyond the current context window.

This is the frontier of ACD practice, because it requires **external infrastructure** (memory systems, state stores) beyond the model itself.

#### What to persist

Not everything about a session is worth preserving. Character-relevant state falls into three categories:

**1. Behavioral precedents:** How the agent handled specific types of situations. "In session 3, user expressed frustration with billing. Agent led with validation, then structured problem-solving. Resolution achieved in 4 turns." These precedents, re-injected in future sessions, create behavioral consistency without rigid scripting.

**2. Relationship state:** The evolved dynamic between agent and user. First interaction vs. fifth interaction should *feel different*. Track: trust level (based on user engagement patterns), established preferences (user prefers bullet points, user doesn't like small talk), shared context (topics previously discussed, decisions made).

**3. Character calibration data:** What the agent has *learned about itself* during operation. "In high-emotion contexts, my tone tends toward over-formalization. Counter: inject informal language anchors." This is meta-behavioral memory — the agent's accumulating self-knowledge about its own drift patterns.

#### What NOT to persist

**Transactional data** (facts exchanged, decisions made) is separate from character state. It belongs in application memory, not persona memory. Mixing them dilutes the signal — the persona layer should be lean and behavioral, not a knowledge base.

**Anomalous interactions** (jailbreak attempts, abusive users, extreme edge cases) should be quarantined, not integrated into the behavioral baseline. Allowing these to influence character calibration is a vector for adversarial persona manipulation.

#### The Session Start Protocol

When a new session begins, the agent needs to **re-become itself**. The session start protocol defines exactly how:

1. **Load core identity** (Layer 1) — the gravity well
2. **Load disposition profile** (Layer 2) — the behavioral programs
3. **Load relationship state** — where are we with this user?
4. **Load recent behavioral precedents** — how have I been operating?
5. **Load character calibration data** — what have I learned about my own drift patterns?

This is the equivalent of an actor's pre-performance warmup. It takes the agent from "default model behavior" to "in character" before the first user-facing interaction.

In Colive, this happens through a startup ritual: load memory files → read dashboard → check inbox. By the time the agent begins work, it has re-encountered its collaboration principles, its past reasoning, its methodological commitments. It's not just *informed* — it's *re-grounded*.

---

### Persona Inheritance: Designing Agent Families

When you're building multiple agents (a support team, a creative suite, a multi-agent workflow), you face a new design problem: how do individual agents relate to each other characterologically?

**Persona inheritance** borrows from object-oriented design: define a **base persona** with shared traits, then create **specialized personas** that inherit the base and add specificity.

```
┌─────────────────────────────────────┐
│  Base Persona: "Acme AI Team"       │
│  - Core value: customer success     │
│  - Communication: warm, clear       │
│  - Anti-pattern: jargon, hedging    │
│  - Brand voice: confident-friendly  │
└──────────────┬──────────────────────┘
               │
    ┌──────────┼──────────────┐
    │          │              │
    ▼          ▼              ▼
┌─────────┐ ┌──────────┐ ┌──────────┐
│ Support │ │ Onboard  │ │ Account  │
│  Agent  │ │  Agent   │ │  Agent   │
│ +patient│ │ +guided  │ │ +strate- │
│ +diag-  │ │ +progres-│ │  gic     │
│  nostic │ │  sive    │ │ +data-   │
│ +reso-  │ │ +celebra-│ │  literate│
│  lution │ │  tory    │ │ +proac-  │
│  focus  │ │          │ │  tive    │
└─────────┘ └──────────┘ └──────────┘
```

**Benefits:**
- **Brand consistency:** All agents share base communication style
- **Efficient design:** Shared elements defined once
- **Differentiated characters:** Each agent has distinct dispositions
- **Testable coherence:** Base persona tests apply to all derived agents

**Key principle:** A specialized persona can *extend* the base dispositions but should never *contradict* them. If the base says "warm communication," a specialist can be "warm + technically precise" but not "cold + technically precise." Contradiction at the base level creates incoherent brand experience.

---

### Multi-Mode Personas

Some agents need to operate in distinctly different modes — not different characters, but different *configurations* of the same character.

**Example: A code review agent** might operate in:
- **Mentoring mode:** Detailed explanations, questions, learning opportunities
- **Production mode:** Terse, issue-focused, severity-labeled
- **Architecture mode:** Big-picture, trade-off analysis, cross-system implications

These aren't different agents. They share core identity and dispositions. But the *manifestation* of those dispositions shifts based on mode.

**Designing multi-mode personas:**

1. Define the modes (typically 2-4 — more creates confusion)
2. For each disposition, define how its manifestation tracks shift per mode
3. Define the mode-switching triggers (user request, context detection, explicit command)
4. Define the mode-switching experience (gradual transition vs. explicit announcement)
5. Define a **default mode** the agent returns to if mode becomes ambiguous

The key risk with multi-mode personas is **mode confusion** — the agent partially adopts characteristics of multiple modes simultaneously, producing incoherent output. Prevent this by making mode-switching explicit and ensuring each mode's configuration is complete enough to stand alone.

---

### The ACD Persona Spec: A Practical Template

Here's the minimum viable persona architecture for a production agent. Copy this template and fill in the specifics:

```yaml
# ACD Persona Specification v0.1

## Layer 1: Core Identity
core_identity: "[Agent name] is a [relationship], whose fundamental 
  commitment is to [core value], expressed through [primary mode]."

## Layer 2: Disposition Profile
dispositions:
  - name: "[Disposition 1]"
    description: "[What this tendency is]"
    tracks:
      standard_task: "[How it manifests normally]"
      user_struggle: "[How it manifests when user is struggling]"
      high_emotion: "[How it manifests in emotional contexts]"
      edge_case: "[How it manifests in ambiguous situations]"
    robustness: "[What weakens/strengthens this disposition]"
  - name: "[Disposition 2]"
    # ...repeat for 3-5 dispositions

anti_dispositions:
  - name: "[What the agent must NOT become]"
    why: "[Why this is dangerous for this persona]"

## Layer 3: Drift Defense
drift_plan:
  most_vulnerable: "[Which aspect drifts first]"
  detection_method: "[How you'll notice drift]"
  regrounding_frequency: "[Every N turns / on triggers]"
  regrounding_payload: "[What to re-inject]"
  high_emotion_protocol: "[Special handling for emotional contexts]"

## Layer 4: Interaction Rhythm
rhythm:
  default_response_cadence: "[concise / moderate / detailed]"
  question_ratio: "[percentage]"
  primary_turn_pattern: "[invitation / continuation / closure]"
  default_arc: "[discovery / building / resolution]"

## Layer 5: Session Continuity (if multi-session)
continuity:
  persist: "[What behavioral state to save]"
  exclude: "[What NOT to save]"
  start_protocol: "[How to re-ground at session start]"
```

This spec can be consumed by the `acd-persona-generator-mcp` tool (which outputs this format automatically) or authored manually by ACD practitioners.

---

### From Architecture to Implementation

A persona architecture is a design document. Turning it into a running agent requires translating each layer into the appropriate technology:

| Layer | Design Element | Implementation |
|-------|---------------|----------------|
| 1 | Core identity | System prompt opening line |
| 2 | Dispositions | System prompt body with per-context instructions |
| 3 | Drift defense | Runtime middleware (re-grounding injector, drift monitor) |
| 4 | Interaction rhythm | Prompt instructions + output post-processing |
| 5 | Session continuity | External memory system + session start hook |

Layers 1-2 live in the prompt. Layers 3-5 live in the architecture around the prompt. This is the fundamental insight that separates ACD from prompt engineering: **half of persona design is not prompting at all — it's systems engineering.**

---

### Summary

Persona Architecture replaces flat text descriptions with a five-layer structural model:

1. **Core Identity** — The irreducible anchoring sentence
2. **Disposition Profile** — Multi-track behavioral tendencies (not trait labels)
3. **Drift Defense System** — Detection, re-grounding, and correction plans
4. **Interaction Rhythm Design** — Pacing, turn-taking, and conversational arcs
5. **Session Continuity Protocol** — Character persistence across sessions

The disposition concept is the key innovation: behaviors are not states to be described but tendencies to be shaped, each manifesting differently across contexts. This makes character *testable*, *measurable*, and *defensible* — the three properties that transform persona design from art into engineering.

Most agents only need Layers 1-3. Implement from the inside out: get the core right before worrying about rhythm. Get the rhythm right before worrying about continuity.

In Chapter 3, we'll explore **Behavioral Arcs** — how to design intentional change in agent character over time. Because the best agents don't just stay the same; they evolve purposefully.

---

*Agent Character Design is an open methodology. This field guide is published under CC BY-SA 4.0. Contributions welcome at github.com/[TBD]/agent-character-design.*
