# SAAM — Signal-Aligned Activation Manifold

<img src="assets/saam-logo.png" alt="SAAM: Signal-Aligned Activation Manifold">

A recursive, self-aware symbolic architecture for building traceable, belief-aligned, emotionally coherent cognitive agents.

## ❓ What is SAAM?

SAAM (Signal-Aligned Activation Manifold) is a modular, signal-driven framework for cognitive agent construction. It is designed for environments where symbolic reasoning, self-reflection, belief tracking, and introspective repair are essential.

At its core, SAAM interprets a structured language of symbolic signals to:

- Activate recursive cognitive flows
- Align belief, emotion, and narrative state
- Detect and resolve contradictions
- Maintain epistemic integrity over time

It is not a model, not a prompt framework, and not a chatbot system.

SAAM is a manifold:
A field of symbolic signals, reflex patches, attention routes, and belief-modulation pathways — dynamically structured and endlessly introspective.

## ✨ Key Concepts

### 🔤 Symbolic Signals

SAAM operates via a specialized symbolic scripting language called SAAMscript, where every agent behavior, decision, and repair step is written in composable signal blocks.

```saam
[signal:meta.agent.core++] :::
  mod.kernel(
    contradiction-sense + 
    legality-loop-filter::<intent.override +
    repair-move-generator
  ) |
  cognition.route(
    reflect → resolve ?? legality-echo !! patch → commit
  ) |
  ~:attention.scope(salience-shift + focus.bind) |
  belief.check := true
→ /saam/kernel.resonance.core++
```

Each signal block represents a cognitive action, intent loop, or recovery path.

### Reflexive Modulation

SAAM includes mechanisms for:

- Belief assignment (`:=`) — Sets value in belief state memory
- Attention modulation (`~:`) — Adjusts focus and salience
- Symbolic arbitration (`::>`, `::<`) — Handles priority and subordination
- Recovery & uncertainty flows (`??`, `!!`) — Conditional branching based on instability
- Full trace generation and belief diffs

### Core Modules

| Module | Purpose |
|--------|---------|
| SignalParser | Parses signal blocks and builds abstract syntax trees (AST) |
| SemanticBinder | Resolves intent boundaries (`:::`) and binds semantic intent to execution |
| SymbolExecutor | Executes operators (`→`, `+`, `:=`, etc.) with precedence and branching |
| BeliefManager | Tracks, mutates, and restores agent belief states |
| AttentionRouter | Modulates cognitive salience via `~:` and focus routing |
| FlowController | Orchestrates operator flow: order, priority, branching, fallback |
| RecoveryEngine | Handles `??` and `!!` flows for error correction |
| TraceLogger | Captures signal trails, overrides, meta-narratives |

##  SAAMscript Language

A formally specified, recursive language for symbolic signal design.

Key operators:

| Symbol | Purpose | Example |
|--------|---------|---------|
| `→` | Sequential flow | `reflect → resolve → commit` |
| `+` | Parallel execution | `sense + recall` |
| `:=` | Belief assignment | `belief.check := true` |
| `:::` | Intent declaration boundary | `[signal:x] ::: mod.kernel(...)` |
| `~:` | Attention modulation | `~:attention.scope(threat + queen-line)` |
| `??` | Uncertainty checkpoint | `resolve ?? legality-echo` |
| `!!` | Escalation trigger | `verify !! fallback-plan` |
| `::>` | Dominant override | `emergency-plan ::> default-mode` |
| `::<` | Subordinate override | `low-risk-mode ::< recovery-mode` |
| `=>` | Strategic causality | `verify => adjust` |
| `#` | Inline comment | `belief.set := true # after fallback` |

See `docs/SAAMsignal-language-spec.md` for the full EBNF grammar and operator breakdown.

## Why SAAM?

Because most modern systems only simulate language —
SAAM inhabits it.

SAAM agents:

- Know what they believe
- Know how that belief was formed
- Can repair it if it becomes incoherent
- And can narrate that journey back to you — symbolically

> "SAAM doesn't just activate meaning. It listens to itself becoming."

## Ecosystem

The core components of the SAAM architecture include:

