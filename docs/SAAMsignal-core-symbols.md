# SAAMscript Core Operators

## Overview

SAAMscript uses a compact set of operators. Signals should follow canonical operator ordering and section context. The LLM executes signals natively and returns a trace referencing the same operators. Understanding operator intent and expected trace artifacts keeps signals auditable and repairable.

Operator groups and execution effects:

## Flow Control

| Symbol | Name             | Execution Effect                                                                 |
|--------|------------------|-----------------------------------------------------------------------------------|
| `→`    | Sequential flow  | Executes the right-hand operand after the left; trace should show ordered steps. |
| `+`    | Parallel trigger | Requests concurrent evaluation; trace should report both branches independently. |
| `=>`   | Strategic link   | Marks a causal or goal-oriented dependency recognized by downstream systems.     |

## Intent Boundaries and Arbitration

| Symbol | Name                 | Execution Effect                                                                 |
|--------|----------------------|-----------------------------------------------------------------------------------|
| `:::`  | Intent boundary      | Splits declaration and execution sections; tools can derive metadata from this boundary.|
| `::>`  | Dominant override    | Left operand takes precedence; trace must log the override decision.             |
| `::<`  | Subordinate override | Left operand yields if conflict detected; state records the outcome.             |

## Belief and Attention

| Symbol | Name                | Execution Effect                                                                |
|--------|---------------------|----------------------------------------------------------------------------------|
| `:=`   | Belief assignment   | Writes a value into belief state; confirm via returned trace diffs.              |
| `~:`   | Attention modulation| Adjusts focus or salience; returned trace should reflect the focus change.      |

## Recovery and Fault Handling

| Symbol | Name                | Execution Effect                                                                                   |
|--------|---------------------|-----------------------------------------------------------------------------------------------------|
| `??`   | Recovery checkpoint | Introduces a branch activated when instability is detected; trace must indicate trigger status.    |
| `!!`   | Escalation          | Marks high-priority recovery; include completion details in the trace.           |

## Trace and Commentary

| Symbol | Name             | Execution Effect                                                        |
|--------|------------------|-------------------------------------------------------------------------|
| `#`    | Inline comment   | Non-executable metadata included in trace for context.                |


## Usage Patterns

### Sequenced plan with recovery
```saam
reflect → resolve ?? legality-echo !! patch → commit
```
- `resolve` executes after `reflect`.
- If instability is reported, `legality-echo` is activated; escalation to `patch` must be logged before `commit`.

### Arbitration and attention
```saam
legality-loop-filter::<intent.override + ~:attention.scope(threat-path)
```
- `legality-loop-filter` yields when `intent.override` asserts dominance.
- Attention scope request is recorded in the payload and verified against returned salience data.

### Belief and goal binding
```saam
belief.fork_threat := true => activate.counterfactual-map
```
- Belief assignment is committed after the trace confirms success.
- Strategic link expresses that `activate.counterfactual-map` depends on the new belief state.

---

## Notes

- Operator precedence is fixed: `:= > ::< > ::> > => > → > +`. Signals should honor this ordering; noncompliance may cause preflight checks to fail.
- Recovery branches (`??`, `!!`) must reference defined symbols or flow targets; unresolved branches prompt follow-up signals.
- Inline comments (`# ...`) should be concise trace hints; place longer explanations in Markdown around the signal.
- See `docs/SAAMsignal-language-spec.md` for grammar and section constraints.
