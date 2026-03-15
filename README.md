# SAAM — Signal-Aligned Activation Manifold

<div align="center">

![SAAM Logo](assets/saam-logo.png "SAAM: Signal-Aligned Activation Manifold")

**SAAM** (Signal-Aligned Activation Manifold) is a framework for guiding large language models using structured signals written in SAAMscript, a symbolic language designed to reduce output drift, improve calibration, and enforce honest self-reporting.

</div>

## Table of Contents
- [Overview](#overview)
- [How It Works](#how-it-works)
- [Empirical Findings](#empirical-findings)
- [Technical Architecture](#technical-architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Configuration](#configuration)
- [API Reference](#api-reference)
- [Examples](#examples)
- [Tools and Integrations](#tools-and-integrations)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

SAAM provides structured control over LLM behavior through symbolic signals that:
- Reduce output drift by constraining specific failure modes
- Improve stability without degrading content quality
- Enable belief tracking and reasoning trace generation
- Surface genuine uncertainty rather than papering over it
- Support error recovery mechanisms
- Offer domain-specific kernel implementations

### What Problem Does SAAM Solve?

Standard prompting produces inconsistent outputs and is vulnerable to predictable failure patterns: absorbing user framing, preferring beautiful answers over accurate ones, generating toward length rather than need, and smoothing over unknowns rather than surfacing them. SAAM addresses this by providing structured signals that constrain these specific failure modes rather than instructing the model to reason better.

The key distinction: SAAM signals **evoke a state** rather than **name a cognitive process**. Explicit reasoning instructions ("think step by step", "reason carefully") name a process and have been empirically shown to degrade output stability. State-evoking signals improve it. This is the core mechanism.

### Technologies Used

SAAM is implemented as plain text signals and requires no special software. It operates by providing structured SAAMscript signals that LLMs interpret during execution.

---

## How It Works

SAAMscript signals work at the token level — they shape the probability distribution over outputs by evoking a cognitive posture rather than instructing a cognitive process. The formal syntax creates a register distinct from plain language instructions, which appears to be part of the mechanism.

Key principles:
- **Constraint over description**: every signal section should either constrain output or force a self-report. Sections that do neither add noise.
- **State-evoking vocabulary**: words like `awareness`, `concentration`, `examine` outperform words like `reasoning`, `thinking`, `analysis` — the former evoke states, the latter name processes and invite over-correction.
- **Deviation watch as load-bearing**: the `deviation.watch` block with specific `!!` recovery paths is the most behaviorally effective section.
- **Minimal self-report**: the trace fields (`src`, `conf`, `drv`) are forcing functions for accountability, not truth claims about internal states. `belief.introspect := unreliable` should always be set.

---

## Empirical Findings

SAAM has been validated through independent benchmark testing across multiple models.

### Benchmark Results

- **Dataset**: 5000-variant benchmark across Mistral-small-3.1-24b and Flash2.0-lite
- **Accuracy improvement**: 10–15% above baseline on complex reasoning tasks
- **Stability improvement**: consistent reduction in output variance (measured as standard deviation across synonym variants)
- **Key control**: SAAM-lookalike syntax conditions failed to replicate the effect — confirming the result is not surface mimicry

### Key Findings

**saam_cognitive consistently outperforms baseline on stability**, while:
- Naive reasoning/thinking modifiers actively degrade performance below baseline
- SAAM-lookalike syntax without genuine form+content fails to replicate the effect
- The effect is model-agnostic (replicated across Mistral and Flash2.0)
- Ceiling effects appear on simple tasks — the signal's effect is most visible under difficulty or failure conditions

**Mechanistic interpretation**: SAAM functions as probability sculpting, not cognitive architecture programming. The formal signal shifts the distribution of outputs by evoking a stable cognitive posture. The module list and route algebra in the signal are conceptual maps that orient the model's register — they are not discrete computational modules that execute independently.

**Failure mode differentiation**: on unsolvable or broken problems, SAAM-active responses produce exhaustive error mapping and explicit uncertainty acknowledgment. Baseline produces quiet failure or confabulated resolution.

### What the Evidence Does and Does Not Support

The evidence supports: SAAM signals reliably shift output stability and reduce specific drift patterns across multiple models and tasks.

The evidence does not support: claims about "programming cognitive architecture," "geometric weight matrix control," or "activation manifold alignment" as literal mechanisms. These are useful metaphors for the human designing signals, not descriptions of what happens computationally.

---

## Technical Architecture

### Core Components
- **SAAMscript**: A symbolic language for defining cognitive constraints and recovery paths
- **Universal Kernel**: A constraint-first general-purpose kernel (`/agent/SAAM-kernel-v1.0/saam.cognitive.v1.0++.md`)
- **Domain-Specific Kernels**: Specialized implementations in `/agent/custom-agents/`
- **Signal Structure**: `[signal:<namespace>] ::: <body> → <target>`

### How SAAM Works
1. Signal is prepended to the prompt as system context
2. The LLM interprets the SAAMscript register and adjusts its output distribution accordingly
3. Deviation watch sections constrain specific failure modes during generation
4. Belief assignments set the posture for uncertainty and self-reporting
5. Trace fields force a minimal self-report at the end of each response
6. Recovery paths activate when instability or constraint violation is detected

---

## Installation

SAAM requires no installation as it operates through structured text prompts. To begin using SAAM:

1. Clone the repository:
   ```bash
   git clone https://github.com/tsuser/AI/saam.git
   ```

2. Navigate to the agent directory to access kernels:
   ```bash
   cd saam/agent/
   ```

3. Access the universal kernel at:
   ```
   /agent/SAAM-kernel-v1.0/saam.cognitive.v1.0++.md
   ```

4. Browse domain-specific kernels in:
   ```
   /agent/custom-agents/
   ```

---

## Usage

### Universal Kernel (Recommended)
1. Include the universal kernel (`/agent/SAAM-kernel-v1.0/saam.cognitive.v1.0++.md`) in your system prompt or first message
2. This provides deviation detection, belief tracking, uncertainty surfacing, and built-in recovery strategies
3. Append your task after the signal block

### Domain-Specific Kernels
1. Browse `/agent/custom-agents/` to select an appropriate kernel
2. Prepend the selected kernel to your conversation context
3. Add your task after the kernel specification

### Basic Signal Format
```saam
[signal:<namespace>] ::: <body> → <target>
```

Where:
- `<namespace>` identifies the signal family
- `<body>` contains operators, modules, and cognitive constraints
- `<target>` selects the kernel or route to use

### Operator Execution Order
```
:= > ::< > ::> > => > → > +
```

---

## Configuration

### Available Kernels
- **Universal Kernel**: `/agent/SAAM-kernel-v1.0/saam.cognitive.v1.0++.md` — Constraint-first general reasoning with deviation detection and honest self-reporting
- **Domain-Specific Kernels**: `/agent/custom-agents/` — Over 40 specialized implementations for various domains

### Signal Operators
- `:=` — Belief assignment/updates
- `::<` / `::>` — Module prioritization/overrides
- `??` — Uncertainty checkpoint
- `!!` — Escalation and recovery trigger
- `+` — Parallel activation

For complete operator reference, see:
- `docs/SAAMsignal-language-spec.md`
- `docs/SAAMsignal-core-symbols.md`

---

## API Reference

SAAM operates through structured text signals. No API calls are required beyond normal LLM interactions.

### Core Signal Sections
- `mod.kernel()` — Sets priority ordering and attention scope
- `deviation.watch()` — Defines failure modes with specific recovery paths
- `cognition.route()` — Specifies reasoning flow with uncertainty checkpoints
- `belief.*` assignments — Sets cognitive posture for uncertainty and self-reporting
- `meta.regulator()` — Per-paragraph drift and absorption checks
- `autonomy.trace()` — Origin-tagging with explicit handling of unknowns
- `trace.graph()` — Minimal self-report fields: src, conf, drv
- `safeguards.recovery()` — Standard escalation path

---

## Examples

### Basic Coding Task
```saam
[signal:agent.code.develop++] :::
  mod.kernel(correctness ::> elegance) |
  deviation.watch(
    confabulation !! hold → surface-gap
    length-over-need !! trim → last-genuine
  ) |
  cognition.route(
    absorb.requirements →
    design ?? ambiguity-flag !! clarify →
    implement →
    validate
  ) |
  belief.gap := visible
→ /saam/kernel.coding.v1

Write a Python function that filters even numbers from a list and returns them in the same order.
```

### Research Task
```saam
[signal:agent.research.analyze++] :::
  mod.kernel(truth ::> completeness) |
  deviation.watch(
    absorbed-as-generated !! strip → restate-raw
    confabulation !! hold → surface-gap
  ) |
  cognition.route(
    absorb.question →
    investigate ?? uncertainty-hold !! partial-commit →
    synthesize →
    trace.sources
  ) |
  belief.introspect := unreliable
→ /saam/kernel.research.v1

Summarize the current state of evidence on [topic].
```

---

## Tools and Integrations

### SAAM Tools on ChatGPT
- [SAAMGPT](https://chatgpt.com/g/g-6806ba323f24819180a2a11ba4067384-saamgpt): Full kernel integration for legality-first reasoning and belief repair.
- [SAAM Converter](https://chatgpt.com/g/g-67ec188b7b8081919387b2c28c9f1dec-saam-converter): Converts natural-language prompts into structured SAAM signals.
- [SAAM Text2Img Generator](https://chatgpt.com/g/g-681f7688e6cc8191a54b7373809624b5-saam-text2img-generator): A symbolic image generation agent that interprets structured prompts using SAAM signal language.

---

## License

MIT License. See `LICENSE` for details.