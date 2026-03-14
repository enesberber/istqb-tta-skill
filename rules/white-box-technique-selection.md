---
name: white-box-technique-selection
description: Selecting white-box techniques based on non-safety factors (contract, regulatory, test strategy, coding style, defect history, skills, tools) and safety factors (IEC 61508 SIL table mapping SIL 1-4 to statement/branch/MC/DC). Subsumption hierarchy guides minimum acceptable technique.
type: rule
chapter: "2"
bloom: K4
priority: CRITICAL
syllabus: TTA-2.8
---

# White-Box Technique Selection

## Selection Framework

Technique selection depends on two primary contexts:
1. **Non-safety systems** — use non-safety selection factors
2. **Safety-critical systems** — use the IEC 61508 SIL table

---

## Non-Safety Selection Factors

When safety standards do not apply, select the technique based on:

| Factor | Guidance |
|---|---|
| **Contractual requirements** | If a contract specifies a coverage technique or target, use it |
| **Customer requirements** | Some customers mandate branch or MC/DC coverage |
| **Regulatory requirements** | Industry regulations may require specific coverage levels |
| **Test strategy / policy** | Organizational standard (e.g., "all code must have 80% branch coverage") |
| **Coding style / conventions** | Simple, well-structured code → decision coverage sufficient; complex compound conditions → MC/DC |
| **Historical defects** | Previous condition-related defects → MC/DC; integration defects → API testing |
| **Available skills** | MC/DC requires training; select technique team can apply correctly |
| **Available tools** | Verify tool supports the required coverage metric before committing |

### Decision Process for Non-Safety Systems

```
Is there a contractual/regulatory/customer requirement?
├── YES → Use specified technique
└── NO  → Assess code complexity:
          Simple control flow, few conditions    → Decision/branch coverage
          Compound conditions, medium risk        → MC/DC
          Compound conditions, maximum assurance  → Multiple condition
          Minimum baseline needed                 → Statement coverage
```

---

## Safety-Critical Systems: IEC 61508 SIL Table

For systems subject to IEC 61508 (Functional Safety of Electrical/Electronic/Programmable Electronic Safety-related Systems):

| Technique | SIL 1 | SIL 2 | SIL 3 | SIL 4 |
|---|---|---|---|---|
| Statement Testing | Recommended | — | — | — |
| Branch / Decision Testing | Highly Recommended | Recommended | — | — |
| MC/DC | — | — | Recommended | Highly Recommended |

**Legend:**
- **Highly Recommended**: Strong expectation of use; requires justification if not applied
- **Recommended**: Should be used unless an alternative provides equivalent assurance
- **—**: Not specified / not sufficient for this level

### SIL Level Guidance
- **SIL 1** (lowest): Statement + branch coverage acceptable
- **SIL 2**: Branch coverage recommended; consider MC/DC for complex logic
- **SIL 3**: MC/DC recommended; branch coverage alone is insufficient
- **SIL 4** (highest): MC/DC highly recommended; branch coverage inadequate

### Other Safety Standards
| Standard | Domain | Technique |
|---|---|---|
| DO-178C Level A/B | Aerospace | MC/DC required |
| ISO 26262 ASIL D | Automotive | MC/DC recommended |
| EN 50128 SIL 3/4 | Railway | MC/DC recommended |

---

## Subsumption Hierarchy Summary

Use the hierarchy to determine the minimum acceptable technique:

```
Multiple Condition (2^N)   — exhaustive, all combinations
       ↑ subsumes
   MC/DC (N+1)             — independence of each condition
       ↑ subsumes
Decision / Branch           — all TRUE/FALSE outcomes
       ↑ subsumes
Statement                  — all executable statements
```

- Selecting a higher-level technique automatically satisfies lower-level requirements
- SIL 3 requires MC/DC → decision and statement coverage are automatically satisfied
- If time/resource constrained, apply the **highest technique feasible** for high-risk code and lower techniques for low-risk code

---

## Practical Application

### Checklist for Technique Selection

1. Check for mandatory requirements (contract, regulation, safety standard)
2. Identify SIL level if safety-related
3. Assess code complexity (number of conditions per decision, nesting depth)
4. Assess risk level (complexity, defect history, change rate)
5. Verify team skill and tool availability for selected technique
6. Document the selected technique and justification in the test plan

### Mixed-Level Application
It is valid to apply different techniques to different modules:
- High-risk/safety modules → MC/DC or Multiple Condition
- Medium-risk modules → Decision coverage
- Low-risk / utility code → Statement coverage

---

## Key Points

- Non-safety: select based on contract, regulatory, strategy, coding style, defect history, skills, tools
- Safety-critical: use IEC 61508 SIL table (SIL 3/4 → MC/DC; SIL 1/2 → branch)
- Subsumption: higher technique satisfies all lower requirements
- Mix techniques across modules to balance effort and assurance
- Document selection rationale in the test plan
