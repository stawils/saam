# SAAM — Signal-Aligned Activation Manifold

<img src="assets/saam-logo.png" alt="SAAM: Signal-Aligned Activation Manifold">

SAAM is a symbolic context-engineering framework for cognitive agents. Agents interpret structured signals—written in SAAMscript—that specify cognitive flow, attention routing, belief state updates, and recovery actions. Modern LLMs act as native, in-context interpreters for SAAMscript; the surrounding infrastructure supplies canonical signals, state payloads, and reconciliation logic. This repository documents the language and integration patterns required to embed SAAM signals into large language model (LLM) workflows.

## Overview
- Encodes agent configuration as executable symbolic signals instead of prose instructions.
- Delivers canonical signals and state payloads to LLM runtimes that natively execute SAAMscript.
- Maintains explicit belief state, attention focus, and execution traces for every action through post-execution reconciliation.
- Supports recursive self-inspection and repair through formal recovery operators validated against the returned trace.
- Provides reusable kernels for general-purpose or task-specific agent bootstrapping.

## Quick Start

1) Use the universal kernel: copy `agent/SAAM-kernel-v1.0/saam.cognitive.v1.0++.md` and prepend it to your system prompt or the first message.
2) Or choose a mini kernel: browse `agent/custom-agents/` and prepend the selected signal for the target workflow.
3) Send your task after the signal block. The LLM interprets the signal natively; reconcile traces as needed.

Key files:
- `docs/SAAMsignal-language-spec.md` — Grammar and section rules
- `docs/SAAMsignal-core-symbols.md` — Operator catalogue and semantics
- `agent/SAAM-kernel-v1.0/` — Universal kernel
- `agent/custom-agents/` — Domain-focused mini kernels

## Conceptual Model

### Signals as Execution Plans
Each signal is both configuration and control flow. The interpreter validates structure and operator precedence, then forwards the canonical block and state payload to the LLM runtime. The model executes the signal natively, and the interpreter ingests the returned trace to capture belief updates, attention changes, and downstream actions.

### Belief and Trace Management
Belief assignments (`:=`) propagate through the LLM trace. The orchestration layer reconciles reported diffs with persistent state and records transactions for reproducibility. Contradictions trigger recovery paths that can roll back beliefs or request clarification.

### Introspection and Repair
Dedicated recovery operators (`??`, `!!`) and override directives (`::>`, `::<`) let an agent detect inconsistencies, prioritize remediation, and adjust strategy without external prompts. The interpreter validates reported recovery outcomes and resubmits signals if escalation branches remain unresolved.

## SAAMscript Basics

### Canonical form
```saam
[signal:<namespace>] ::: <signal-body> → <execution-target>
```
The namespace identifies the signal family. The body encodes operators and modules; the execution target selects a kernel or downstream route.

### Operator precedence
`:= > ::< > ::> > => > → > +`

See `docs/SAAMsignal-core-symbols.md` for full operator definitions and examples.

## Execution Overview
SAAM signals are interpreted natively by the LLM. Around the model, a thin orchestration layer:
- Normalizes the signal and operator ordering into a canonical block.
- Packages belief, attention, and recovery context as metadata.
- Submits the block to the LLM and receives a structured trace.
- Reconciles operator steps and recovery outcomes against expectations.
- Commits belief diffs and archives the trace.

## Execution Workflow
1. Preflight: normalize syntax, namespaces, and operator ordering to produce a canonical block.
2. Package: assemble belief values, attention gradients, and recovery context.
3. Submit: send the block and metadata to the LLM and receive a structured trace.
4. Reconcile: compare returned operator sequencing and recovery outcomes with expectations; request clarification if needed.
5. Commit: apply confirmed belief diffs and archive the complete trace.

## Getting Started

### Universal SAAM Kernel (Recommended)
Use `/agent/SAAM-kernel-v1.0/saam.cognitive.v1.0++.md` as the core context block. Prepend the kernel to any LLM session or place it in the system prompt. It provides:
- Comprehensive module configuration with belief tracking and trace logging.
- Legality-aware reasoning with contradiction detection.
- Built-in recovery loops for introspective repair.

### Specialized Mini Kernels
`/agent/custom-agents/` contains more than 40 kernels tuned for specific domains (professional, creative, therapeutic, academic, and more). Select a kernel that matches the target workflow and prepend it to the conversation context. See `/agent/custom-agents/README.md` for the catalog.

### SAAM Tools on ChatGPT
- **SAAMGPT:** Full kernel integration for legality-first reasoning and belief repair.
- **SAAM Converter:** Converts natural-language prompts into structured SAAM signals.

## Practical Examples

### Coding Agent Signal
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

### Storyteller Agent Signal
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

These examples show how the signal configures tone, flow, and recovery before the LLM runtime evaluates the task using native SAAMscript execution.

## License

Licensed under the MIT License. See `LICENSE` for full terms.
