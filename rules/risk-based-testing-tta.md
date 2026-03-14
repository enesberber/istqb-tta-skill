---
name: risk-based-testing-tta
description: TTA-specific risk-based testing covering technical product risk identification (complexity, code change rate, defect history), risk assessment where TTA contributes likelihood and TA contributes business impact, and mitigation by designing test cases targeting high-risk areas.
type: rule
chapter: "1"
bloom: K2
priority: CRITICAL
syllabus: TTA-1.x
---

# Risk-Based Testing — Technical Test Analyst Perspective

## TTA Role in Risk-Based Testing

The Technical Test Analyst (TTA) focuses on **technical product risks** — risks arising from the internal quality and structure of the software under test. This differs from the Test Analyst (TA) role, which focuses on functional risks and business impact.

### Division of Responsibilities

| Activity | TTA Responsibility | TA Responsibility |
|---|---|---|
| Risk Identification | Technical risks | Functional/business risks |
| Risk Assessment | Likelihood (probability) | Business impact |
| Risk Mitigation | Technical test design | Functional test design |

---

## Technical Product Risk Identification

The TTA identifies risks related to:

### Structural Complexity
- High cyclomatic complexity (many independent paths)
- Deep inheritance hierarchies
- High fan-in / fan-out coupling
- Large number of parameters or global variables

### Code Change Rate
- Frequently modified modules (churn metrics from version control)
- Recently refactored code without corresponding test updates
- Code with many contributors (integration risk)

### Defect History
- Modules with historically high defect density
- Areas with recurring defect types (e.g., memory, concurrency)
- Components that caused production incidents

### Additional Technical Risk Factors
- New or unfamiliar technology
- Third-party or COTS components with limited test access
- Components with real-time or timing constraints
- Security-sensitive components (authentication, cryptography)
- Safety-critical components (failure causes physical harm)

---

## Risk Assessment

Risk level is typically expressed as:

```
Risk Level = Likelihood × Business Impact
```

- **TTA contributes**: Likelihood estimate based on technical factors (complexity, change rate, defect history)
- **TA contributes**: Business impact estimate based on operational consequence to end users

### Likelihood Assessment Factors (TTA)
- Cyclomatic complexity score
- Number of recent changes
- Historical defect count in component
- Technical novelty
- Interface complexity

---

## Risk Mitigation

For high-risk areas, the TTA designs test cases to reduce residual risk:

### Technique Selection Based on Risk
- High risk + simple logic → Decision/branch coverage
- High risk + complex conditions → MC/DC
- High risk + safety-critical → MC/DC or Multiple Condition per SIL table
- High risk + integration point → API testing, call graph analysis

### Coverage Targets
- Higher risk → higher coverage target (e.g., 100% branch coverage)
- Lower risk → minimum coverage (e.g., 80% statement coverage)
- Risk level determines the test thoroughness required

### Prioritization
- Allocate more test effort to high-risk areas
- Run high-risk tests earlier in the test cycle
- Revisit risk assessment when code changes occur

---

## Key Points

- TTA focuses on **technical** product risks, not functional or business risks
- The TTA is responsible for the **likelihood** dimension of risk; TA handles **impact**
- Technical risks include: complexity, code change rate, and defect history
- Risk level directly drives technique selection and coverage targets
- Risk assessment should be revisited when the codebase changes significantly
