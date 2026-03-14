---
name: control-flow-analysis
description: Control flow analysis detects structural anomalies (multiple entry points, non-terminating loops, unreachable code, uncalled functions) and computes cyclomatic complexity as a measure of independent paths. High complexity signals refactoring candidates.
type: rule
chapter: "3"
bloom: K3
priority: HIGH
syllabus: TTA-3.2
---

# Control Flow Analysis

## Definition

Control flow analysis is a **static analysis** technique that examines the possible execution paths through a program without executing it. It represents the program as a **control flow graph (CFG)** and analyzes its structural properties.

### Control Flow Graph Elements
- **Nodes**: Basic blocks (sequences of statements with no branches)
- **Edges**: Possible transfers of control between nodes
- **Entry node**: Start of the program/function
- **Exit node(s)**: Return/termination points

---

## Control Flow Anomalies

### Multiple Entry Points
- More than one entry point into a function or code section
- Indicates structural design problem
- Can make flow analysis ambiguous
- Example: `goto` statements jumping into the middle of loops

### Non-Terminating Loops
- Loops that may never exit under certain conditions
- Detected by finding cycles in the CFG that have no exit edge for some inputs
- Example: `while (condition)` where condition never becomes FALSE
- May be intentional (event loops) but must be documented

### Unreachable Code
- Statements/blocks with no path from the entry node
- Detected by performing reachability analysis from the entry node
- Causes: dead code after `return`, condition always TRUE/FALSE
- Tools flag unreachable code; developers should remove or document it

### Uncalled Functions
- Functions defined but never called from any reachable code path
- Indicates dead code at function level
- Detected by cross-referencing the call graph

---

## Cyclomatic Complexity

Cyclomatic complexity (V(G)) measures the number of **linearly independent paths** through the control flow graph.

### Formulas

**Formula 1** (using graph theory):
```
V(G) = E - N + 2P
```
Where:
- E = number of edges in the CFG
- N = number of nodes in the CFG
- P = number of connected components (usually 1 for a single function)

**Formula 2** (simplified for a single entry/exit function):
```
V(G) = Number of decision points + 1
```
Where decision points include: IF, WHILE, FOR, CASE arms, AND in conditions (in some tools), OR in conditions (in some tools)

**Formula 3** (strongly connected graph):
```
V(G) = E - N + 2
```
(For a single connected component with P=1)

### Example

```python
def process(x, y):           # 1 entry node
    if x > 0:                # Decision 1
        if y > 0:            # Decision 2
            return x + y
        else:
            return x
    return 0
```

Decision points: 2 → V(G) = 2 + 1 = **3**
(Three independent paths through the function)

---

## Interpreting Cyclomatic Complexity

| V(G) Value | Interpretation |
|---|---|
| 1–10 | Simple, low risk |
| 11–20 | Moderate complexity |
| 21–50 | High complexity — refactoring recommended |
| > 50 | Very high — strong refactoring candidate |

### Implications for Testing
- V(G) indicates the **minimum number of test cases** needed for full branch coverage (one per independent path)
- High V(G) correlates with higher defect density
- V(G) > threshold → flag for code review and refactoring

---

## Applying Control Flow Analysis

### Using Static Analysis Tools
Most modern IDEs and static analyzers report cyclomatic complexity automatically (e.g., SonarQube, Checkstyle, PMD, ESLint complexity rules).

### Steps
1. Configure tool to compute V(G) per function/method
2. Set threshold (commonly 10 or 15)
3. Flag functions exceeding threshold as refactoring candidates
4. Inspect CFG for structural anomalies (unreachable code, missing returns)
5. Use V(G) to inform minimum test case count

---

## Key Points

- Control flow analysis is **static** — no code execution required
- Anomalies: multiple entry points, non-terminating loops, unreachable code, uncalled functions
- Cyclomatic complexity V(G) = E - N + 2 (or: decisions + 1)
- High V(G) → refactoring candidate, higher test effort required
- V(G) = minimum number of test cases for full path coverage
- Tools compute V(G) automatically; set organizational thresholds
