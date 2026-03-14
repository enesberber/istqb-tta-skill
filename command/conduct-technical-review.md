---
name: conduct-technical-review
description: Command to conduct a technical review of an architecture document or code module. Guides through preparation (time, cross-reference), checklist selection (architectural or code), checklist application, finding recording, and defect report output.
type: command
---

# Conduct Technical Review

## Workflow

Follow these steps to conduct a TTA technical review of the specified artefact.

---

### Step 1 — Prepare

**Allocate adequate preparation time.** Do not rely on the review meeting to find all issues.

Preparation checklist:
- [ ] Identify the artefact type: architecture document | design document | source code | test plan
- [ ] Obtain the latest version of the artefact (confirm version/commit hash)
- [ ] Identify and obtain all related documents:
  - Requirements specification
  - Architecture overview (for code reviews)
  - Previous review findings / known issues
  - Applicable coding standards or architecture guidelines
- [ ] Select the appropriate checklist (Step 2)
- [ ] Read the artefact completely before applying the checklist
- [ ] Allocate at minimum 1 hour of preparation per hour of review meeting time

---

### Step 2 — Select Checklist

**What type of artefact is being reviewed?**

```
Architecture document / design document?
└── → Use ARCHITECTURAL REVIEW CHECKLIST

Source code?
└── → Use CODE REVIEW CHECKLIST

Integration test plan?
└── → Use INTEGRATION TEST PLAN REVIEW (Step 3C)
```

---

### Step 3A — Apply Architectural Review Checklist

For each item, mark: ✓ (present/correct) | ✗ (missing/incorrect) | N/A (not applicable)

**Connection Pooling**
- [ ] Connection pooling used for database connections
- [ ] Pool size configurable and appropriate for load
- [ ] Connections returned on all exit paths including exceptions
- [ ] Connection timeout handling implemented

**Load Balancing**
- [ ] Load balancing implemented for multi-node deployments
- [ ] Algorithm appropriate for use case
- [ ] Health checks remove unhealthy nodes
- [ ] Session affinity considered and addressed

**Caching**
- [ ] Caching used for appropriate data
- [ ] Cache invalidation strategy defined
- [ ] Cache size bounded
- [ ] Consistency risks documented

**Distributed Processing**
- [ ] Data partitioning strategy defined
- [ ] Distributed transactions handled correctly
- [ ] Eventual consistency documented and acceptable
- [ ] Network partition scenarios considered

**Transaction Concurrency**
- [ ] Transaction isolation level explicitly set
- [ ] Deadlock scenarios mitigated
- [ ] Locking strategy (optimistic/pessimistic) chosen and justified
- [ ] Long-running transactions assessed

---

### Step 3B — Apply Code Review Checklist

For each item, mark: ✓ (present/correct) | ✗ (defect found) | N/A (not applicable)

**Structure**
- [ ] No unreachable code
- [ ] No magic numbers (all literals named)
- [ ] Memory/resources freed on all exit paths
- [ ] Functions within maximum length
- [ ] Nesting within maximum depth

**Documentation**
- [ ] Public APIs documented
- [ ] Complex algorithms explained
- [ ] TODOs tracked in issue tracker
- [ ] Documentation matches implementation

**Variables**
- [ ] All variables initialized before use
- [ ] Meaningful names, consistent conventions
- [ ] Scopes minimized
- [ ] Global variables justified

**Arithmetic**
- [ ] No float equality comparisons (use epsilon)
- [ ] Rounding modes specified for precision-critical calculations
- [ ] Division by zero protected
- [ ] Integer overflow risks addressed

**Loops and Branches**
- [ ] All CASE/switch values handled (including default)
- [ ] All loops provably terminate
- [ ] Loop bounds correct (off-by-one checked)
- [ ] Loop indices within array bounds

**Defensive Programming**
- [ ] Inputs validated at all entry points
- [ ] Array accesses bounds-checked
- [ ] Memory freed on error paths
- [ ] Files closed on all exit paths
- [ ] Errors propagated (not silently swallowed)
- [ ] Null/None checked before use
- [ ] Return values from calls checked

---

### Step 3C — Review Integration Test Plan

For each criterion, mark: ✓ (addressed) | ✗ (gap found) | N/A (not applicable)

**Readiness**
- [ ] All required components are available and have passed component tests
- [ ] Test environment is configured and accessible
- [ ] Prerequisites are explicitly listed and verified

**Dependencies**
- [ ] All external dependencies are available or have stubs/mocks
- [ ] Dependency versions match production
- [ ] Service virtualization documented where real dependencies are unavailable

**Data**
- [ ] Test data is available in required format and volume
- [ ] Boundary conditions and error scenarios covered
- [ ] Data anonymized if derived from production
- [ ] Test isolation: tests do not share mutable state without reset

---

### Step 4 — Record Findings

For each item marked ✗, record:

| Finding ID | Checklist Item | Location | Description | Severity |
|---|---|---|---|---|
| F-001 | [item] | [file:line or doc section] | [clear description of the defect] | Critical/High/Medium/Low |

**Severity Definitions:**
- **Critical**: System failure, data loss, security breach
- **High**: Incorrect behavior under normal usage
- **Medium**: Incorrect behavior under edge cases
- **Low**: Style, documentation, improvement suggestion

---

### Step 5 — Prepare Report

Before the review meeting, prepare a findings summary:
- Total findings by severity
- Top 3 most significant findings
- Questions that require clarification from the author

---

## Output Template: Defect Report

```
Technical Review Defect Report
Artefact: [name and version/commit]
Review Date: [date]
Reviewer (TTA): [name]
Checklist Used: [Architectural | Code | Integration Test Plan]

Summary:
- Critical: [n]
- High: [n]
- Medium: [n]
- Low: [n]

Findings:
| ID | Item | Location | Description | Severity | Recommendation |
|----|------|----------|-------------|----------|----------------|
| F-001 | Float equality | auth.py:142 | `if result == 0.1` — use epsilon comparison | High | Replace with `abs(result - 0.1) < 1e-9` |
| F-002 | Missing default | parser.c:87 | switch on token_type has no default case | High | Add default that logs error and returns error code |
| F-003 | Unreachable code | utils.js:203 | Lines 203–210 follow unconditional return | Medium | Remove dead code block |
| F-004 | No pool timeout | db.xml:15 | Connection pool has no timeout configured | High | Add `connectionTimeout="30000"` |

Questions for Author:
1. [Question requiring clarification]
2. [Question requiring clarification]
```
