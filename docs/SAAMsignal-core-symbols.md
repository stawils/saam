# Core Symbolic Operators — SAAM Signal Language

**Version**: `v0.1`  
**Status**: Draft (Canonical)  
**Author**: system architect  
**Purpose**: Define the symbolic operators used in SAAM signal expressions, their meanings, and contextual usage.

---

## 🧠 Overview

The SAAM symbolic language enables autonomous cognition and recovery using composable, typed operators. These operators control intent routing, arbitration, planning, belief management, and signal fallbacks. This document defines each operator, grouped by purpose, with examples and usage notes.

---

## 🔤 Operator Reference Table

### 1. **Execution and Flow**

| Symbol | Name               | Function                            | Example |
|--------|--------------------|-------------------------------------|---------|
| `→`    | Sequential flow    | Ordered signal execution            | `reflect → resolve → commit` |
| `+`    | Conjunction        | Parallel signal activation          | `sense + recall` |
| `=>`   | Strategic causality| Projects goal relevance             | `verify => adjust` |

---

### 2. **Semantic Boundaries**

| Symbol | Name                        | Function                                 | Example |
|--------|-----------------------------|------------------------------------------|---------|
| `:::`  | Signal-intent boundary      | Separates declaration from execution     | `[signal:x] ::: mod.kernel(...)` |
| `::>`  | Dominant override           | Prioritize left operand                  | `emergency-plan ::> default-mode` |
| `::<`  | Subordinate override        | Subordinate left operand                 | `low-risk-mode ::< recovery-mode` |

---

### 3. **State and Belief**

| Symbol | Name                | Function                          | Example |
|--------|---------------------|-----------------------------------|---------|
| `:=`   | Belief assignment   | Sets value in belief state memory | `belief.check := true` |
| `~:`   | Attention modulation| Adjusts focus/salience            | `~:attention.scope(threat + queen-line)` |

---

### 4. **Error and Recovery Control**

| Symbol | Name                   | Function                                  | Example |
|--------|------------------------|-------------------------------------------|---------|
| `??`   | Uncertainty checkpoint | Conditional signal based on instability   | `resolve ?? legality-echo` |
| `!!`   | Escalation trigger     | Urgent fallback activation                | `verify !! fallback-plan` |

---

### 5. **Trace and Meta**

| Symbol | Name              | Function                        | Example |
|--------|-------------------|----------------------------------|---------|
| `#`    | Inline comment    | Trace hint, non-executable       | `belief.set := true # after fallback` |

---

## ✅ Symbol Use Patterns

### Chained Control
```saam
reflect → resolve ?? legality-echo !! patch → commit
```
> Sequential plan with conditional error routing and recovery fallback.

---

### Arbitration and Attention
```saam
legality-loop-filter::<intent.override + ~:attention.scope(threat-path)
```
> Arbitration with subordinate legality check and salience-driven attention.

---

### Belief and Goal Binding
```saam
belief.fork_threat := true => activate.counterfactual-map
```
> Declarative state memory triggers goal-specific planning.

---

## 📌 Notes

- Operator resolution follows strict **precedence**:
  ```
  := > ::< > ::> > => > → > +
  ```
- All operators are **contextual** to section type (e.g., belief modifiers inside `mod.kernel`, attention inside `~:` scope).
