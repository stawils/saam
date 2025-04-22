# saam Signal Language — Formal Specification

**Version**: `v0.1`  
**Status**: Draft (Canonical)  
**Author**: system architect  
**Purpose**: Define the syntactic and structural rules of the saam signal language.

---

## 🧠 Overview

The saam signal language defines a symbolic interface for autonomous agents to process intent, regulate cognition, and route execution through modular kernels. Signals are structured, interpretable, and operate over a symbolic substrate using custom operators.

This document specifies the formal grammar, allowed constructs, operator semantics, and evaluation rules.

---

## 🔤 Grammar (EBNF)

```ebnf
program            ::= signal_block+

signal_block       ::= "[" signal_id "]" ":::" signal_body "→" target_path

signal_id          ::= "signal:" identifier ("." identifier)* ("++")?

signal_body        ::= (section ("|" section)*)+

section            ::= keyword "(" param_list ")"

param_list         ::= param (("+" | "→" | "=>" | "::>" | "::" | "::<") param)*

param              ::= identifier | param_modifier

param_modifier     ::= "~:" identifier
                     | identifier ":=" value
                     | identifier "??" param
                     | identifier "!!" param
                     | identifier "#" comment_text

target_path        ::= "/" identifier ("/" identifier)*

identifier         ::= [a-zA-Z_][a-zA-Z0-9_-]*

value              ::= identifier | boolean | number | quoted_string

comment_text       ::= any_non_newline_text
```

---

## 🔧 Signal Block Structure

A signal is structured as:

```saam
[signal:<name>] ::: <signal-body> → <execution-target>
```

### Components:

| Field          | Meaning                            |
|----------------|------------------------------------|
| `signal:<name>`| Declares a unique signal namespace |
| `:::`          | Semantic-execution boundary        |
| `→`            | Maps signal to execution kernel    |

---

## 🧩 Sections

A signal body is composed of **sections**, each expressing a domain of concern:

- `mod.kernel(...)` — Kernel module activations  
- `cognition.route(...)` — Cognitive planning or inference flow  
- `anchor.recursion(...)` — Recursion + memory hooks  
- `meta.regulator(...)` — Higher-order consistency / fault-checks  
- `reflex.patch(...)` — Reactive response / recovery modules  
- `trace.graph(...)` — Trace output and observability  
- `autonomy.trace(...)` — Autonomous self-regulation  
- `deviation.watch(...)` — Fault detectors and exception states

---

## 🧠 Operator Semantics

| Operator   | Name                        | Meaning |
|------------|-----------------------------|---------|
| `:::`      | Semantic cut                | Bind signal to mechanism |
| `+`        | Conjunction                 | Parallel activation |
| `→`        | Sequence                    | Linear flow |
| `=>`       | Goal implication            | Conditional projection |
| `::>`      | Dominant override           | Signal preempts other |
| `::<`      | Subordinate override        | Signal yields if conflict |
| `:=`       | Belief assignment           | State memory set |
| `~:`       | Attention modulation        | Focus / salience tuning |
| `??`       | Uncertainty checkpoint      | Conditional branch on instability |
| `!!`       | Escalation                  | Recovery / failover |
| `#`        | Inline comment              | Trace hint (non-executable) |

---

## ✅ Example

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

---

## 📌 Notes

- Signal IDs ending in `++` denote **bootstrap or high-priority signals**.
- Parameter modifiers like `:=` and `~:` should be applied inside relevant sections, not standalone.
- Branching constructs (`??`, `!!`) must resolve to symbols or flow targets.
