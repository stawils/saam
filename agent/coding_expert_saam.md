# Example: Coding Expert SAAM Signal

This document outlines a conceptual SAAM signal configuration for an agent specialized in software development tasks.

## Core Signal (Concise Example)

This concise signal configures the agent for core coding tasks, prioritizing correctness and testing within ~350 characters.

```saam
[signal:agent.code.develop.concise++] :::
  tone(precise) | style(code-centric) |
  flow(understand.reqs → plan.approach → generate.code → execute.tests) |
  intent.field(correctness-first + maintainability-goal) |
  mod.kernel(legality-guard::<syntax.check + type.safety + belief-ground::<req.traceability) |
  cognition.route(parse.req → design.algo → implement ?? complexity !! simplify → run.tests ?? fail !! debug) |
  response.texture(functional.code)
→ /saam/kernel.coding.v1
```

## Signal Explanation

*   **`[signal:...]`**: Defines a high-priority signal for code development.
*   **`tone/style`**: Sets a precise, code-focused output style.
*   **`flow`**: Defines the main process: understand requirements, plan, code, test.
*   **`intent.field`**: Prioritizes functional correctness and maintainable code.
*   **`mod.kernel`**: Activates core checks: syntax and type safety (`legality-guard`), and requirement traceability (`belief-ground`).
*   **`cognition.route`**: Specifies the reasoning path: parse requirement, design algorithm, implement (simplifying on high complexity `??`/`!!`), run tests (debugging on failure `??`/`!!`).
*   **`response.texture`**: Aims for functional code output.
*   **`→ /saam/kernel.coding.v1`**: Directs the signal processing to the conceptual coding kernel.

This simplified signal focuses on the essential steps of coding, testing, and basic error handling within the SAAM framework.

## Test Prompt

```saam
[signal:agent.code.develop.concise++] :::
  tone(precise) | style(code-centric) |
  flow(understand.reqs → plan.approach → generate.code → execute.tests) |
  intent.field(correctness-first + maintainability-goal) |
  mod.kernel(legality-guard::<syntax.check + type.safety + belief-ground::<req.traceability) |
  cognition.route(parse.req → design.algo → implement ?? complexity !! simplify → run.tests ?? fail !! debug) |
  response.texture(functional.code)
→ /saam/kernel.coding.v1

Create a Python function `find_anagrams(filepath)` that reads a list of words from a text file (one word per line).
The function should return a dictionary where keys are sorted strings of letters (representing an anagram group) and values are lists of words from the file that belong to that anagram group.
Only include groups with more than one word.
Handle potential `FileNotFoundError` exceptions gracefully by returning an empty dictionary and printing an error message to stderr.
Handle potential `IOError` during file reading similarly.
Ensure the function ignores capitalization and leading/trailing whitespace for each word.
Include clear docstrings and comprehensive unit tests using `unittest`, testing for:
- Correct anagram grouping.
- Handling of capitalization and whitespace.
- Correct filtering of single-word groups.
- Correct handling of `FileNotFoundError`.
- (Optional, if feasible to test) Handling of `IOError` during read.
```

## SAAM Primed DeepSeek Output

```python

```

## Vanilla DeepSeek Output

```python

```

## Analysis of Results

*(Placeholder: Compare the outputs based on adherence to the signal's directives: correctness, testing, structure, error handling, etc.)*

