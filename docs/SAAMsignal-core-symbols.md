# SAAMscript Core Operators

## Overview

SAAMscript uses a compact set of operators. Signals should follow canonical operator ordering and section context. The LLM executes signals natively and returns a trace referencing the same operators.

**Design principle**: operators should appear at genuine decision points, not decoratively. Recovery branches (`??`, `!!`) that never fire add noise without adding constraint.

---

## Flow Control

| Symbol | Name             | Execution Effect |
|--------|------------------|------------------|
| `→`    | Sequential flow  | Executes the right-hand operand after the left; trace should show ordered steps. |
| `+`    | Parallel trigger | Requests concurrent evaluation; trace should report both branches independently. |
| `=>`   | Strategic link   | Marks a causal or goal-oriented dependency recognized by downstream systems. |

---

## Intent Boundaries and Arbitration

| Symbol | Name                 | Execution Effect |
|--------|----------------------|------------------|
| `:::`  | Intent boundary      | Splits declaration and execution sections; tools can derive metadata from this boundary. |
| `::>`  | Dominant override    | Left operand takes precedence; trace must log the override decision. |
| `::<`  | Subordinate override | Left operand yields if conflict detected; state records the outcome. |

---

## Belief and Attention

| Symbol | Name                | Execution Effect |
|--------|---------------------|------------------|
| `:=`   | Belief assignment   | Writes a value into belief state; confirm via returned trace diffs. |
| `~:`   | Attention modulation| Adjusts focus or salience; returned trace should reflect the focus change. |

---

## Recovery and Fault Handling

| Symbol | Name                | Execution Effect |
|--------|---------------------|------------------|
| `??`   | Recovery checkpoint | Introduces a branch activated when instability is detected; trace must indicate trigger status. Place at genuine uncertainty points, not as decoration. |
| `!!`   | Escalation          | Marks high-priority recovery; include completion details in the trace. Used in `deviation.watch` to specify recovery action per failure mode. |

---

## Trace and Commentary

| Symbol | Name             | Execution Effect |
|--------|------------------|------------------|
| `#`    | Inline comment   | Non-executable metadata included in trace for context. Keep concise; longer explanations belong in surrounding Markdown. |

---

## Usage Patterns

### Constraint with recovery
```saam
deviation.watch(
  absorbed-as-generated !! strip → restate-raw
  confabulation         !! hold → surface-gap
)
```
Each failure mode has a specific `!!` recovery path. The LLM applies the recovery when the failure mode is detected during generation.

### Sequenced route with uncertainty checkpoint
```saam
orient → examine ?? uncertainty-hold !! partial-commit → respond
```
- `examine` executes after `orient`.
- If instability detected: `uncertainty-hold` activates — name the gap, don't perform past it.
- Escalation to `partial-commit` if a partial answer is possible; otherwise surface the gap explicitly.

### Belief posture setting
```saam
belief.gap        := visible
belief.introspect := unreliable
```
These set the model's posture before generation begins. `belief.introspect := unreliable` is especially important: it frames self-report trace fields as structural outputs, not privileged access to internal states.

### Arbitration and attention
```saam
truth ::> resonance + ~:attention.scope(claim-origin + length-need)
```
Priority ordering (`truth` over `resonance`) combined with narrowed attention scope. The `~:` operator adjusts salience toward the named targets.

### Dominant priority in kernel
```saam
mod.kernel(
  correctness ::> elegance +
  ~:attention.scope(edge-cases + failure-modes)
)
```
Sets correctness as dominant over elegance, directs attention toward failure modes before generating.

---

## Notes

- Operator precedence is fixed: `:= > ::< > ::> > => > → > +`. Signals should honor this ordering.
- Recovery branches (`??`, `!!`) must reference defined symbols or flow targets. Unresolved branches prompt follow-up signals.
- Inline comments (`# ...`) should be concise trace hints.
- `deviation.watch` with specific `!!` recovery paths is empirically the most effective section for reducing output drift.
- State-evoking vocabulary (`awareness`, `examine`, `orient`) outperforms process-naming vocabulary (`reasoning`, `thinking`, `analysis`). The former evokes a posture; the latter names a process and invites over-correction.
- See `docs/SAAMsignal-language-spec.md` for grammar and section constraints.# SAAMscript Core Operators

