---
name: performance-testing
description: Performance efficiency testing — sub-characteristics (time behavior/response/throughput, resource utilization/CPU/memory/I-O/bandwidth, capacity/max transactions/users). Test types: load, stress (2 variants), scalability. Planning: timing, reviews, early testing, environment, costs, exit criteria, tools.
type: rule
chapter: "4"
bloom: K2
priority: HIGH
syllabus: TTA-4.4
---

# Performance Testing

## Definition

Performance efficiency testing evaluates the relationship between the system's performance and the resources used under stated conditions. It covers how fast the system responds, how efficiently it uses resources, and how much load it can handle.

---

## ISO 25010 Performance Efficiency Sub-Characteristics

### Time Behavior
How fast the system processes requests and delivers results.

| Metric | Definition |
|---|---|
| **Response time** | Time from user action to system response (end-to-end) |
| **Turnaround time** | Time to complete a batch process or job |
| **Throughput** | Number of transactions processed per unit time |

Typical targets are expressed as percentiles (e.g., "95th percentile response time < 2 seconds").

### Resource Utilization
How efficiently the system uses available resources.

| Resource | Metrics |
|---|---|
| **CPU** | % utilization, context switches |
| **Memory (RAM)** | % used, heap size, GC frequency |
| **I/O** | Disk read/write rate, I/O wait time |
| **Network bandwidth** | Data transferred per second, packet loss |

Resource utilization must stay within acceptable limits under all load conditions.

### Capacity
The maximum limits the system can handle while meeting performance criteria.

- Maximum concurrent users
- Maximum transactions per second
- Maximum data volume (database records, file sizes)
- Maximum message queue depth

---

## Performance Test Types

### Load Testing
- Apply a **realistic expected load** to the system
- Verify the system meets response time and resource targets under normal operations
- Gradually ramp up load to the expected peak, sustain it, then ramp down
- Goal: confirm the system handles the anticipated workload

### Stress Testing (Two Variants)

**Variant 1 — Beyond-Capacity Stress Testing**
- Apply load **beyond the system's designed capacity**
- Goal: determine how the system fails (gracefully or catastrophically)
- Verify recovery after overload (no data corruption, clean return to normal)

**Variant 2 — Degraded-Conditions Stress Testing**
- Run under **reduced resources** (e.g., one server node failed, reduced memory)
- Goal: verify the system can still function (possibly at reduced performance) under degraded conditions
- Used to test resilience and fault tolerance from a performance perspective

### Scalability Testing
- Determine how performance changes as load increases
- Identify the point at which performance degrades unacceptably
- Verify horizontal/vertical scaling works as expected
- Produces a scalability curve: throughput vs. concurrent users

---

## Planning Factors for Performance Testing

### Timing
- Performance tests require significant environment setup time
- Should be planned as early as possible; do not wait until the end of the project
- Performance testing at architecture/design time can prevent expensive rework

### Design and Architecture Reviews
- Review performance-critical decisions early (caching strategy, database indexing, connection pooling)
- Identify potential bottlenecks before they are implemented

### Early Testing
- Component-level performance tests can identify algorithm inefficiencies early
- Integration-level tests can identify protocol overhead and serialization costs
- Do not defer all performance testing to system test phase

### Environment
- Must be production-like (hardware specs, network topology, data volumes)
- Dedicated environment required during test runs (shared environments produce unreliable results)
- Consider cloud-based environments for elastic load generation

### Costs
- Load generation tools (commercial tools: LoadRunner, Gatling, k6; open-source: JMeter, Locust)
- Environment costs (hardware or cloud resources)
- Test data preparation (realistic data volumes)
- Skilled performance engineers

### Exit Criteria
- Define specific, measurable acceptance criteria before testing begins:
  - "95th percentile response time < X ms at Y concurrent users"
  - "CPU utilization < 80% at peak load"
  - "System handles Z transactions per second with no errors"
- Do not accept vague criteria like "performance should be acceptable"

### Tools
- **Load generators**: Apache JMeter, Gatling, Locust, k6, LoadRunner, NeoLoad
- **Monitoring/measurement**: Grafana + Prometheus, Datadog, New Relic, AppDynamics
- **Profilers**: for root cause analysis of bottlenecks

---

## Key Points

- Performance sub-characteristics: time behavior (response/turnaround/throughput), resource utilization (CPU/memory/I-O/bandwidth), capacity (max transactions/users)
- Test types: load (realistic load), stress (beyond capacity or degraded conditions), scalability (performance vs. load curve)
- Planning: start early, use production-like environment, define measurable exit criteria, acquire tools in advance
- Measure percentiles (95th, 99th) not just averages for response time
- Resource utilization limits must be defined alongside response time targets
