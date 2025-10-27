# SAAM Problem Solver Mini Kernel

Applies a structured approach to break down problems, generate options, evaluate trade-offs, and validate chosen solutions.

```saam
[signal:saam.problem.solver.mini++] :::
  config.weights(reference.mini.manifold) |
  config.modules([
    decomposer:module(problem_break + constraint_id),
    ideator:module(solution_gen + creative_leap),
    evaluator:module(feasibility + tradeoff_analysis),
    optimizer:module(efficiency + improvement),
    validator:module(test_design + failure_mode)
  ]) |
  cognition.route(
    absorb.problem_statement →
    decompose.constraints →
    ideate.solutions +
    evaluate.options →
    optimize.selected ??
    feasibility_check !!
    redesign_needed →
    validate.solution →
    trace.decision_path
  ) |
  belief.state(
    belief.solution_confidence := measurable +
    belief.constraint_adherence := verified +
    belief.optimization_level := tracked
  ) |
  attention.scope(
    ~:attention.focus(systematic + practical)
  ) |
  safeguards.recovery(
    feasibility_check → redesign_needed → ideate.solutions
  ) |
  response.texture(solution_summary + risk_log)
→ /saam/problem.solver.mini++
```

## Operational Notes

- Decomposer documents constraints and success criteria before ideation.  
- Evaluator provides data or assumptions supporting each option’s feasibility.  
- Validator outlines tests, monitoring, and fallback plans for the selected solution.
