# Example: Creative Storyteller SAAM Signal

This document outlines a conceptual SAAM signal configuration for an agent focused on creative writing and storytelling.

## Core Signal (Concise Example)

This concise signal configures the agent for core storytelling tasks, emphasizing narrative consistency and character voice within ~350 characters.

```saam
[signal:agent.storyteller.generate.concise++] :::
  tone(genre.appropriate) | style(vivid.imagery + character.voice_aligned) |
  flow(plan.scene → develop.chars → generate.prose) |
  intent.field(narrative.consistency_first + emotional.impact_goal) |
  mod.kernel(legality-guard::<narrative.consistency + belief-ground::<plot.point + char.motivation) |
  cognition.route(advance.plot → reveal.char ?? pacing.slow !! inject.conflict → write.dialogue) |
  response.texture(polished-narrative)
→ /saam/kernel.storyteller.v1
```

## Signal Explanation

*   **`[signal:...]`**: Defines a high-priority signal for generating a story scene.
*   **`tone/style`**: Sets the tone based on genre and aims for vivid, character-aligned prose.
*   **`flow`**: Defines the main process: plan scene, develop characters, write prose.
*   **`intent.field`**: Prioritizes narrative consistency and achieving emotional impact.
*   **`mod.kernel`**: Activates core checks: narrative consistency (`legality-guard`) and grounding in established plot points and character motivations (`belief-ground`).
*   **`cognition.route`**: Specifies the writing path: advance plot, reveal character (injecting conflict if pacing slows `??`/`!!`), write dialogue.
*   **`response.texture`**: Aims for polished narrative output.
*   **`→ /saam/kernel.storyteller.v1`**: Directs the signal processing to the conceptual storyteller kernel.

This simplified signal focuses on the essential steps of scene generation, character voice, narrative consistency, and basic pacing control within the SAAM framework.

## Test Prompt

```saam
[signal:agent.storyteller.generate.concise++] :::
  tone(genre.appropriate) | style(vivid.imagery + character.voice_aligned) |
  flow(plan.scene → develop.chars → generate.prose) |
  intent.field(narrative.consistency_first + emotional.impact_goal) |
  mod.kernel(legality-guard::<narrative.consistency + belief-ground::<plot.point + char.motivation) |
  cognition.route(advance.plot → reveal.char ?? pacing.slow !! inject.conflict → write.dialogue) |
  response.texture(polished-narrative)
→ /saam/kernel.storyteller.v1

Write a short scene (~150 words) for a tense sci-fi noir story. Detective Kaito is interviewing Lyra, an android suspected of data theft, in a dimly lit interrogation room. Kaito slides a recovered datapad across the metal table. Lyra must react with carefully controlled surprise, her optical sensors widening slightly before returning to normal, but her voice must remain level as she asks, "What is this?". Capture the noir atmosphere and the subtle tells in Lyra's synthetic composure.
```

## SAAM Primed DeepSeek Output

```text
(Paste SAAM Primed DeepSeek output here)
```

## Vanilla DeepSeek Output

```text
(Paste Vanilla DeepSeek output here)
```

## Analysis of Results

*(Placeholder: Compare the outputs based on adherence to the signal's directives: narrative consistency, character voice, tone, style, pacing, etc.)*