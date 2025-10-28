# SAAMscript Core Operators


## Overview

SAAMscript relies on a compact set of symbolic operators. Signals should adhere to canonical operator ordering and section context. The LLM executes signals natively and returns a trace that references the same operators. Understanding each operator’s intent and the expected trace artefacts is essential for authoring signals that remain auditable and repairable.

Operators are grouped by function below. All precedence references follow the ordering defined in the language specification (`:=` highest, `+` lowest).

---

## Flow Control

| Symbol | Name             | Execution Effect                                                                 |
|--------|------------------|-----------------------------------------------------------------------------------|
| `→`    | Sequential flow  | Executes the right-hand operand after the left; trace must show ordered steps.   |
| `+`    | Parallel trigger | Requests concurrent evaluation; trace should report both branches independently. |
| `=>`   | Strategic link   | Marks a causal or goal-oriented dependency recognised by downstream modules.     |

## Intent Boundaries and Arbitration

| Symbol | Name                 | Execution Effect                                                                 |
|--------|----------------------|-----------------------------------------------------------------------------------|
| `:::`  | Intent boundary      | Splits declaration and execution sections; tools can derive payloads from this boundary.|
| `::>`  | Dominant override    | Left operand takes precedence; trace must log the override decision.             |
| `::<`  | Subordinate override | Left operand yields if conflict detected; override table retains the outcome.    |

## Belief and Attention

| Symbol | Name                | Execution Effect                                                                |
|--------|---------------------|----------------------------------------------------------------------------------|
| `:=`   | Belief assignment   | Writes a value into belief state; confirmation occurs via returned trace diffs.  |
| `~:`   | Attention modulation| Adjusts focus or salience; returned trace should reflect the focus change.      |

## Recovery and Fault Handling

| Symbol | Name                | Execution Effect                                                                                   |
|--------|---------------------|-----------------------------------------------------------------------------------------------------|
| `??`   | Recovery checkpoint | Introduces a branch activated when instability is detected; trace must indicate trigger status.    |
| `!!`   | Escalation          | Marks high-priority recovery; completion details should be present in the trace. |

## Trace and Commentary

| Symbol | Name             | Execution Effect                                                        |
|--------|------------------|-------------------------------------------------------------------------|
| `#`    | Inline comment   | Non-executable metadata included in trace for contextual review.      |

---

## Usage Patterns

### Sequenced Plan with Recovery
```saam
reflect → resolve ?? legality-echo !! patch → commit
```
- `resolve` executes after `reflect`.
- If instability is reported, `legality-echo` is activated; escalation to `patch` must be logged before `commit`.

### Arbitration and Attention
```saam
legality-loop-filter::<intent.override + ~:attention.scope(threat-path)
```
- `legality-loop-filter` yields when `intent.override` asserts dominance.
- Attention scope request is recorded in the payload and verified against returned salience data.

### Belief and Goal Binding
```saam
belief.fork_threat := true => activate.counterfactual-map
```
- Belief assignment is committed after the trace confirms success.
- Strategic link expresses that `activate.counterfactual-map` depends on the new belief state.

---

## Notes

- Operator precedence is fixed: `:= > ::< > ::> > => > → > +`. Signals must honour this ordering or preflight checks will fail.  
- Recovery branches (`??`, `!!`) must reference defined symbols or flow targets; unresolved branches prompt follow-up signals.  
- Inline comments (`# ...`) should provide concise trace hints only; extensive documentation belongs in Markdown surrounding the signal.  
- See `docs/SAAMsignal-language-spec.md` for grammar rules and section constraints.
