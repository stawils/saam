# SAAM — Signal-Aligned Activation Manifold

<div align="center">

![SAAM Logo](assets/saam-logo.png "SAAM: Signal-Aligned Activation Manifold")


**SAAM** (Signal-Aligned Activation Manifold) is a technical framework for guiding large language models (LLMs) using structured signals written in SAAMscript, a symbolic language.

</div>

## Table of Contents
- [Overview](#overview)
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
- Define cognitive reasoning paths for LLMs
- Implement safety guards and ethical boundaries
- Enable belief tracking and reasoning trace generation
- Support error recovery mechanisms
- Offer domain-specific kernel implementations

### What Problem Does SAAM Solve?

Traditional prompting methods provide limited control over LLM reasoning processes, leading to inconsistent outputs and difficulty tracking decision-making paths. SAAM addresses this by offering structured cognitive blueprints that guide model behavior predictably.

### Technologies Used

SAAM is implemented as plain text signals and requires no special software. It operates by providing structured instructions in SAAMscript that LLMs interpret during execution.

---

## Technical Architecture

### Core Components
- **SAAMscript**: A symbolic language for defining cognitive instructions
- **Universal Kernel**: A general-purpose cognitive framework (`/agent/SAAM-kernel-v1.0/saam.cognitive.v1.0++.md`)
- **Domain-Specific Kernels**: Specialized implementations in `/agent/custom-agents/`
- **Signal Structure**: `[signal:<namespace>] ::: <body> → <target>`

### How SAAM Works
1. Signal parsing and validation
2. Cognitive blueprint application to LLM context
3. Reasoning trace generation during execution
4. Belief tracking and update recording
5. Recovery procedure execution when needed

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
2. This provides belief tracking, reasoning trace generation, consistency checks, and built-in recovery strategies
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
- `<body>` contains operators, modules, and cognitive routes
- `<target>` selects the kernel or route to use

### Operator Execution Order
```
:= > ::< > ::> > => > → > +
```

---

## Configuration

### Available Kernels
- **Universal Kernel**: `/agent/SAAM-kernel-v1.0/saam.cognitive.v1.0++.md` - General reasoning with belief tracking
- **Domain-Specific Kernels**: `/agent/custom-agents/` - Over 40 specialized implementations for various domains

### Signal Operators
- `:=` - Belief assignment/updates
- `::<` / `::>` - Module prioritization/overrides
- `??` - Uncertainty handling
- `!!` - Escalation to stronger safeguards
- `+` - Parallel execution

For complete operator reference, see:
- `docs/SAAMsignal-language-spec.md`
- `docs/SAAMsignal-core-symbols.md`

---

## API Reference

SAAM operates through structured text signals. No API calls are required beyond normal LLM interactions.

### Core Signal Elements
- `tone()` - Sets communication style
- `style()` - Defines output format
- `flow()` - Specifies reasoning sequence
- `intent.field()` - Defines primary objectives
- `mod.kernel()` - Applies safety constraints
- `cognition.route()` - Details processing steps
- `response.texture()` - Formats output style

---

## Examples

### Basic Coding Task
```saam
[signal:agent.code.develop++] :::
  tone(precise) | style(code-focused) |
  flow(understand → plan → write.code → run.tests) |
  intent.field(correctness-first + clarity-goal) |
  mod.kernel(legality-guard::<syntax.check + type.safety) |
  cognition.route(parse.reqs → design.algo → implement ?? simplify !! debug) |
  response.texture(functional.code)
→ /saam/kernel.coding.v1

Write a Python function that filters even numbers from a list and returns them in the same order.
```

### Creative Writing Task
```saam
[signal:agent.story.generate++] :::
  tone(genre.appropriate) | style(vivid) |
  flow(plan.scene → build.char → write.prose) |
  intent.field(narrative.consistency_first) |
  mod.kernel(narrative.guard::<plot.consistency + char.motivation) |
  cognition.route(advance.plot → write.dialogue ?? pacing.adjust !! add.conflict) |
  response.texture(polished.narrative)
→ /saam/kernel.storyteller.v1

Write a tense sci-fi scene where Captain Eva confronts Kael about suspected sabotage.
```

---

## Tools and Integrations

### SAAM Tools on ChatGPT
- [SAAMGPT](https://chatgpt.com/g/g-6806ba323f24819180a2a11ba4067384-saamgpt): Full kernel integration for legality-first reasoning and belief repair.
- [SAAM Converter](https://chatgpt.com/g/g-67ec188b7b8081919387b2c28c9f1dec-saam-converter): Converts natural-language prompts into structured SAAM signals.
- [SAAM Text2Img Generator](https://chatgpt.com/g/g-681f7688e6cc8191a54b7373809624b5-saam-text2img-generator): A symbolic image generation agent that interprets structured prompts using SAAM signal language. It aligns mood, scene, and composition with symbolic consistency and traceable intent routing.
- **[SAAM Kernel Creator](../.claude/skills/saam-kernel-creator): Create custom SAAM kernels by describing requirements. Generates valid SAAMscript signals with proper operator precedence, module declarations, and cognitive architecture. Ideal for developers, researchers, and organizations building AI agents with verifiable reasoning trails.
---
---

## License

MIT License. See `LICENSE` for details.
