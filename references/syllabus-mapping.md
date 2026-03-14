---
name: syllabus-mapping
description: Mapping of CTAL-TTA v4.0 syllabus sections and learning objectives to rule files and command files. Use to verify full coverage of the syllabus.
type: reference
source: ISTQB CTAL-TTA v4.0 Syllabus
---

# CTAL-TTA v4.0 Syllabus Mapping

## Coverage Status

| Status | Meaning |
|---|---|
| ✓ | Covered by a rule or command file |
| N/A | Excluded from skill (removed from v4.0 or assigned to TA syllabus) |

---

## Chapter 1 — The Technical Test Analyst's Tasks in Risk-Based Testing

| Section | Title | Bloom | Rule/Command | Status |
|---|---|---|---|---|
| TTA-1.2.1 | Risk Identification | K2 | `risk-based-testing-tta` | ✓ |
| TTA-1.2.2 | Risk Assessment | K2 | `risk-based-testing-tta` | ✓ |
| TTA-1.2.3 | Risk Mitigation | K2 | `risk-based-testing-tta` | ✓ |

---

## Chapter 2 — White-Box Test Techniques

| Section | Title | Bloom | Rule/Command | Status |
|---|---|---|---|---|
| TTA-2.2 | Statement Testing | K3 | `statement-testing` | ✓ |
| TTA-2.3 | Decision Testing | K3 | `decision-testing` | ✓ |
| TTA-2.4 | Modified Condition/Decision Coverage | K3 | `modified-condition-decision-testing` | ✓ |
| TTA-2.5 | Multiple Condition Testing | K3 | `multiple-condition-testing` | ✓ |
| TTA-2.6 | Basis Path Testing | K2 | — | N/A (removed from v4.0) |
| TTA-2.7 | API Testing | K2 | `api-testing` | ✓ |
| TTA-2.8 | Selecting a White-Box Technique | K4 | `white-box-technique-selection` | ✓ |
| — | design-white-box-tests command | — | `design-white-box-tests` | ✓ |

---

## Chapter 3 — Static and Dynamic Analysis

| Section | Title | Bloom | Rule/Command | Status |
|---|---|---|---|---|
| TTA-3.2.1 | Control Flow Analysis | K3 | `control-flow-analysis` | ✓ |
| TTA-3.2.2 | Data Flow Analysis | K3 | `data-flow-analysis` | ✓ |
| TTA-3.2.3 | Using Static Analysis for Maintainability | K3 | `static-analysis-maintainability` | ✓ |
| TTA-3.2.4 | Call Graphs | K2 | — | N/A (removed from v4.0) |
| TTA-3.3 | Dynamic Analysis | K3 | `dynamic-analysis` | ✓ |

---

## Chapter 4 — Quality Characteristics for Technical Testing

| Section | Title | Bloom | Rule/Command | TTA/TA | Status |
|---|---|---|---|---|---|
| TTA-4.1 | General Planning Issues | K4 | `non-functional-test-planning` | TTA | ✓ |
| TTA-4.1 | Operational Profiles | K2 | `operational-profiles` | TTA | ✓ |
| TTA-4.2 | Security Testing | K2 | `security-testing` | TTA | ✓ |
| TTA-4.3 | Reliability Testing | K2 | `reliability-testing` | TTA | ✓ |
| TTA-4.4 | Performance Efficiency Testing | K2 | `performance-testing` | TTA | ✓ |
| TTA-4.5 | Maintainability Testing | K2 | `maintainability-testing` | TTA | ✓ |
| TTA-4.6 | Portability Testing | K2 | `portability-testing` | TTA | ✓ |
| TTA-4.7 | Compatibility Testing (Coexistence) | K2 | `compatibility-testing` | TTA | ✓ |
| — | Usability Testing | K2 | — | TA | N/A (TA syllabus) |
| — | Functional Suitability | K2 | — | TA | N/A (TA syllabus) |
| — | Interoperability | K2 | — | TA | N/A (TA syllabus) |
| — | plan-non-functional-tests command | — | `plan-non-functional-tests` | TTA | ✓ |

---

## Chapter 5 — Reviews

| Section | Title | Bloom | Rule/Command | Status |
|---|---|---|---|---|
| TTA-5.x | TTA Role in Reviews | K2 | `technical-reviews-tta` | ✓ |
| TTA-5.x | Using Checklists in Reviews | K4 | `review-checklists` | ✓ |
| — | conduct-technical-review command | — | `conduct-technical-review` | ✓ |

---

## Chapter 6 — Test Tools and Test Automation

| Section | Title | Bloom | Rule/Command | Status |
|---|---|---|---|---|
| TTA-6.1 | Defining the Test Automation Project | K2 | `test-automation-project` | ✓ |
| TTA-6.2 | Specific Test Approaches for Test Automation | K3 | `automation-approaches` | ✓ |
| TTA-6.3 | Specific Types of Test Tools | K2 | `specific-test-tools` | ✓ |

---

## ISO 25010 Quality Characteristics — TTA vs TA Assignment

Per the CTAL-TTA v4.0 syllabus (p.28 table):

| Quality Characteristic | Sub-Characteristic | Syllabus |
|---|---|---|
| Security | All sub-chars | TTA |
| Reliability | Maturity, Availability, Fault Tolerance, Recoverability | TTA |
| Performance Efficiency | Time Behavior, Resource Utilization, Capacity | TTA |
| Maintainability | All sub-chars | TTA |
| Portability | Installability, Adaptability, Replaceability | TTA |
| Compatibility | Coexistence | TTA |
| Compatibility | Interoperability | TA |
| Usability | All sub-chars | TA |
| Functional Suitability | All sub-chars | TA |

---

## File Count Verification

| Category | Count |
|---|---|
| SKILL.md | 1 |
| rules/ | 24 |
| command/ | 3 |
| references/ | 2 |
| **Total** | **30** |

### rules/ (24 files)
1. risk-based-testing-tta.md
2. statement-testing.md
3. decision-testing.md
4. modified-condition-decision-testing.md
5. multiple-condition-testing.md
6. api-testing.md
7. white-box-technique-selection.md
8. control-flow-analysis.md
9. data-flow-analysis.md
10. static-analysis-maintainability.md
11. dynamic-analysis.md
12. non-functional-test-planning.md
13. security-testing.md
14. reliability-testing.md
15. performance-testing.md
16. maintainability-testing.md
17. portability-testing.md
18. compatibility-testing.md
19. operational-profiles.md
20. technical-reviews-tta.md
21. review-checklists.md
22. test-automation-project.md
23. automation-approaches.md
24. specific-test-tools.md

### command/ (3 files)
1. design-white-box-tests.md
2. plan-non-functional-tests.md
3. conduct-technical-review.md

### references/ (2 files)
1. glossary.md
2. syllabus-mapping.md
