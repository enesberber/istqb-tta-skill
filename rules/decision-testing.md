---
name: decision-testing
description: Decision (branch) coverage — exercising all TRUE/FALSE outcomes of every decision in IF/LOOP/CASE constructs. Subsumes statement coverage. Cannot detect multi-condition defects. Coverage = decision outcomes exercised / total outcomes.
type: rule
chapter: "2"
bloom: K3
priority: CRITICAL
syllabus: TTA-2.3
---

# Decision Testing

## Definition

Decision testing (also called **branch testing**) designs test cases to exercise all possible **decision outcomes** — TRUE and FALSE — for every decision point in the test object.

**Decision Coverage** measures:

```
Decision Coverage (%) = (Decision outcomes exercised / Total possible decision outcomes) × 100
```

For each decision (IF, WHILE, FOR, CASE/SWITCH), there are at minimum 2 outcomes:
- TRUE (condition holds)
- FALSE (condition does not hold)

---

## Decision Points and Their Outcomes

| Construct | Decision Outcomes |
|---|---|
| `if (condition)` | TRUE, FALSE |
| `while (condition)` | TRUE (loop entered), FALSE (loop not entered) |
| `for (init; condition; step)` | TRUE (loop body executed), FALSE (zero iterations) |
| `switch / case` | Each case label + default |
| Ternary `cond ? a : b` | TRUE (a selected), FALSE (b selected) |

---

## Relationship to Branch Coverage

**Decision coverage and branch coverage are interchangeable** in the ISTQB context.
- A "branch" is the edge in the control flow graph connecting two nodes
- A "decision outcome" maps directly to a branch taken or not taken
- Both terms appear in tools and literature; treat them as synonyms

---

## Subsumption

Decision coverage **subsumes** statement coverage:

```
Decision Coverage → guarantees → Statement Coverage
Statement Coverage → does NOT guarantee → Decision Coverage
```

Achieving 100% decision coverage automatically achieves 100% statement coverage (all branches taken means all statements executed, assuming no unreachable code).

---

## Applying Decision Testing

### Steps
1. Identify all decision points in the test object
2. List all outcomes for each decision (TRUE/FALSE; all CASE arms)
3. Design test cases to exercise each outcome at least once
4. Measure coverage; add tests to cover missed outcomes

### Minimum Test Count
For a function with N independent binary decisions: minimum **N+1** test cases are often sufficient (though the exact number depends on structure).

### Example

```python
def classify(score, bonus):
    if score >= 60:          # Decision A
        result = "Pass"
    else:
        result = "Fail"
    if bonus:                # Decision B
        result += "+"
    return result
```

Decisions: A (score >= 60: TRUE/FALSE), B (bonus: TRUE/FALSE)
- Test 1: `score=70, bonus=True`  → A=TRUE, B=TRUE
- Test 2: `score=50, bonus=False` → A=FALSE, B=FALSE

Both decisions fully covered with 2 tests.

---

## Limitations

### Cannot Detect Multi-Condition Defects

If a decision involves compound conditions (AND, OR), decision coverage only requires that the overall decision evaluates to TRUE and FALSE. It does not require every atomic condition to be evaluated independently.

```python
if (a > 0 and b > 0):  # Decision with 2 atomic conditions
    ...
```

Decision testing requires:
- Case where `(a > 0 and b > 0)` = TRUE
- Case where `(a > 0 and b > 0)` = FALSE

But it does NOT verify whether a defect in `b > 0` alone causes a failure.
→ For compound conditions, use **MC/DC** or **Multiple Condition Testing**.

---

## When to Use

- As the standard minimum for general software development
- When contract, customer, or regulatory requirements specify branch coverage
- When coding standards mandate decision coverage
- Preferred over statement coverage for all non-trivial test objects

---

## Key Points

- Coverage = decision outcomes exercised ÷ total decision outcomes
- Each IF/WHILE/FOR/CASE has at minimum TRUE and FALSE outcomes
- Branch coverage and decision coverage are interchangeable terms
- Subsumes statement coverage
- Does NOT subsume MC/DC or multiple condition coverage
- Cannot detect defects in individual atomic conditions of compound decisions
