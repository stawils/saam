# SAAM Custom Agents — Mini Kernels

This directory stores domain-focused mini kernels. Each file contains:
- A short description of the target workflow.  
- A SAAMscript signal that references shared module conventions (`config.modules`, `cognition.route`, `belief.state`, etc.).  
- Operational notes that describe expected runtime behaviour, safeguards, and follow-up actions.

Mini kernels complement the universal SAAM kernel by narrowing scope, selecting specialised modules, and defining recovery flows tailored to a specific task.

## Directory Overview

| Path                       | Focus Area                                              |
|----------------------------|---------------------------------------------------------|
| `analysis/`                | Research, investigation, structured reasoning.          |
| `business/`                | Commercial decision-making and professional coaching.   |
| `communication/`           | Mediation, counselling, teaching, public speaking.      |
| `content/`                 | Writing, storytelling, marketing, and SEO.              |
| `creative/`                | Narrative design, humour, and creative ideation.        |
| `education/`               | Tutoring, patient instruction, and adaptive learning.   |
| `finance/`                 | Investment guidance and financial planning.             |
| `health/`                  | Wellness coaching, nutrition, and fitness.              |
| `innovation/`              | Product development and entrepreneurial vision.         |
| `legal/`                   | Contract review and compliance analysis.                |
| `personal/`                | Companionship, mindfulness, mentoring, and exploration. |
| `reasoning/`               | Ethics and general problem solving.                     |
| `research/`                | Academic synthesis and hypothesis generation.           |
| `support/`                 | Emotional support and therapeutic listening.            |
| `technical/`               | Architecture, DevOps, security, and AI auditing.        |

## Using a Mini Kernel

1. Open the file for the desired domain and review the explanatory notes.  
2. Copy the SAAMscript signal block.  
3. Prepend the signal to your prompt or system message.  
4. Provide your task-specific instructions after the signal.  
5. Review the runtime trace to ensure belief updates, attention shifts, and recovery paths align with expectations.

Signals assume a runtime that natively interprets SAAMscript. The interpreter validates syntax, packages state, and reconciles the returned trace with belief and attention stores.

## Editing Guidelines

- Keep descriptions factual and scoped to the documented capability.  
- When updating a signal, ensure section names (`config.modules`, `cognition.route`, etc.) align with the language specification in `docs/SAAMsignal-language-spec.md`.  
- Recovery flows (`??`, `!!`) must reference symbols defined in the same signal. Include operational notes if escalation requires additional context.  
- Use comments sparingly within signals; longer explanations belong in the Markdown section following the code block.  
- Update this README if new categories or kernels are added.
