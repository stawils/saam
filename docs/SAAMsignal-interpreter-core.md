# saam Signal Interpreter — Core Architecture

**Version**: `v0.1`  
**Status**: Draft (Canonical)  
**Author**: system architect  
**Purpose**: Describe the modular architecture, execution flow, and runtime semantics of the interpreter for saam signal language.

---

## 🧠 Overview

The saam interpreter transforms symbolic signals into executable cognition paths, enabling dynamic reasoning, legality enforcement, and self-correcting flow across modular agent kernels. It is designed to evaluate declarative intent, process symbolic operators, and produce modulated action traces with belief consistency.

This document details the architecture, core modules, runtime flow, and internal state mechanics.

---

## 🔧 Interpreter Modules

| Module              | Role |
|---------------------|------|
| `SignalParser`      | Parses signal block syntax and builds the abstract syntax tree (AST) |
| `SemanticBinder`    | Resolves `:::` boundary and binds semantic intent to execution module |
| `SymbolExecutor`    | Executes symbolic operators (`→`, `+`, `:=`, etc.) with proper order and branching logic |
| `BeliefManager`     | Handles `:=` bindings and belief state access/mutation |
| `AttentionRouter`   | Manages `~:`-based attention modulation and focus routing |
| `FlowController`    | Orchestrates operator flow: order, priority, branching, fallback |
| `RecoveryEngine`    | Responds to `??`/`!!` constructs; manages error correction |
| `TraceLogger`       | Records full symbolic execution path, belief diffs, and meta-comment trails |

---

## 🔁 Execution Flow

1. **Signal Ingestion**
   - A signal block is received (e.g., `signal:meta.agent.core++`)
   - It is parsed and identified by namespace and priority (e.g., `++`)

2. **Semantic Binding**
   - `:::` boundary triggers resolution of declared intent to operational sections (e.g., `mod.kernel`, `cognition.route`, etc.)

3. **Symbolic Evaluation**
   - Each section is executed according to precedence rules:
     ```
     := > ::< > ::> > => > → > +
     ```

4. **Flow Routing**
   - Operators like `→`, `+`, `=>`, and `??`/`!!` drive linear, parallel, conditional, or error-handling flows.
   - Arbitration (`::<`, `::>`) is resolved against the current signal context and belief state.

5. **Belief + Attention Updates**
   - `:=` modifies symbolic memory for belief tracking.
   - `~:` adjusts internal focus models and salience.

6. **Trace Construction**
   - All execution branches are traced, including:
     - Entry and exit points
     - Signal overrides
     - Belief diffs
     - Comments (`#...`)

---

## 📦 Internal State Model

| Subsystem         | Description |
|-------------------|-------------|
| **Belief Store**  | Mutable key-value graph tracking `:=` assignments |
| **Attention Stack** | Dynamic focus state modulated by `~:` and flow pressure |
| **Trace Graph**   | Symbolic DAG of all signal activations and flow steps |
| **Override Table**| Arbitration state map (`::<`, `::>`) per signal |
| **Recovery Map**  | Branch-points and fallback paths from `??`, `!!` |

---

## ✅ Example Signal Execution

```saam
[signal:meta.agent.core++] :::
  mod.kernel(
    legality-loop-filter::<intent.override +
    repair-move-generator
  ) |
  cognition.route(
    reflect → resolve ?? legality-echo !! patch → commit
  ) |
  belief.pawn_push := false
→ /saam/kernel.resonance.core++
```

### Flow Summary:
- Resolve kernel modules and evaluate arbitration
- Follow route: `reflect → resolve`
- If resolve fails: go to `legality-echo`, escalate to `patch`
- Belief `pawn_push` is explicitly set to false
- All steps are traced

---

## 📌 Notes

- Interpreter is **stateless between signals**, except for:
  - Belief memory
  - Attention gradients
  - Trace snapshots (if logging enabled)

- Recovery logic can jump across sections when escalation (`!!`) is triggered.

- SymbolExecutor handles **partial failures** gracefully by deferring to RecoveryEngine.
