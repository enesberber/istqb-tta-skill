---
name: modified-condition-decision-testing
description: MC/DC — each atomic condition independently affects the decision outcome. Required for safety-critical systems (aerospace DO-178C, automotive IEC 61508 SIL 3/4). Minimum N+1 test cases for N conditions. Beware short-circuit evaluation.
type: rule
chapter: "2"
bloom: K3
priority: CRITICAL
syllabus: TTA-2.4
---

# Modified Condition/Decision Coverage (MC/DC)

## Definition

MC/DC requires that every atomic condition in a decision has been shown to **independently affect the outcome** of that decision.

For each atomic condition C in a compound decision:
- There must exist a pair of test cases where:
  - C changes value (TRUE→FALSE or FALSE→TRUE)
  - All other atomic conditions remain the same
  - The overall decision outcome changes

---

## Formal Requirements

MC/DC satisfies all four of:
1. **Every entry and exit point** is invoked at least once
2. **Every decision** takes every possible outcome at least once
3. **Every condition** in a decision takes every possible outcome at least once
4. **Every condition** in a decision independently affects the decision outcome

Requirements 1–3 are also satisfied by decision coverage + condition coverage. Requirement 4 is unique to MC/DC.

---

## Minimum Test Count

For a decision with **N** unique atomic conditions:
- Minimum **N + 1** test cases are required
- This is the theoretical minimum (masking MC/DC variant)
- Standard MC/DC may require up to **2N** tests

### Example: 3 Conditions → Minimum 4 Tests

```
Decision: (A and B) or C

Conditions: A, B, C  →  N = 3  →  minimum 4 tests
```

| Test | A | B | C | Outcome | Shows independence of |
|------|---|---|---|---------|----------------------|
| T1   | T | T | F | T       | —                    |
| T2   | F | T | F | F       | A (T1↔T2: A changes, outcome changes) |
| T3   | T | F | F | F       | B (T1↔T3: B changes, outcome changes) |
| T4   | T | T | T | T→T... | need C variant       |

(Exact test set depends on the expression structure.)

---

## Applying MC/DC

### Steps
1. Parse the decision into atomic conditions (smallest boolean sub-expressions)
2. For each atomic condition, find a pair of test cases that shows independence
3. Combine pairs into a minimal test set
4. Verify each pair satisfies the MC/DC independence condition
5. Measure coverage using an MC/DC-capable tool

---

## Short-Circuit Evaluation Issue

Many compilers and interpreters use **short-circuit evaluation**:
- In `A and B`: if A is FALSE, B is not evaluated
- In `A or B`: if A is TRUE, B is not evaluated

**Problem**: A test case designed to show B's independence may not actually evaluate B due to short-circuit behavior, making the MC/DC requirement unsatisfied in practice.

### Mitigation
- Confirm whether the target compiler/language uses short-circuit evaluation
- Use parentheses or restructure conditions to prevent unwanted short-circuiting
- Check with coverage tool that the condition was actually evaluated

---

## Safety-Critical Application

MC/DC is mandated or recommended by safety standards:

| Standard | Domain | Requirement |
|---|---|---|
| DO-178C Level A | Aerospace software | Required |
| DO-178C Level B | Aerospace software | Required |
| IEC 61508 SIL 3 | Functional safety | Recommended |
| IEC 61508 SIL 4 | Functional safety | Highly recommended |
| ISO 26262 ASIL D | Automotive safety | Recommended |

---

## Subsumption

MC/DC is subsumed by Multiple Condition Testing:

```
Multiple Condition (2^N) → subsumes → MC/DC → subsumes → Decision → subsumes → Statement
```

MC/DC provides strong assurance with far fewer tests than full multiple condition testing.

---

## When to Use

- Safety-critical systems with SIL 3/4 (IEC 61508) or DO-178C Level A/B
- Whenever compound decisions must be rigorously verified
- When regulatory or customer requirements specify MC/DC
- When defects in individual atomic conditions must be detectable

---

## Key Points

- Each atomic condition must **independently** affect the decision outcome
- N conditions → minimum N+1 test cases
- Subsumes decision coverage and statement coverage
- Subsumed by multiple condition testing
- Short-circuit evaluation can prevent conditions from being evaluated — verify with tools
- Mandatory for aerospace (DO-178C A/B), recommended for IEC 61508 SIL 3/4