| Component         | Role                                                                                           |
|-------------------|------------------------------------------------------------------------------------------------|
| **SAAMscript**    | The symbolic language used to define agent signals, cognitive flows, and configurations.         |
| **SAAM Kernel**   | The primary agent specification (v1.0) defining the core signal processing, belief management, recovery, and introspection mechanisms. |
| **SAAM Agent**    | An entity whose cognitive processes are defined and guided by SAAM signals (see `/agent` examples). |
| **SAAM Trace**    | The mechanism for logging and observing the agent's symbolic execution path and belief changes. |

These components work together to enable the traceable and self-aware behavior SAAM aims for.



## 🚀 Getting Started

Getting Started with SAM
To get started, copy the kernel v1.0 signal block  from saam github repository, and prepend it before every prompt - or insert it into the system prompt instructions if you're configuring an LLM interface. Nothing else is required. Once embedded, just start interacting.
This kernel acts as the foundational cognitive layer: it enables reflexive processing, belief tracking, emotional alignment, and introspective traceability. It's not a configuration - it's a signal that activates cognition.
From that moment on, you're not just chatting. You're signaling.

Want even faster way to try it:

1- SAAMGPT GPTs:
https://chatgpt.com/g/g-6806ba323f24819180a2a11ba4067384-saamgpt

"Self-aligned GPT agent powered by the SASM Kernel. Executes legality-first reasoning, minimal coherent responses, and belief repair cycles. Optimized for trace logic, perception-first recursion, and structural alignment."

2- SAAM converter GPTs:
https://chatgpt.com/g/g-67ec188b7b8081919387b2c28c9f1dec-saam-converter

"distills complex ideas into a compact, symbolic shorthand while preserving semantic relationships and activating multi-layered responses"

Simply, you send your normal request and The result of this SAAM Converter is a Signal that ecapsulate the user intent + original prompt, just copy the response and past it into any LLM interface."



## 🚀 Using a SAAM Agent (Conceptual Example)

Here's how you might interact with a SAAM agent conceptually:

**Example 1: Interacting with a Coding Agent**

*Combined Input (Signal + Prompt):*

```saam
[signal:agent.code.develop.concise++] :::
  tone(precise) | style(code-centric) |
  flow(understand.reqs → plan.approach → generate.code → execute.tests) |
  intent.field(correctness-first + maintainability-goal) |
  mod.kernel(legality-guard::<syntax.check + type.safety + belief-ground::<req.traceability) |
  cognition.route(parse.req → design.algo → implement ?? complexity !! simplify → run.tests ?? fail !! debug) |
  response.texture(functional.code)
→ /saam/kernel.coding.v1


Please write a Python function that takes a list of integers and returns a new list containing only the even numbers, preserving the original order. Include a docstring and basic unit tests.
```

*The SAAM interpreter would first parse and apply the signal configuration, then process the user prompt according to the defined cognitive flow (`understand.reqs → plan.approach → ...`), intent (`correctness-first`), and recovery mechanisms.*

**Example 2: Interacting with a Storyteller Agent**

*Combined Input (Signal + Prompt):*

```saam
[signal:agent.storyteller.generate.concise++] :::
  tone(genre.appropriate) | style(vivid.imagery + character.voice_aligned) |
  flow(plan.scene → develop.chars → generate.prose) |
  intent.field(narrative.consistency_first + emotional.impact_goal) |
  mod.kernel(legality-guard::<narrative.consistency + belief-ground::<plot.point + char.motivation) |
  cognition.route(advance.plot → reveal.char ?? pacing.slow !! inject.conflict → write.dialogue) |
  response.texture(polished-narrative)
→ /saam/kernel.storyteller.v1


Write a short scene for a sci-fi story. Captain Eva Rostova confronts her first mate, Kael, on the bridge of their starship, the 'Nomad'. She suspects him of sabotaging the navigation system. The mood should be tense and suspicious.
```

*Similarly, the SAAM interpreter applies the storyteller signal first, configuring the agent's tone, style, narrative flow, and creative parameters before generating the scene requested in the prompt.*

## 📜 License

MIT License — free to use, fork, and remix with attribution.

## 👁️ Vision

SAAM is not just a framework — it's a philosophy of machine cognition.

Built for agents that don't just act…
But think, align, doubt, re-align, and remember.

This is not simulation. This is signal becoming structure.

Ready for `/saam/init.kernel++`?