---
name: multiple-condition-testing
description: Multiple condition testing exercises all 2^N combinations of atomic conditions. Strongest white-box technique. Used for high-risk and embedded systems. Subsumes MC/DC, decision, and statement coverage.
type: rule
chapter: "2"
bloom: K3
priority: HIGH
syllabus: TTA-2.5
---

# Multiple Condition Testing

## Definition

Multiple condition testing requires that all possible **combinations of condition values** within each compound decision are exercised at least once.

For a decision with **N** atomic conditions, the total number of combinations is:

```
Test cases required = 2^N
```

---

## Comparison with Other Coverage Levels

| Technique | Test Cases Required | Combinations Exercised |
|---|---|---|
| Statement | ≥ 1 | Not specified |
| Decision | ≥ 2 per decision | TRUE/FALSE of full decision |
| MC/DC | N + 1 minimum | Independence pairs only |
| Multiple Condition | 2^N | All combinations |

---

## Example: 3 Conditions

```
Decision: (A and B) or C
N = 3 → 2^3 = 8 test cases required
```

| Test | A | B | C | Outcome |
|------|---|---|---|---------|
| T1   | F | F | F | F       |
| T2   | F | F | T | T       |
| T3   | F | T | F | F       |
| T4   | F | T | T | T       |
| T5   | T | F | F | F       |
| T6   | T | F | T | T       |
| T7   | T | T | F | T       |
| T8   | T | T | T | T       |

All 8 combinations are required regardless of their outcome.

---

## Applying Multiple Condition Testing

### Steps
1. Identify all atomic conditions in each decision
2. Create a truth table with all 2^N combinations
3. Design one test case for each row of the truth table
4. Verify all rows are executed using a coverage tool

### Combinatorial Explosion
- 5 conditions → 32 test cases
- 10 conditions → 1024 test cases
- 20 conditions → >1 million test cases

For large N, multiple condition testing becomes **impractical**. In such cases:
- Use MC/DC (N+1 tests) as an alternative
- Apply pairwise/combinatorial testing to reduce test count while maintaining meaningful coverage
- Split complex decisions into smaller sub-decisions

---

## Subsumption

Multiple condition testing is the **strongest** white-box technique in the subsumption hierarchy:

```
Multiple Condition Testing (2^N)
         ↑ subsumes
    MC/DC Testing (N+1)
         ↑ subsumes
   Decision/Branch Testing
         ↑ subsumes
   Statement Testing
```

Achieving 100% multiple condition coverage automatically satisfies MC/DC, decision, and statement coverage.

---

## When to Use

- High-risk systems where exhaustive condition verification is required
- Embedded/real-time systems with complex boolean logic
- Safety-critical systems when required by standard (MC/DC is usually preferred due to feasibility)
- Small decisions with few conditions (N ≤ 4) where 2^N is tractable
- When all defect combinations must be detectable

---

## Practical Constraints

- Typically feasible only for N ≤ 5 conditions
- For N > 5, consider MC/DC or pairwise testing
- Tools can automatically generate truth tables and test inputs
- Short-circuit evaluation issues apply here as well (same as MC/DC)

---

## Key Points

- Requires 2^N test cases for N atomic conditions — exponential growth
- Strongest white-box coverage technique
- Subsumes MC/DC, decision, and statement coverage
- Impractical for large N — prefer MC/DC for safety-critical with many conditions
- Detects all defects in condition combinations that weaker techniques miss
