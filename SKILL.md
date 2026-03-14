---
name: istqb-technical-test-analyst
description: ISTQB Certified Tester Advanced Level – Technical Test Analyst (CTAL-TTA v4.0). Covers white-box test techniques (statement, decision, MC/DC, multiple condition), static and dynamic analysis, non-functional quality characteristic testing (security, reliability, performance, maintainability, portability, compatibility), risk-based testing, technical reviews, test automation architecture, and tool selection. Use for any task involving code coverage, safety-critical testing, IEC 61508 SIL levels, cyclomatic complexity, data-flow anomalies, operational profiles, or automation framework design.
---

# ISTQB Technical Test Analyst (CTAL-TTA v4.0) Skill

## Knowledge Areas

| # | Area | Syllabus Chapter | Rules |
|---|------|-----------------|-------|
| 1 | Risk-Based Testing | Ch 1 | risk-based-testing-tta |
| 2 | White-Box Techniques | Ch 2 | statement-testing, decision-testing, modified-condition-decision-testing, multiple-condition-testing, api-testing, white-box-technique-selection |
| 3 | Static & Dynamic Analysis | Ch 3 | control-flow-analysis, data-flow-analysis, static-analysis-maintainability, dynamic-analysis |
| 4 | Quality Characteristics | Ch 4 | non-functional-test-planning, security-testing, reliability-testing, performance-testing, maintainability-testing, portability-testing, compatibility-testing, operational-profiles |
| 5 | Reviews | Ch 5 | technical-reviews-tta, review-checklists |
| 6 | Test Tools & Automation | Ch 6 | test-automation-project, automation-approaches, specific-test-tools |

---

## Quick Decision Trees

### Which White-Box Technique?

```
Is the system safety-critical (aerospace, automotive, medical)?
├── YES → Check IEC 61508 SIL level:
│         SIL 1 → Statement + Branch coverage
│         SIL 2 → Branch coverage
│         SIL 3 → MC/DC (recommended)
│         SIL 4 → MC/DC (highly recommended)
└── NO  → Check applicable factors:
          Contract/regulatory requirement? → Use required technique
          Complex boolean conditions?      → MC/DC or Multiple Condition
          Simple control flow?             → Decision/Branch coverage
          Minimum baseline needed?         → Statement coverage
          All condition combos needed?     → Multiple Condition (2^N)
```

### Coverage Subsumption Hierarchy

```
Multiple Condition Testing  (strongest — 2^N combinations)
         ↑ subsumes
    MC/DC Testing           (N+1 minimum tests)
         ↑ subsumes
   Decision/Branch Testing  (all TRUE/FALSE outcomes)
         ↑ subsumes
   Statement Testing        (weakest — baseline only)
```

Higher coverage subsumes all lower levels. Choose the lowest level that satisfies your risk/safety requirement.

### Which Quality Characteristic Test?

```
Does the threat involve unauthorized access or data breach?  → security-testing
Is the concern about system uptime, MTBF, failover?         → reliability-testing
Is the concern about response time, throughput, or load?    → performance-testing
Is the concern about code structure, coupling, modifiability?→ maintainability-testing
Is the concern about install, run on multiple platforms?    → portability-testing
Is the concern about shared environment, resource conflicts? → compatibility-testing
```

### Non-Functional Test Planning

```
1. Identify quality characteristics from stakeholder requirements
2. Benchmark existing system (if available)
3. Plan production-like test environment
4. Acquire specialized tools
5. Address data security/privacy constraints
6. Write test specifications using operational profiles
```

---

## Common Patterns

### Operational Profile Usage
- Define user types and frequency of operations
- Generate pseudo-random test inputs weighted by usage frequency
- Apply to both reliability testing (MTBF estimation) and performance testing (realistic load)
- Tools can automate test case generation from profiles

### Risk-Based Technique Selection
- High technical risk (complex logic, high change rate, defect history) → stronger coverage technique
- TTA contributes probability assessment; TA contributes business impact assessment
- Risk level determines minimum coverage target and technique selection

### MC/DC Minimum Test Count
- N unique atomic conditions → minimum N+1 test cases
- Each condition must independently affect the decision outcome
- Watch for short-circuit evaluation (compiler may not evaluate all conditions)

---

## Anti-Patterns

| Anti-Pattern | Problem | Correct Approach |
|---|---|---|
| Using statement coverage for SIL 3/4 safety systems | Misses condition defects that cause catastrophic failure | Apply MC/DC per IEC 61508 SIL table |
| Skipping dynamic analysis until system test | Memory leaks and wild pointers found too late, expensive to fix | Start dynamic analysis at component/integration level |
| Ignoring non-functional test planning | Environment unavailable, tools not acquired, data privacy not addressed | Plan non-functional tests early with dedicated environment and tool budget |
| Capture/playback automation without refactoring | Brittle scripts, high maintenance burden, poor ROI | Use data-driven or keyword-driven approach; treat automation as software project |

---

## Rule Reference Index

| Rule File | Chapter | Priority | Topic |
|---|---|---|---|
| `risk-based-testing-tta` | 1 | CRITICAL | Technical risk ID, assessment, mitigation |
| `statement-testing` | 2 | HIGH | Statement coverage metric and limits |
| `decision-testing` | 2 | CRITICAL | Decision/branch coverage, subsumption |
| `modified-condition-decision-testing` | 2 | CRITICAL | MC/DC for safety-critical systems |
| `multiple-condition-testing` | 2 | HIGH | All 2^N condition combinations |
| `api-testing` | 2 | HIGH | API test types and defect classes |
| `white-box-technique-selection` | 2 | CRITICAL | Selection factors, SIL table, subsumption |
| `control-flow-analysis` | 3 | HIGH | Anomalies, cyclomatic complexity |
| `data-flow-analysis` | 3 | HIGH | Variable lifecycle, anomaly sequences |
| `static-analysis-maintainability` | 3 | MEDIUM | Standards, coupling/cohesion, structure |
| `dynamic-analysis` | 3 | HIGH | Memory leaks, wild pointers, profiling |
| `non-functional-test-planning` | 4 | CRITICAL | Planning factors, environment, benchmarking |
| `security-testing` | 4 | CRITICAL | Threats, approval, ISO 25010 sub-chars |
| `reliability-testing` | 4 | HIGH | MTBF, availability, fault tolerance |
| `performance-testing` | 4 | HIGH | Load/stress/scalability, sub-chars |
| `maintainability-testing` | 4 | MEDIUM | Static+dynamic, sub-chars |
| `portability-testing` | 4 | MEDIUM | Installability, adaptability, replaceability |
| `compatibility-testing` | 4 | MEDIUM | Coexistence, resource conflicts |
| `operational-profiles` | 4 | HIGH | Usage patterns for reliability/performance |
| `technical-reviews-tta` | 5 | HIGH | TTA viewpoint, checklists, integration plans |
| `review-checklists` | 5 | CRITICAL | Architectural and code checklist items |
| `test-automation-project` | 6 | HIGH | Automation as software project, ROI |
| `automation-approaches` | 6 | HIGH | GUI/API, capture/playback, data/keyword-driven |
| `specific-test-tools` | 6 | MEDIUM | Fault seeding/injection, perf, web, MBT, mobile |
