---
name: data-flow-analysis
description: Data flow analysis tracks variable lifecycle (define/use/kill) and detects anomalous sequences (dd, dk, uk, ku). Definition-use pairs guide test case design. Limitations include dynamic data, concurrency, and array indexing.
type: rule
chapter: "3"
bloom: K3
priority: HIGH
syllabus: TTA-3.3
---

# Data Flow Analysis

## Definition

Data flow analysis is a **static analysis** technique that tracks how data values are created, used, and destroyed as they flow through a program. It identifies **anomalous sequences** in variable lifecycles that indicate potential defects.

---

## Variable Lifecycle States

Each occurrence of a variable in code is classified as:

| State | Symbol | Description | Example |
|---|---|---|---|
| **Define** | d | Variable is given a value | `x = 5` |
| **Use** | u | Variable's value is read | `y = x + 1` |
| **Kill** | k | Variable goes out of scope or is explicitly freed | End of block, `free(ptr)`, `del x` |

---

## Anomalous Sequences

Data flow analysis detects **sequences of lifecycle states** that indicate defects or dead code:

### dd — Defined then Defined (without intervening use)
```
x = 5;   // define
x = 10;  // define again — first assignment was useless
```
- The first definition is never used
- Indicates wasted computation or a missing use (the programmer forgot to use `x`)

### dk — Defined then Killed (without intervening use)
```
x = compute();  // define
// x is never used
// x goes out of scope (killed)
```
- The variable is defined but never read before being destroyed
- Indicates dead code or a missing read operation

### uk — Used then Killed (use after kill)
```
free(ptr);  // kill
y = *ptr;   // use — ptr is now invalid (wild pointer)
```
- Reading a variable after it has been freed/destroyed
- Classic wild pointer / use-after-free defect

### ku — Killed then Used (use without prior definition in scope)
```
// x not yet defined
y = x + 1;  // use before define
```
- Reading a variable before it has been given a valid value
- Results in undefined behavior (uninitialized variable)

---

## Definition-Use Pairs

A **definition-use pair** (du-pair) is a pair of:
- A **definition** of a variable at statement d
- A **use** of that variable at statement u
- Where there is a path from d to u with no intervening redefinition

Test cases are designed to execute specific du-pairs to verify correct data flow.

### Du-Path Coverage
- **All du-pairs coverage**: At least one test covers each definition-use pair
- **All du-paths coverage**: Every simple path between every du-pair is covered (stronger, often impractical)

---

## Limitations

### Dynamic Data Structures
- Arrays: analysis must determine which array element is being accessed
- Index expressions `a[i]` — static analysis cannot always determine `i` at compile time
- Pointers: tracking pointer targets requires alias analysis

### Concurrency
- Multiple threads may define or use the same variable simultaneously
- Race conditions are difficult to detect statically
- Thread-interleaved du-pairs require dynamic analysis tools (e.g., ThreadSanitizer)

### Dynamic Dispatch / Polymorphism
- In object-oriented code, the actual method called may not be known statically
- Reduces precision of data flow analysis

### External Data
- Data read from files, databases, or network is defined externally
- Static analysis tools may conservatively assume all values are possible

---

## Applying Data Flow Analysis

### Using Static Analysis Tools
Tools that perform data flow analysis include: Coverity, Polyspace, FindBugs/SpotBugs, PVS-Studio, Clang Static Analyzer.

### Steps
1. Run a data flow analysis tool on the code under test
2. Review reported anomalies (dd, dk, uk, ku sequences)
3. Classify each finding: genuine defect, dead code, or false positive
4. Fix genuine defects; document intentional patterns
5. Use du-pairs to supplement test case design

---

## Key Points

- Data flow analysis is **static** — examines variable lifecycle without execution
- States: define (d), use (u), kill (k)
- Anomalous sequences: dd (redundant define), dk (defined never used), uk (use after kill), ku (use before define)
- Definition-use pairs guide test coverage of data flow paths
- Limitations: dynamic data structures, concurrency, polymorphism, external data
- Tools automate detection; manual review determines genuine defects vs. false positives
