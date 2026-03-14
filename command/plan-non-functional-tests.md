---
name: plan-non-functional-tests
description: Command to plan non-functional tests for a system. Guides through quality characteristic identification, stakeholder requirements, environment planning, tool acquisition, data security, and operational profile creation. Produces a structured test plan output.
type: command
---

# Plan Non-Functional Tests

## Workflow

Follow these steps to produce a non-functional test plan for the specified system.

---

### Step 1 — Identify Quality Characteristics

Determine which quality characteristics are in scope based on the system type and stakeholder context.

| Characteristic | TTA Responsibility? | Typical Trigger |
|---|---|---|
| Security | Yes (TTA) | User data, financial transactions, access control |
| Reliability | Yes (TTA) | High availability requirements, safety systems |
| Performance Efficiency | Yes (TTA) | Response time SLAs, concurrent user targets |
| Maintainability | Yes (TTA) | Long-lived system, multiple maintenance teams |
| Portability | Yes (TTA) | Multi-platform deployment, IoT, COTS replacement |
| Coexistence (Compatibility) | Yes (TTA) | Shared server environments, OS upgrade impact |

For each selected characteristic, document:
- Why it is relevant to this system
- Who the key stakeholder is
- Initial priority (Critical / High / Medium)

---

### Step 2 — Gather Stakeholder Requirements

For each quality characteristic in scope, capture measurable acceptance criteria:

**Security**
- Authentication mechanisms required
- Data classification and protection levels
- Penetration testing scope and approval process

**Performance**
- Response time targets (specify percentile: 95th, 99th)
- Throughput targets (transactions per second)
- Concurrent user targets
- Resource utilization limits (CPU %, memory %)

**Reliability**
- Availability target (e.g., 99.9% = ~8.7 hours downtime/year)
- MTBF target
- Recovery Time Objective (RTO)
- Recovery Point Objective (RPO)

**Maintainability**
- Complexity thresholds (maximum cyclomatic complexity per function)
- Coverage targets for unit tests
- Code duplication limits

**Portability**
- Target operating systems and versions
- Target hardware configurations
- Supported runtime versions

**Coexistence**
- Other products sharing the production environment
- Shared resource allocation constraints

---

### Step 3 — Plan Test Environment

Define the test environment required for each characteristic:

| Requirement | Details |
|---|---|
| Hardware | CPU, RAM, disk, network specs relative to production |
| Software stack | OS, middleware, database, runtime versions |
| Data volume | Volume relative to production |
| Network | Topology, latency, bandwidth |
| Availability | Dedicated window; no shared workloads during testing |
| Monitoring | APM, logging, metrics collection infrastructure |
| Isolation | No other workloads sharing resources |

**Document environment gaps**: List ways the test environment differs from production and the expected impact on results.

---

### Step 4 — Acquire Tools

For each quality characteristic, identify required tools:

| Characteristic | Tool Category | Selected Tool | License/Cost | Acquisition Timeline |
|---|---|---|---|---|
| Performance | Load generator | [JMeter/Gatling/k6] | | |
| Performance | APM/monitoring | [Prometheus/Datadog] | | |
| Security | SAST | [Checkmarx/SonarQube] | | |
| Security | DAST/scanner | [OWASP ZAP/Burp] | | |
| Reliability | Fault injection | [Chaos toolkit] | | |
| Maintainability | Static analysis | [SonarQube/PMD] | | |

Acquisition lead time must be added to the test schedule.

---

### Step 5 — Address Data Security

For each data set required for non-functional testing:

| Data Type | Volume Needed | Source | Privacy Risk | Mitigation |
|---|---|---|---|---|
| User profiles | 100,000 records | Production export | HIGH — PII | Anonymize names/emails |
| Transaction history | 1M records | Production export | HIGH — financial | Mask card numbers/amounts |
| System logs | 6 months | Production | LOW | Filter credentials from logs |

Document:
- Data anonymization/masking approach and tool
- Regulatory constraints (GDPR, HIPAA, PCI-DSS) and compliance actions
- Data generation approach for records that cannot be derived from production

---

### Step 6 — Define Operational Profile

For performance and reliability testing, define the operational profile:

**User Types and Frequencies:**
| User Type | % of Traffic |
|---|---|
| [User type 1] | [%] |
| [User type 2] | [%] |

**Operations per User Type:**
| User Type | Operation | Frequency |
|---|---|---|
| [Type 1] | [Operation A] | [%] |
| [Type 1] | [Operation B] | [%] |

---

### Step 7 — Write Test Specifications

For each quality characteristic, reference the applicable rule:

| Characteristic | Rule | Test Approach |
|---|---|---|
| Security | `security-testing` | Threat-based, vector-based (UI/FS/OS/external) |
| Reliability | `reliability-testing` | MTBF measurement, fault injection, failover |
| Performance | `performance-testing` | Load test, stress test, scalability test |
| Maintainability | `maintainability-testing` | Static analysis, diagnostic output |
| Portability | `portability-testing` | Install/uninstall, cross-platform, replacement |
| Coexistence | `compatibility-testing` | Co-resident product interaction |

---

## Output Template

```
Non-Functional Test Plan
System: [system name]
Version: [version]
Date: [date]
Prepared by: [TTA name]

## In-Scope Quality Characteristics
[List with stakeholder, priority, and measurable acceptance criteria]

## Test Environment
[Hardware specs, software stack, data volume, monitoring, gaps from production]

## Tools
[Tool, purpose, license, acquisition date]

## Data Security Plan
[Data types, anonymization approach, regulatory constraints]

## Operational Profile
[User types, frequencies, operations]

## Test Schedule
[Milestone: environment ready, tool acquisition, test execution start, results review]

## Exit Criteria
[Measurable criteria for each characteristic]

## Test Specifications
[Reference to detailed test specs per characteristic]
```
