---
name: design-white-box-tests
description: Command to design white-box test cases for a given code module. Guides the user through technique selection (safety vs. non-safety), applying the technique, measuring coverage, and filling gaps. Produces a structured test case output.
type: command
---

# Design White-Box Tests

## Workflow

Follow these steps to design white-box test cases for the specified test object.

---

### Step 1 — Identify the Test Object

Confirm:
- What is the module/function/class to be tested?
- What is the programming language and compiler?
- Is source code available for analysis?
- What is the target coverage tool?

---

### Step 2 — Check if Safety-Related

**Is this component used in a safety-critical system?**

```
Safety-critical (controls physical actuators, medical devices, aerospace, automotive)?
├── YES → What is the Safety Integrity Level (SIL)?
│         SIL 1  → Apply Statement + Branch/Decision coverage
│         SIL 2  → Apply Branch/Decision coverage (Recommended)
│         SIL 3  → Apply MC/DC (Recommended)
│         SIL 4  → Apply MC/DC (Highly Recommended)
│         (See IEC 61508 SIL table in white-box-technique-selection rule)
└── NO  → Proceed to Step 3
```

---

### Step 3 — Select Technique (Non-Safety Path)

Evaluate the following factors in order:

| Factor | Question | Action |
|---|---|---|
| Contract/Regulatory | Does a contract or regulation mandate a technique? | Use specified technique |
| Customer requirement | Has the customer requested a specific coverage level? | Use customer requirement |
| Test strategy | Does the organizational test strategy specify a technique? | Use policy |
| Code complexity | Are there compound boolean conditions (AND/OR)? | Yes → MC/DC; No → Decision |
| Risk level | Is this a high-risk module (high complexity, change rate, defect history)? | Higher risk → stronger technique |
| Skills | Can the team correctly apply the selected technique? | Verify; provide training if needed |
| Tools | Does the coverage tool support the selected technique? | Verify tool capability |

**Selected technique**: _______________

---

### Step 4 — Apply the Technique

#### For Statement Coverage
1. List all executable statements
2. Design test cases ensuring each statement is reached at least once
3. Trace each test case through the code to verify statement execution

#### For Decision/Branch Coverage
1. List all decision points (IF, WHILE, FOR, CASE)
2. For each decision, list all outcomes (TRUE/FALSE; all CASE arms)
3. Design one test case per outcome (minimize total test count)
4. Verify each decision outcome is reached by at least one test

#### For MC/DC
1. Parse each compound decision into its atomic conditions
2. For each atomic condition, identify an independence pair:
   - Pair A: condition = TRUE, all others fixed, decision = TRUE
   - Pair B: condition = FALSE, all others fixed, decision = FALSE
3. Combine pairs into a minimal test set (minimum N+1 tests for N conditions)
4. Check for short-circuit evaluation issues
5. Verify using an MC/DC-capable coverage tool

#### For Multiple Condition Testing
1. For each decision, list all N atomic conditions
2. Create a truth table with all 2^N rows
3. Design one test case per truth table row

---

### Step 5 — Measure Coverage

After executing the test cases:
1. Run coverage tool and record coverage percentage
2. Identify uncovered statements/decisions/condition pairs
3. Classify uncovered items:
   - Reachable: add test cases to cover
   - Unreachable (dead code): document and flag for removal
   - Defensive code: document and accept as residual

---

### Step 6 — Fill Gaps

For each reachable uncovered item:
1. Identify the input conditions required to reach it
2. Design a test case with those conditions
3. Verify the test case covers the target
4. Add to the test suite and re-measure coverage

Repeat until coverage target is met or remaining items are documented as unreachable.

---

## Output Template

```
Test Object: [module/function name]
Language: [language]
Technique Applied: [statement | decision | MC/DC | multiple condition]
Justification: [safety SIL level | contract | risk | strategy]
Coverage Tool: [tool name]
Coverage Target: [%]

Test Cases:
| ID | Input | Expected Output | Coverage Target |
|----|-------|----------------|-----------------|
| TC-001 | [inputs] | [outputs] | [statement/decision/condition pair] |
| TC-002 | [inputs] | [outputs] | [statement/decision/condition pair] |

Coverage Results:
- Statement coverage: [%]
- Decision coverage: [%]
- MC/DC coverage: [%] (if applicable)

Uncovered Items:
| Item | Location | Classification | Action |
|------|----------|----------------|--------|
| [item] | [line] | [reachable/unreachable/defensive] | [add test/accept/remove] |
```
