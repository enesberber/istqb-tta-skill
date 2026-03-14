---
name: statement-testing
description: Statement coverage metric calculation (executed statements / total executable statements), use as minimum baseline for all code, limitations including unreachable code and inability to detect multi-condition defects.
type: rule
chapter: "2"
bloom: K3
priority: HIGH
syllabus: TTA-2.2
---

# Statement Testing

## Definition

Statement testing is a white-box test technique that designs test cases to execute **executable statements** in the test object.

**Statement Coverage** measures the proportion of executable statements exercised:

```
Statement Coverage (%) = (Number of statements executed / Total number of executable statements) × 100
```

---

## What Counts as an Executable Statement

Executable statements include:
- Assignment statements
- Function/method calls
- Return statements
- Control flow statements (if, while, for, switch)
- Exception handling statements (throw, catch)

Non-executable statements (excluded from coverage count):
- Comments
- Blank lines
- Variable declarations (in most tools)
- Compiler directives / preprocessor macros

---

## Applying Statement Testing

### Steps
1. Obtain or construct the control flow graph of the test object
2. Identify all executable statements
3. Design test cases that collectively execute every executable statement at least once
4. Measure coverage using a coverage tool
5. Add test cases to fill gaps; accept residual if statements are unreachable

### Example

```python
def calculate_discount(price, member):   # line 1 — not executable
    discount = 0                          # line 2 — executable
    if price > 100:                       # line 3 — executable
        discount = 0.10                   # line 4 — executable
    if member:                            # line 5 — executable
        discount += 0.05                  # line 6 — executable
    return price * (1 - discount)         # line 7 — executable
```

Minimum tests for 100% statement coverage:
- Test 1: `price=150, member=True` → executes lines 2,3,4,5,6,7
- Test 2: `price=50, member=False` → executes lines 2,3,5,7

---

## Limitations

### 100% Statement Coverage Often Not Achievable
- **Unreachable code**: Dead code that no input can reach
- **Defensive code**: Error handlers for conditions that cannot occur in the current configuration
- **Platform-dependent code**: Branches compiled only on certain platforms

In practice, 100% is a goal; organizations set thresholds (e.g., 80%, 90%) based on risk.

### Statement Coverage Cannot Detect
- **Multi-condition defects**: A bug in a compound condition may not be triggered even with 100% statement coverage
- **Missing paths**: A path through the code that should exist but doesn't
- **Decision outcome defects**: Both outcomes of a decision may not be tested

### Statement Coverage vs. Decision Coverage
Statement coverage is **subsumed by** decision coverage:
- 100% decision coverage guarantees 100% statement coverage
- 100% statement coverage does NOT guarantee 100% decision coverage

---

## When to Use

- As a **minimum baseline** for all code under test
- When no stronger coverage requirement is specified
- For low-risk modules where stronger techniques are not justified
- As a starting point before applying decision or MC/DC coverage

---

## Key Points

- Coverage = executed statements ÷ total executable statements
- Weakest white-box technique; minimum acceptable baseline
- Does not detect multi-condition defects
- 100% often unachievable due to unreachable/defensive code
- Subsumed by all stronger white-box techniques
