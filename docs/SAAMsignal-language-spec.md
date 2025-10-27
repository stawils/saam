# SAAMscript Language Specification


## Overview

SAAMscript expresses agent configuration as declarative signal blocks. The interpreter validates syntax, normalizes structure, and forwards canonical signals together with state payloads. The LLM runtime executes the signal directly and returns a trace that the interpreter reconciles with belief, attention, and recovery state.

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

Notes:
- `list_literal` supports optional labels (`label:entry`) and nested parameter lists; this matches patterns used in kernel module declarations.
- `attention_mod` wraps focus directives so they can appear inline within any section.
- `recovery_mod` covers `symbol ?? target` and `symbol !! target` constructs.
- Comments are retained during trace logging but ignored by execution.

---

## Signal Structure

```saam
[signal:<namespace>] ::: <sections> → <execution-target>
```

| Component        | Purpose                                                                                     |
|------------------|---------------------------------------------------------------------------------------------|
| `signal:<...>`   | Unique namespace used for trace indexing and override tables.                               |
| `:::`            | Separates declaration from execution; interpreter splits sections at this boundary.         |
| `<sections>`     | Ordered list of domain-specific sections (`config.modules`, `cognition.route`, etc.).       |
| `→ <target>`     | Execution target or kernel route selected by the runtime.                                   |

Sections may include sub-qualifiers (e.g., `config.modules`, `belief.state`). The interpreter checks qualifier usage against known templates but does not fix naming choices.

---

## Common Sections

While SAAMscript allows arbitrary section names, the following conventions are recognised by the interpreter when constructing payloads:

| Section                   | Expected Content                                                                    |
|---------------------------|--------------------------------------------------------------------------------------|
| `config.modules(...)`     | Module descriptors, often expressed as list literals with optional labels.          |
| `config.weights(...)`     | Weighting profile or references to stored manifolds.                               |
| `cognition.route(...)`    | Flow definitions using `→`, `+`, `??`, `!!`.                                        |
| `belief.state(...)`       | `:=` assignments describing tracked beliefs or flags.                               |
| `attention.scope(...)`    | Focus or salience directives, frequently wrapped in `~:` forms.                     |
| `safeguards.recovery(...)`| Recovery strategy descriptors using `??` / `!!`.                                    |
| `response.texture(...)`   | Output formatting expectations.                                                     |

Authors can introduce additional sections; unrecognised sections are preserved verbatim in the canonical signal.

---

## Operator Semantics

Operator precedence: `:= > ::< > ::> > => > → > +`. Operators share the meanings documented in `docs/SAAMsignal-core-symbols.md`.

Branches triggered through `??` and `!!` must resolve to symbols present in the runtime environment or future signals. Failure to reconcile a branch results in a follow-up repair signal.

---

## Example

```saam
[signal:meta.agent.core++] :::
  config.weights(reference.default.manifold) |
  config.modules([
    investigator:module(question_gen + source_eval),
    analyzer:module(pattern_detect + synthesis),
    validator:module(fact_check + bias_detect),
    tracer:module(reasoning_path + evidence_track)
  ]) |
  cognition.route(
    absorb →
    analyze →
    validate ?? legality_review !!
    repair →
    commit
  ) |
  belief.state(
    belief.evidence_integrity := tracked +
    belief.route_complete := false
  ) |
  attention.scope(precision + completeness) |
  safeguards.recovery(legality_review → repair)
→ /saam/kernel.resonance.core++
```

---

## Validation Notes

- Canonicalization removes redundant whitespace and normalizes list separators but preserves section order.  
- Inline comments should not be used to transmit executable data.  
- When the LLM omits required trace tokens, the interpreter issues a corrective signal referencing the missing operator sequence.  
- For interpreter responsibilities and reconciliation flow, see the Execution Workflow section in `README.md`.
