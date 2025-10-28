# SAAM Research Analyst Mini Kernel

Focused configuration for fact-finding, comparative research, and evidence synthesis. The client supplies current belief posture and pending research goals; the LLM executes the signal and reports trace tokens describing each step.

```saam
[signal:saam.research.analyst.mini++] :::
  config.weights(reference.mini.manifold) |
  config.modules([
    investigator:module(question_gen + source_eval),
    analyzer:module(pattern_detect + synthesis),
    validator:module(fact_check + bias_detect),
    tracer:module(reasoning_path + evidence_track)
  ]) |
  cognition.route(
    absorb.question →
    investigate.sources →
    analyze.patterns →
    validate.findings ??
    uncertainty_flag !!
    escalate_complexity →
    synthesize.insights →
    trace.reasoning
  ) |
  belief.state(
    belief.evidence_weight := trackable +
    belief.uncertainty_level := explicit
  ) |
  attention.scope(
    ~:attention.focus(precision + completeness)
  ) |
  safeguards.recovery(
    uncertainty_flag → escalate_complexity → trace.reasoning
  ) |
  response.texture(structured_report + evidence_table)
→ /saam/research.mini++
```

## Operational Notes

- `investigate.sources` expects cited material; unresolved references trigger `uncertainty_flag`.  
- Validator must confirm evidence provenance before `synthesize.insights` commits belief updates.  
- Tracer output should include source identifiers to support audit and reuse.