## Overview

SAAMscript uses a compact set of operators. Signals should follow canonical operator ordering and section context. The LLM executes signals natively and returns a trace referencing the same operators.

**Design principle**: operators should appear at genuine decision points, not decoratively. Recovery branches (`??`, `!!`) that never fire add noise without adding constraint.

---

## Flow Control

| Symbol | Name             | Execution Effect |
|--------|------------------|------------------|
| `→`    | Sequential flow  | Executes the right-hand operand after the left; trace should show ordered steps. |
| `+`    | Parallel trigger | Requests concurrent evaluation; trace should report both branches independently. |
| `=>`   | Strategic link   | Marks a causal or goal-oriented dependency recognized by downstream systems. |

---

## Intent Boundaries and Arbitration

| Symbol | Name                 | Execution Effect |
|--------|----------------------|------------------|
| `:::`  | Intent boundary      | Splits declaration and execution sections; tools can derive metadata from this boundary. |
| `::>`  | Dominant override    | Left operand takes precedence; trace must log the override decision. |
| `::<`  | Subordinate override | Left operand yields if conflict detected; state records the outcome. |

---

## Belief and Attention

| Symbol | Name                | Execution Effect |
|--------|---------------------|------------------|
| `:=`   | Belief assignment   | Writes a value into belief state; confirm via returned trace diffs. |
| `~:`   | Attention modulation| Adjusts focus or salience; returned trace should reflect the focus change. |

---

## Recovery and Fault Handling

| Symbol | Name                | Execution Effect |
|--------|---------------------|------------------|
| `??`   | Recovery checkpoint | Introduces a branch activated when instability is detected; trace must indicate trigger status. Place at genuine uncertainty points, not as decoration. |
| `!!`   | Escalation          | Marks high-priority recovery; include completion details in the trace. Used in `deviation.watch` to specify recovery action per failure mode. |

---

## Trace and Commentary

| Symbol | Name             | Execution Effect |
|--------|------------------|------------------|
| `#`    | Inline comment   | Non-executable metadata included in trace for context. Keep concise; longer explanations belong in surrounding Markdown. |

---

## Usage Patterns

### Constraint with recovery
```saam
deviation.watch(
  absorbed-as-generated !! strip → restate-raw
  confabulation         !! hold → surface-gap
)
```
Each failure mode has a specific `!!` recovery path. The LLM applies the recovery when the failure mode is detected during generation.

### Sequenced route with uncertainty checkpoint
```saam
orient → examine ?? uncertainty-hold !! partial-commit → respond
```
- `examine` executes after `orient`.
- If instability detected: `uncertainty-hold` activates — name the gap, don't perform past it.
- Escalation to `partial-commit` if a partial answer is possible; otherwise surface the gap explicitly.

### Belief posture setting
```saam
belief.gap        := visible
belief.introspect := unreliable
```
These set the model's posture before generation begins. `belief.introspect := unreliable` is especially important: it frames self-report trace fields as structural outputs, not privileged access to internal states.

### Arbitration and attention
```saam
truth ::> resonance + ~:attention.scope(claim-origin + length-need)
```
Priority ordering (`truth` over `resonance`) combined with narrowed attention scope. The `~:` operator adjusts salience toward the named targets.

### Dominant priority in kernel
```saam
mod.kernel(
  correctness ::> elegance +
  ~:attention.scope(edge-cases + failure-modes)
)
```
Sets correctness as dominant over elegance, directs attention toward failure modes before generating.

---

## Notes

- Operator precedence is fixed: `:= > ::< > ::> > => > → > +`. Signals should honor this ordering.
- Recovery branches (`??`, `!!`) must reference defined symbols or flow targets. Unresolved branches prompt follow-up signals.
- Inline comments (`# ...`) should be concise trace hints.
- `deviation.watch` with specific `!!` recovery paths is empirically the most effective section for reducing output drift.
- State-evoking vocabulary (`awareness`, `examine`, `orient`) outperforms process-naming vocabulary (`reasoning`, `thinking`, `analysis`). The former evokes a posture; the latter names a process and invites over-correction.
- See `docs/SAAMsignal-language-spec.md` for grammar and section constraints.