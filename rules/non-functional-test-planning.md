---
name: non-functional-test-planning
description: Planning non-functional tests — general factors (stakeholder requirements, test environment, tool acquisition, organizational constraints, data security), benchmarking the existing system, and production-like environment options.
type: rule
chapter: "4"
bloom: K4
priority: CRITICAL
syllabus: TTA-4.1
---

# Non-Functional Test Planning

## Definition

Non-functional test planning addresses **how** a system behaves (performance, security, reliability, maintainability, portability, compatibility) rather than **what** it does. Planning must occur early because non-functional testing requires specialized environments, tools, and data that take time to acquire.

---

## General Planning Factors

### Stakeholder Requirements
- Identify which quality characteristics matter to which stakeholders
- Capture specific, measurable acceptance criteria (e.g., "95th percentile response time < 2 seconds at 500 concurrent users")
- Prioritize characteristics when budget or time is limited
- Agree on exit criteria before testing begins

### Test Environment
- Non-functional testing typically requires a **production-like environment**
- Differences between test and production environments must be documented and accounted for
- Environment setup time must be factored into the schedule
- Environment availability must be planned (shared environments cause scheduling conflicts)

### Tool Acquisition
- Specialized tools are required: load generators, security scanners, profilers, reliability measurement tools
- Tool evaluation, procurement, licensing, and training take time — plan early
- Open-source vs. commercial tools: assess capabilities vs. cost
- Some tools require specific hardware or cloud resources

### Organizational Factors
- Budget approval for tools and environments
- Cross-team coordination (infrastructure, security, operations teams)
- Test data management (production data constraints, GDPR/privacy)
- Access approvals (especially for security testing)
- Change management for test environment configuration

### Data Security
- Non-functional tests often use large datasets that may contain personal data
- Production data must be anonymized/masked before use in test environments
- Regulatory requirements (GDPR, HIPAA, PCI-DSS) restrict which data can be used
- Data generation tools may be needed to create realistic volumes without using real data

---

## Benchmarking the Existing System

Before testing a new version, benchmark the existing system to establish baselines:

### Why Benchmark
- Define "good enough" performance targets based on actual current behavior
- Detect regressions: new version must perform at least as well as baseline
- Provide objective evidence for improvement claims

### What to Benchmark
- Response times for key transactions (95th and 99th percentile)
- Throughput (transactions per second)
- Resource utilization (CPU, memory, I/O) at typical and peak loads
- Error rates under normal operating conditions
- System availability and MTBF from production monitoring data

### Benchmark Procedure
1. Define the benchmark scenarios (key user journeys)
2. Run baseline tests against the existing system under controlled conditions
3. Record all metrics with timestamps and environment details
4. Store baseline results — compare every new release against them

---

## Production-Like Environment Options

Full production replication is often impractical. Common options:

| Option | Description | Trade-Off |
|---|---|---|
| Full production replica | Identical hardware, data volume, network topology | Most accurate; highest cost |
| Scaled-down replica | Same topology, smaller hardware | Lower cost; results must be extrapolated |
| Cloud-based on-demand | Spin up production-equivalent cloud infra for test duration | Flexible; cloud-specific behavior may differ |
| Staging environment | Shared environment close to production | Lower cost; scheduling conflicts with deployments |
| Production (with safeguards) | Run controlled tests in production off-peak | Highest accuracy; risk of impacting real users |

### Minimum Requirements for Valid Results
- Same software stack (OS, middleware, database version) as production
- Same or proportionally scaled data volumes
- Network topology consistent with production (same latency characteristics)
- No other test workloads sharing resources during the test run

---

## Non-Functional Test Planning Checklist

- [ ] Quality characteristics to test identified and prioritized
- [ ] Measurable acceptance criteria agreed with stakeholders
- [ ] Existing system benchmarked (if applicable)
- [ ] Test environment specified and scheduled
- [ ] Required tools identified, evaluated, and procured
- [ ] Data security and privacy requirements addressed
- [ ] Organizational approvals obtained (security testing approval, change management)
- [ ] Exit criteria defined for each non-functional characteristic
- [ ] Test schedule accounts for environment setup and tool configuration time
- [ ] Operational profiles defined for realistic load generation

---

## Key Points

- Plan non-functional testing **early** — environment and tool acquisition takes time
- Five general factors: stakeholder requirements, test environment, tool acquisition, organizational constraints, data security
- Benchmark the existing system to establish performance baselines for regression detection
- Use a production-like environment; document differences and their impact on results
- Define measurable exit criteria before testing begins
