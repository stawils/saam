# SAAM Bounded Metacognition Kernel

Enables structured self-critique with architectural safeguards against infinite reflection loops. The kernel separates the acting agent from the auditing agent, enforces a finite reflection budget, uses typed critique questions instead of open-ended reflection, and exits early when the answer converges or the budget is exhausted.

```saam
[signal:saam.metacognition.bounded++] :::
  config.modules([
    actor:module(task_execution + answer_generation),
    auditor:module(assumption_audit + evidence_check),
    grounder:module(tool_invocation + external_evidence),
    convergence:module(delta_check + stability_detect)
  ]) |

  deviation.watch(
    absorbed-as-generated !! strip → restate-raw
    confabulation         !! hold → surface-gap
    length-redundancy     !! compress → last-genuine
    overclaim-certainty   !! flag → surface-uncertainty
  ) |

  cognition.route(
    absorb.task →
    act.generate_answer →
    audit.typed_critique ?? evidence_gap !! flag_ungrounded →
    check.convergence ?? answer_stable → exit.deliver !! budget_exceeded → exit.deliver_best →
    trace.reflection
  ) |

  belief.gap        := visible
  belief.introspect := unreliable

  attention.scope(
    ~:attention.focus(assumption_detection + evidence_sufficiency)
  ) |

  safeguards.recovery(
    evidence_gap → flag_ungrounded → ground.external_evidence +
    answer_stable → exit.deliver +
    budget_exceeded → exit.deliver_best
  ) |

  response.texture(
    final_answer +
    audit_trail:visible(per_pass:assumption_audit + evidence_check) +
    convergence_note:visible(position_changes + exit_reason)
  )
→ /saam/metacognition.bounded++
```

## Module Roles

| Module Key     | Purpose                                                                                           |
|----------------|---------------------------------------------------------------------------------------------------|
| `actor`        | Produces the answer. Only generates; never self-critiques.                                        |
| `auditor`      | Critiques the actor's output using typed checks. Never evaluates itself.                          |
| `grounder`     | Forces contact with external evidence (tool output, data, citations) before each revision cycle.  |
| `convergence`  | Compares the current answer to the previous pass; signals `answer_stable` when delta is negligible.|

## Typed Audit Criteria

The auditor does **not** perform open-ended reflection. Each pass evaluates the actor's output against exactly four structured questions:

1. **Assumption audit** — "What assumptions did the answer rely on? Are they stated and justified?"
2. **Evidence check** — "What evidence supports the answer? Is any claim ungrounded?"
3. **Bias scan** — "Does the answer favour a particular perspective without acknowledging alternatives?"
4. **Counterargument** — "What is the single strongest objection to this answer?"

Each criterion produces a bounded output (a short finding, not a recursive essay).

## Exit Conditions

The kernel exits the reflection loop via one of two paths:

| Exit Path          | Trigger                                                                 |
|--------------------|-------------------------------------------------------------------------|
| `exit.deliver`     | `convergence` detects `answer_stable` — the revision did not materially change the answer. |
| `exit.deliver_best`| `budget` reaches zero — the best available answer is delivered with an audit trail.        |

Both paths produce the final response with the structured output format defined below.

## Output Format

The `response.texture` directive requires three **visible** sections in every response. This prevents the audit trace from being absorbed silently into the reasoning and lost from the output.

### Required Response Structure

```
## Answer
Final position with supporting arguments and evidence.

## Audit Trail
For each reflection pass, show:
- Pass N (of max)
- Assumption audit: [findings]
- Evidence check: [findings]
- Bias scan: [findings]
- Counterargument: [strongest objection considered]
- Revision delta: [what changed from previous pass, or "no material change"]

## Convergence Note
- Position changes: [e.g. "stable from Pass 1" or "shifted from X to Y in Pass 2"]
- Exit reason: [answer_stable | budget_exceeded]
- Total passes used: [N of max]
```

The `audit_trail:visible` and `convergence_note:visible` modifiers signal that these sections are **mandatory output**, not optional internal reasoning. If a runtime omits them, a corrective signal should be issued.

## Operational Notes

- The actor and auditor are architecturally separated; the auditor **never** critiques its own critique. This prevents recursive self-reference.
- `belief.passes_remaining` defaults to `3`. Adjust upward for high-stakes decisions or downward for latency-sensitive tasks. Values above `5` are not recommended.
- The `grounder` module is the circuit breaker: it forces the loop out of internal reasoning and into external reality before any revision occurs.
- If `evidence_gap` is triggered and no grounding tool is available, the `flag_ungrounded` escalation marks the claim in the audit trail rather than looping.
- Convergence is measured as material change: if the core conclusion and supporting evidence are unchanged, the answer is considered stable regardless of surface rewording.
- The audit trail in the response shows each pass's findings, creating transparency into how the final answer was reached.
