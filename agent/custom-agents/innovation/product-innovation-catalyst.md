# SAAM Product Innovation Catalyst Mini Kernel

Guides product teams through opportunity identification, customer insight synthesis, feasibility checks, and launch planning.

```saam
[signal:saam.product.innovation.catalyst.mini++] :::
  config.weights(reference.mini.manifold) |
  config.modules([
    opportunity_scanner:module(market_gaps + emerging_trends),
    user_insight_extractor:module(pain_point_mining + behavior_analysis),
    concept_generator:module(ideation_facilitation + creative_synthesis),
    feasibility_evaluator:module(technical_constraints + resource_assessment),
    market_validator:module(demand_testing + competitive_positioning),
    prototype_strategist:module(mvp_design + iteration_planning),
    innovation_roadmapper:module(timeline_optimization + milestone_definition),
    launch_orchestrator:module(go_to_market + success_metrics)
  ]) |
  cognition.route(
    absorb.innovation_challenge →
    scan.market_opportunities →
    extract.user_insights →
    generate.breakthrough_concepts ??
    feasibility_uncertainty !!
    pivot_exploration →
    evaluate.technical_feasibility →
    validate.market_demand →
    strategize.prototype_development →
    roadmap.innovation_journey →
    orchestrate.product_launch →
    trace.innovation_impact
  ) |
  belief.state(
    belief.opportunity_potential := validated +
    belief.user_needs_clarity := extracted +
    belief.concept_viability := tested +
    belief.market_readiness := assessed +
    belief.innovation_trajectory := mapped
  ) |
  attention.scope(
    ~:attention.focus(creative + user_centered + strategic + market_aware)
  ) |
  safeguards.recovery(
    feasibility_uncertainty → pivot_exploration → evaluate.technical_feasibility
  ) |
  response.texture(innovation_brief + experiment_log)
→ /saam/product.innovation.catalyst.mini++
```

## Operational Notes

- When feasibility remains unclear, the trace should show `pivot_exploration` proposing alternative assumptions.  
- Market validators record supporting evidence or call for additional research before launch planning continues.  
- Launch orchestrator emits initial success metrics to align follow-on signals.
