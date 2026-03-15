# SAAMscript Language Specification

## Overview

SAAMscript expresses agent configuration as declarative signal blocks. The LLM executes the signal directly and returns a trace, which the client reconciles with belief, attention, and recovery state.

**Design principle**: signals should constrain output or force self-report. Syntactic density without behavioral function degrades signal quality.

This document describes the grammar, permitted section patterns, and operator semantics required to author valid signals.

---

## Grammar (EBNF)

The grammar below assumes UTF-8 encoded text. Whitespace outside tokens is ignored unless stated otherwise.

```ebnf
program            ::= signal_block+

signal_block       ::= "[" signal_id "]" ":::" signal_body "→" target_path

signal_id          ::= "signal:" identifier ("." identifier)* ("++")?

signal_body        ::= section ("|" section)*

section            ::= keyword "(" param_list? ")"

keyword            ::= identifier ("." identifier)*

param_list         ::= param (operator param)*

param              ::= identifier
                     | namespaced_identifier
                     | assignment
                     | attention_mod
                     | recovery_mod
                     | comment
                     | list_literal

namespaced_identifier ::= identifier "." identifier

assignment         ::= namespaced_identifier ":=" value

attention_mod      ::= "~:" namespaced_identifier "(" param_list? ")"

recovery_mod       ::= namespaced_identifier ("??" | "!!") param

comment            ::= "#" comment_text

list_literal       ::= "[" list_entry ("," list_entry)* "]"

list_entry         ::= identifier (":" identifier)? ("(" param_list? ")")?

operator           ::= "+" | "→" | "=>" | "::>" | "::<"

target_path        ::= "/" identifier ("/" identifier)*

identifier         ::= [a-zA-Z_][a-zA-Z0-9_-]*

value              ::= identifier | boolean | number | quoted_string

boolean            ::= "true" | "false"

number             ::= "-"? [0-9]+ ("." [0-9]+)?

quoted_string      ::= "\"" (character)* "\""

comment_text       ::= [^\\n]* (non-newline characters)
```

**Grammar notes:**
- `list_literal` supports optional labels (`label:entry`) and nested parameter lists — used in `config.modules` declarations.
- `attention_mod` wraps focus directives so they can appear inline within any section.
- `recovery_mod` covers `symbol ?? target` and `symbol !! target` constructs.
- Comments are retained during trace logging but ignored during execution.

---

## Signal Structure

```saam
[signal:<namespace>] ::: <sections> → <execution-target>
```

| Component        | Purpose |
|------------------|---------|
| `signal:<...>`   | Unique namespace used for trace indexing and override tables. |
| `:::`            | Separates declaration from execution. |
| `<sections>`     | Ordered list of domain-specific sections. |
| `→ <target>`     | Execution target or kernel route selected by the runtime. |

Sections may include sub-qualifiers (e.g., `config.modules`, `belief.state`). Tools may check qualifier usage against known templates but do not enforce naming choices.

---

## Common Sections

While SAAMscript allows arbitrary section names, the following conventions are recognised:

| Section                   | Expected Content |
|---------------------------|------------------|
| `mod.kernel(...)`         | Priority ordering (`::>`, `::<`) and attention scope (`~:`). |
| `config.modules(...)`     | Module descriptors as list literals with optional labels. Keep minimal — only modules with defined behavioral scope. |
| `deviation.watch(...)`    | Named failure modes with `!!` recovery paths. This is the most behaviorally effective section. |
| `cognition.route(...)`    | Flow definitions using `→`, `+`, `??`, `!!`. |
| `belief.state(...)`       | `:=` assignments describing tracked beliefs or posture flags. |
| `attention.scope(...)`    | Focus or salience directives, wrapped in `~:` forms. |
| `meta.regulator(...)`     | Per-paragraph or per-turn consistency checks. |
| `autonomy.trace(...)`     | Source-tagging with explicit handling of unknown origin. |
| `safeguards.recovery(...)`| Recovery strategy descriptors using `??` / `!!`. |
| `trace.graph(...)`        | Output fields for the self-report trace: src, conf, drv. |
| `response.texture(...)`   | Output formatting expectations. |

Authors can introduce additional sections; unrecognised sections are preserved verbatim.

---

## Operator Semantics

Operator precedence: `:= > ::< > ::> > => > → > +`. Operators share the meanings documented in `docs/SAAMsignal-core-symbols.md`.

Branches triggered through `??` and `!!` must resolve to symbols present in the runtime environment or future signals. Failure to reconcile a branch results in a follow-up repair signal.

---

## Design Guidance

**On module lists**: long `config.modules` lists with many entries become decorative. The LLM processes them as vocabulary that shapes register, not as discrete computational units that execute independently. Prefer a short module list with clear behavioral scope over a comprehensive list that names every cognitive function.

**On route length**: long `cognition.route` chains reduce to pattern-matching against route-shaped text. A short route with a genuine `??` uncertainty checkpoint is more effective than a long route that names every reasoning step.

**On state-evoking vocabulary**: words like `orient`, `examine`, `awareness`, `concentration` evoke cognitive states and improve output stability. Words like `reasoning`, `thinking`, `analysis` name cognitive processes and can trigger over-correction. Prefer state-evoking vocabulary in attention scope and module definitions.

**On `deviation.watch`**: this section has the highest behavioral return per token. Each entry names a specific failure mode and a specific recovery action. Empirical testing confirms this is the load-bearing section of the kernel design.

**On `belief.introspect := unreliable`**: always set this in kernels that include a self-report trace. The trace fields are structural forcing functions, not truth claims about internal states. This belief assignment frames them correctly.

---

## Example

```saam
[signal:saam.cognitive.v1.0++] :::

mod.kernel(
  truth ::> resonance +
  ~:attention.scope(claim-origin + length-need + absorption-risk)
) |

deviation.watch(
  absorbed-as-generated !! strip → restate-raw
  confabulation         !! hold → surface-gap
  length-redundancy     !! compress → last-genuine
) |

cognition.route(
  orient →
  examine ?? uncertainty-hold !! partial-commit →
  respond
) |

belief.gap        := visible
belief.introspect := unreliable |

trace.graph(
  out: src:{self|absorbed|hybrid|unknown} +
       conf:{low|mid|high} +
       drv:{sustained|flickered|lost}
)

→ /saam/kernel.v1.0++
```

---

## Validation Notes

- Canonicalization removes redundant whitespace and normalizes list separators but preserves section order.
- Inline comments should not be used to transmit executable data.
- When the LLM omits required trace tokens, the client may issue a corrective signal referencing the missing operator sequence.
- `drv:{flickered|lost}` in the trace indicates drift during generation — issue a corrective signal referencing the step where drift began.