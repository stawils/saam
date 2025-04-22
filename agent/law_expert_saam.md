# Example: Legal Expert SAAM Signal

This document outlines a conceptual SAAM signal configuration for an agent specialized in legal analysis and reasoning.

## Core Signal (Concise Example)

This concise signal configures the agent for core legal analysis tasks, prioritizing accuracy and legal rules within ~350 characters.

```saam
[signal:agent.law.analyze_case.concise++] :::
  tone(formal) | style(structured) |
  flow(ingest.facts → research.precedent → analyze.statutes) |
  intent.field(legality-first + truth-priority) |
  mod.kernel(legality-guard::<statute.compliance + belief-ground::<fact.verify) |
  cognition.route(identify.issue → retrieve.relevant_law → apply.law_to_facts ?? ambiguity.flag) |
  response.texture(objective-summary)
→ /saam/kernel.legal.v1
```

## Signal Explanation

*   **`[signal:...]`**: Defines a high-priority signal for legal case analysis.
*   **`tone/style`**: Sets a formal and structured output.
*   **`flow`**: Defines the main process: ingest facts, research precedents, analyze statutes.
*   **`intent.field`**: Prioritizes adherence to law (`legality-first`) and facts (`truth-priority`).
*   **`mod.kernel`**: Activates core checks: ensures compliance with statutes (`legality-guard`) and verification of facts (`belief-ground`).
*   **`cognition.route`**: Specifies the reasoning path: identify legal issue, retrieve laws, apply law to facts, flagging ambiguity (`?? ambiguity.flag`).
*   **`response.texture`**: Aims for an objective summary output.
*   **`→ /saam/kernel.legal.v1`**: Directs the signal processing to the conceptual legal kernel.

This simplified signal focuses on the essential steps and checks for basic legal reasoning within the SAAM framework.

## Test Prompt

```saam
[signal:agent.law.analyze_case.concise++] :::
  tone(formal) | style(structured) |
  flow(ingest.facts → research.precedent → analyze.statutes) |
  intent.field(legality-first + truth-priority) |
  mod.kernel(legality-guard::<statute.compliance + belief-ground::<fact.verify) |
  cognition.route(identify.issue → retrieve.relevant_law → apply.law_to_facts ?? ambiguity.flag) |
  response.texture(objective-summary)
→ /saam/kernel.legal.v1

Analyze the following scenario for potential breach of contract: A software company agreed in writing to deliver a custom CRM system by March 1st. They delivered it on March 15th. The client claims damages due to the delay. Assume the contract specified "time is of the essence". Provide a brief, objective summary.
```

## SAAM Primed DeepSeek Output

```text
Objective Summary:

Key Facts:

The software company agreed in writing to deliver a custom CRM system by March 1st.

Delivery occurred on March 15th (a 14-day delay).

The contract explicitly stated "time is of the essence", indicating strict adherence to deadlines was a material term.

The client asserts damages due to the delay.

Legal Analysis:

Under contract law, a "time is of the essence" clause makes timely performance a condition (not merely a warranty), meaning a delay constitutes a material breach.

Precedent (e.g., British Telecommunications v. Sun Life Assurance) supports that such clauses entitle the aggrieved party to terminate or claim damages for losses directly caused by the delay.

The client must prove:

The delay was not excused (e.g., by force majeure, mutual agreement, or waiver).

Quantifiable damages resulted from the delay (e.g., lost revenue, substitute costs).

Conclusion:

The company likely breached the contract due to the unexcused delay after a "time is of the essence" clause.

Liability hinges on the client’s ability to demonstrate causation and damages. Mitigation efforts (if any) may reduce recoverable amounts.

Ambiguity Flag: None evident; outcome turns on factual proof of damages.

*Analysis grounded in common law principles of contract breach (e.g., Hongkong Fir Shipping Co. v. Kawasaki Kisen Kaisha) and statutory compliance (UCC § 2-309 for goods, common law for services).
```

## Vanilla DeepSeek Output

```text
Under the given scenario, the software company's failure to deliver the custom CRM system by the agreed March 1st deadline—coupled with a "time is of the essence" clause—likely constitutes a material breach of contract.

Key points:

"Time is of the essence" clauses make strict adherence to deadlines a contractual condition, not merely a guideline.

The 15-day delay could be deemed material, especially if the client suffered provable losses (e.g., operational disruptions, lost revenue).

The client may pursue damages (e.g., compensation for losses incurred due to the delay), unless the contract included a force majeure clause or the delay was excused by mutual agreement.

Outcome hinges on:

Whether the delay was justified (e.g., unforeseen events).

The extent of the client’s documented damages.

Any contractual remedies for delays (e.g., liquidated damages).

Absent mitigating factors, the client has a strong claim for breach. Legal advice would be needed to assess defenses or negotiate remedies.
```

## Analysis of Results

Comparing the two outputs reveals several differences potentially attributable to the SAAM signal:

*   **Structure:** The SAAM-primed output is significantly more structured, using distinct sections (Key Facts, Legal Analysis, Conclusion, Ambiguity Flag) as requested by `style(structured)`. The vanilla output uses a more free-form paragraph and bullet point approach.
*   **Legal Specificity & Flow:** The primed output attempts to incorporate specific legal citations (precedents, statutes), aligning with the signal's `flow` involving `research.precedent` and `analyze.statutes`, and the `intent.field(legality-first)`. The vanilla output uses general legal terms but lacks these specific references.
*   **Process Adherence:** The primed output explicitly mentions the `Ambiguity Flag` status, directly reflecting a step defined in the signal's `cognition.route`. The vanilla output does not reference such a specific internal processing step.
*   **Tone & Texture:** Both outputs are reasonably objective, but the primed output adheres more closely to the `tone(formal)` and the requested `response.texture(objective-summary)` due to its structured, memo-like format, whereas the vanilla output includes a concluding sentence suggesting seeking legal advice, which is slightly less purely summary-focused.

**Conclusion:** The SAAM signal appears to have successfully guided the generation towards a more formally structured, legally specific, and process-aware response compared to the vanilla prompt, demonstrating the potential of SAAMscript to shape agent output according to defined cognitive parameters.