---
name: review-checklists
description: TTA review checklists — architectural checklist (connection pooling, load balancing, caching, distributed processing, transaction concurrency) and code checklist (structure, documentation, variables, arithmetic, loops/branches, defensive programming).
type: rule
chapter: "5"
bloom: K4
priority: CRITICAL
syllabus: TTA-5.x
---

# Review Checklists

## Architectural Review Checklist

Use during architecture and design reviews to verify that the system design addresses key technical quality concerns.

### Connection Pooling
- [ ] Is connection pooling used for database connections?
- [ ] Is pool size configurable and appropriate for the expected load?
- [ ] Are connections returned to the pool on all exit paths (including exceptions)?
- [ ] Is connection timeout handling implemented?

### Load Balancing
- [ ] Is load balancing implemented for multi-node deployments?
- [ ] Is the load balancing algorithm appropriate (round-robin, least-connections, IP-hash)?
- [ ] Does the load balancer perform health checks and remove unhealthy nodes?
- [ ] Is session affinity (sticky sessions) required and correctly configured?

### Caching
- [ ] Is caching used appropriately for frequently accessed, rarely changed data?
- [ ] Is cache invalidation strategy defined and correct?
- [ ] Is cache size bounded to prevent memory exhaustion?
- [ ] Are cache consistency issues identified and addressed (stale data risk)?

### Distributed Processing
- [ ] Is data partitioning strategy defined (sharding, replication)?
- [ ] Are distributed transactions handled correctly (2-phase commit, saga pattern)?
- [ ] Is eventual consistency documented and acceptable for the use case?
- [ ] Are network partition scenarios (CAP theorem) considered?

### Transaction Concurrency
- [ ] Is the transaction isolation level explicitly set and appropriate?
- [ ] Are deadlock scenarios identified and mitigation strategies defined?
- [ ] Is optimistic vs. pessimistic locking explicitly chosen and justified?
- [ ] Are long-running transactions identified and their impact assessed?

---

## Code Review Checklist

Use during code reviews to identify defects in source code before execution.

### Code Structure
- [ ] **Unreachable code**: Are there statements/branches that can never be executed? (Remove or document)
- [ ] **Magic numbers**: Are all numeric literals replaced by named constants? (`MAX_RETRIES = 3` not `3`)
- [ ] **Storage allocation**: Is memory/resource allocation matched by deallocation on all exit paths?
- [ ] **Function length**: Are functions within the agreed maximum length (e.g., 50 lines)?
- [ ] **Nesting depth**: Is nesting within the agreed maximum depth (e.g., 4 levels)?

### Documentation
- [ ] Are public APIs documented (parameters, return values, exceptions, side effects)?
- [ ] Are non-obvious algorithms explained with comments?
- [ ] Are all TODO/FIXME items tracked in the issue tracker?
- [ ] Is documentation consistent with the current implementation?

### Variables
- [ ] Are all variables initialized before first use?
- [ ] Are variable names meaningful and consistent with naming conventions?
- [ ] Are variable scopes minimized (declared in the smallest applicable scope)?
- [ ] Are global variables justified and documented?

### Arithmetic
- [ ] **Floating-point equality**: Is `==` comparison of floats avoided? (Use tolerance: `|a-b| < epsilon`)
- [ ] **Rounding**: Are rounding modes explicitly specified for financial/precision-critical calculations?
- [ ] **Integer division**: Is integer division vs. floating-point division the correct choice?
- [ ] **Division by zero**: Are potential zero divisors checked before division?
- [ ] **Overflow**: Are integer overflow risks identified and handled (especially for counters, indices)?

### Loops and Branches
- [ ] **CASE/switch completeness**: Does every switch/case statement handle all expected values?
- [ ] **Default case**: Is there a `default` case (or equivalent) with defined behavior?
- [ ] **Loop termination**: Can every loop be shown to terminate under all inputs?
- [ ] **Loop bounds**: Are loop indices within array bounds on every iteration?
- [ ] **Off-by-one**: Are loop boundaries (start, end, inclusive vs. exclusive) correct?

### Defensive Programming
- [ ] **Input validation**: Are all inputs validated at system boundaries (not just UI)?
- [ ] **Array bounds**: Are all array accesses bounds-checked?
- [ ] **Memory release**: Is all allocated memory freed on all paths (including error paths)?
- [ ] **File state**: Are files always closed on all exit paths (including exceptions)?
- [ ] **Error propagation**: Are errors propagated or logged rather than silently swallowed?
- [ ] **Null/None checks**: Are null/None references checked before use?
- [ ] **Return value checks**: Are return values from called functions checked for errors?

---

## Using These Checklists

### Application Process
1. Select the appropriate checklist (architectural for design reviews, code for code reviews)
2. Apply each item to the artefact under review during preparation
3. Record each finding with:
   - Checklist item reference
   - Location in artefact (file, line number, section)
   - Description of the issue
   - Severity (Critical/High/Medium/Low)
4. Bring documented findings to the review meeting
5. Update the checklist when new defect types are discovered

### Severity Guidelines
| Severity | Description |
|---|---|
| Critical | Defect will cause system failure, data loss, or security breach |
| High | Defect will cause incorrect behavior under normal usage |
| Medium | Defect will cause incorrect behavior under edge cases |
| Low | Style violation, documentation gap, improvement suggestion |

---

## Key Points

- Architectural checklist: connection pooling, load balancing, caching, distributed processing, transaction concurrency
- Code checklist: structure (unreachable code, magic numbers, storage), documentation, variables, arithmetic (float equality, rounding, divisors), loops/branches (CASE completeness, termination), defensive programming (bounds, memory, file state)
- Apply checklists during preparation, not during the review meeting
- Record findings with location, description, and severity
- Update checklists when new defect types are encountered
