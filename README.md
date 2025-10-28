# SAAM — Signal-Aligned Activation Manifold

<img src="assets/saam-logo.png" alt="SAAM: Signal-Aligned Activation Manifold">

SAAM is a simple way to guide AI systems using short, structured signals (SAAMscript). These signals set goals, steps, focus, and safety checks. Modern LLMs can read and follow these signals directly. Optional helper tools can check the signal’s structure and keep a clean record of what changed.

## Overview
- Uses structured signals instead of long instructions.
- Works with LLMs that execute SAAMscript directly.
- Tracks beliefs, focus, and a step-by-step trace for each run.
- Supports self-checks and error handling through built-in recovery operators.
- Offers a universal kernel and many mini kernels for common tasks.

## Quick Start

1) Use the universal kernel: copy `agent/SAAM-kernel-v1.0/saam.cognitive.v1.0++.md` and prepend it to your system prompt or the first message.
2) Or choose a mini kernel: browse `agent/custom-agents/` and prepend the selected signal for the target workflow.
3) Send your task after the signal block. The LLM interprets the signal natively; reconcile traces as needed.

Key files:
- `docs/SAAMsignal-language-spec.md` — Grammar and section rules
- `docs/SAAMsignal-core-symbols.md` — Operator catalogue and semantics
- `agent/SAAM-kernel-v1.0/` — Universal kernel
- `agent/custom-agents/` — Domain-focused mini kernels

## Core Ideas

### Signals as Execution Plans
Each signal is both configuration and control flow. You can optionally check a signal’s structure and order before sending it. The model runs the signal and returns a trace you can read to update beliefs, focus, and actions.

### Belief and Trace Management
Belief assignments (`:=`) appear in the model’s trace. Record those updates and keep a history. If results conflict, use a recovery step or ask for clarification.

### Introspection and Repair
Recovery operators (`??`, `!!`) and override directives (`::>`, `::<`) help detect inconsistencies and choose what to do next. If a recovery step did not finish, send a follow‑up signal.

## SAAMscript Basics

### Signal format
```saam
[signal:<namespace>] ::: <signal-body> → <execution-target>
```
The namespace identifies the signal family. The body encodes operators and modules; the execution target selects a kernel or downstream route.

### Operator order
Operators run in this order: `:= > ::< > ::> > => > → > +`

See `docs/SAAMsignal-core-symbols.md` for all operators and examples.

## How It Works
SAAM signals are interpreted by the LLM. Around that, you can use simple helper steps:
- Check the signal’s structure and order (optional).
- Add current facts (beliefs), focus settings, and any recovery context (optional).
- Send the signal and your task to the model.
- Read the trace and update beliefs or follow‑ups as needed.
- Save the trace for review.

## Execution Workflow
1. Check structure (optional).
2. Add context (optional).
3. Send the signal.
4. Read the trace.
5. Update and save.

## Getting Started

### Universal SAAM Kernel (Recommended)
Use `/agent/SAAM-kernel-v1.0/saam.cognitive.v1.0++.md` as the core context block. Add it at the top of your prompt or system message. It provides:
- A ready-to-use configuration with belief tracking and trace logging.
- Safety and policy checks; contradiction detection.
- Built-in recovery steps for error handling.

### Specialized Mini Kernels
`/agent/custom-agents/` contains more than 40 kernels tuned for specific domains (professional, creative, therapeutic, academic, and more). Select a kernel that matches the target workflow and prepend it to the conversation context. See `/agent/custom-agents/README.md` for the catalog.

### SAAM Tools on ChatGPT
- [SAAMGPT](https://chatgpt.com/g/g-6806ba323f24819180a2a11ba4067384-saamgpt): Full kernel integration for legality-first reasoning and belief repair.
- [SAAM Converter](https://chatgpt.com/g/g-67ec188b7b8081919387b2c28c9f1dec-saam-converter): Converts natural-language prompts into structured SAAM signals.
- [SAAM Text2Img Generator](https://chatgpt.com/g/g-681f7688e6cc8191a54b7373809624b5-saam-text2img-generator): A symbolic image generation agent that interprets structured prompts using SAAM signal language. It aligns mood, scene, and composition with symbolic consistency and traceable intent routing.

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
