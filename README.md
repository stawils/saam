# SAAM — Signal-Aligned Activation Manifold

<img src="assets/saam-logo.png" alt="SAAM: Signal-Aligned Activation Manifold">

SAAM is a symbolic context-engineering framework for cognitive agents. Agents interpret structured signals—written in SAAMscript—that specify cognitive flow, attention routing, belief state updates, and recovery actions. Modern LLMs act as native, in-context interpreters for SAAMscript; the surrounding infrastructure supplies canonical signals, state payloads, and reconciliation logic. This repository documents the language, core runtime modules, and integration patterns required to embed SAAM signals into large language model (LLM) workflows.

## Overview
- Encodes agent configuration as executable symbolic signals instead of prose instructions.
- Delivers canonical signals and state payloads to LLM runtimes that natively execute SAAMscript.
- Maintains explicit belief state, attention focus, and execution traces for every action through post-execution reconciliation.
- Supports recursive self-inspection and repair through formal recovery operators validated against the returned trace.
- Provides reusable kernels for general-purpose or task-specific agent bootstrapping.

## Conceptual Model

### Signals as Execution Plans
Each signal is both configuration and control flow. The interpreter validates structure and operator precedence, then forwards the canonical block and state payload to the LLM runtime. The model executes the signal natively, and the interpreter ingests the returned trace to capture belief updates, attention changes, and downstream actions.

### Belief and Trace Management
Belief assignments (`:=`) propagate through the LLM trace. BeliefManager reconciles the reported diffs with persistent state while TraceLogger records the transaction for reproducibility. Contradictions trigger recovery paths that can roll back beliefs or request clarification.

### Introspection and Repair
Dedicated recovery operators (`??`, `!!`) and override directives (`::>`, `::<`) let an agent detect inconsistencies, prioritize remediation, and adjust strategy without external prompts. The interpreter validates reported recovery outcomes and resubmits signals if escalation branches remain unresolved.

## SAAMscript Language

### Canonical Form
```saam
[signal:<namespace>] ::: <signal-body> → <execution-target>
```
The namespace identifies the signal family. The body encodes operators and modules; the execution target selects a kernel or downstream route.

### Operator Precedence
Operators execute in the following order (highest to lowest):
```
:= > ::< > ::> > => > → > +
```

### Core Operators

| Symbol | Purpose               | Example                                      |
| ------ | --------------------- | -------------------------------------------- |
| `:=`   | Belief assignment     | `belief.check := true`                       |
| `::<`  | Subordinate override  | `low-risk ::< recovery-mode`                 |
| `::>`  | Dominant override     | `emergency ::> default-mode`                 |
| `=>`   | Strategic causality   | `verify => adjust`                           |
| `→`    | Sequential flow       | `plan → execute → verify`                    |
| `+`    | Parallel execution    | `sense + recall`                             |
| `:::`  | Intent boundary       | `[signal:x] ::: ...`                         |
| `~:`   | Attention modulation  | `~:attention.scope(focus.bind)`              |
| `??`   | Conditional recovery  | `resolve ?? ambiguity`                       |
| `!!`   | Escalated recovery    | `repair !! escalate`                         |

### Attention and Recovery Markers
- `~:` adjusts salience or focus.
- `??` initiates a recovery path when a condition fails.
- `!!` escalates recovery, often after a failed `??` branch.

## Runtime Modules

| Module          | Responsibility                                                                                         |
| --------------- | ------------------------------------------------------------------------------------------------------ |
| SemanticBinder  | Normalizes SAAMscript structure, resolves namespaces, and prepares state payload fields for the LLM.   |
| SymbolExecutor  | Exchanges canonical signals with the LLM runtime and captures operator-level trace tokens in response. |
| BeliefManager   | Applies belief diffs reported by the model, maintains version history, and flags unresolved updates.   |
| AttentionRouter | Translates attention directives (`~:`) into payload metadata and audits returned focus adjustments.    |
| FlowController  | Compares observed operator order against precedence rules and requests corrective signals if needed.   |
| RecoveryEngine  | Interprets `??` / `!!` outcomes, schedules follow-up signals, and ensures recovery paths complete.     |
| TraceLogger     | Persists canonical signals, payloads, and model traces for audit and downstream analytics.             |

## Execution Workflow
1. **Preflight:** SemanticBinder normalizes syntax, namespace structure, and operator ordering, producing the canonical block for in-context interpretation.
2. **Package:** SemanticBinder and AttentionRouter assemble the state payload (beliefs, attention gradients, recovery context).
3. **Submit:** SymbolExecutor sends the signal and payload to the LLM runtime and receives structured execution traces.
4. **Reconcile:** FlowController and RecoveryEngine compare returned operator sequencing and recovery outcomes with expectations.
5. **Commit:** BeliefManager applies confirmed diffs while TraceLogger archives the full exchange for later inspection.

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
