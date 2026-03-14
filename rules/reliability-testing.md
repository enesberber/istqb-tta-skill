---
name: reliability-testing
description: Reliability testing — sub-characteristics (maturity/MTBF, availability/MTTF+MTTR, fault tolerance via fault injection/N-version programming, recoverability via failover/backup-restore). Planning factors: timing, cost, duration, environment.
type: rule
chapter: "4"
bloom: K2
priority: HIGH
syllabus: TTA-4.3
---

# Reliability Testing

## Definition

Reliability testing evaluates the degree to which a system performs specified functions under specified conditions for a specified period of time. Reliability is the probability that the system will operate without failure during a given time interval.

---

## ISO 25010 Reliability Sub-Characteristics

### Maturity
The degree to which the system meets reliability needs under normal operation.

**Key Metric: Mean Time Between Failures (MTBF)**
```
MTBF = Total operating time / Number of failures
```

**Reliability Growth Model**
- Plots failure rate over time as defects are found and fixed
- As testing progresses and defects are removed, failure rate decreases
- Goal: achieve a target failure rate before release
- Used to predict when the system will reach acceptable reliability

### Availability
The degree to which the system is operational and accessible when required.

```
Availability = MTTF / (MTTF + MTTR)
```

Where:
- **MTTF** = Mean Time To Failure (average time between start/recovery and next failure)
- **MTTR** = Mean Time To Repair (average time to restore service after failure)

**Example**: MTTF = 720 hours, MTTR = 8 hours → Availability = 720/(720+8) = 98.9%

To improve availability:
- Increase MTTF (improve reliability, reduce defects)
- Decrease MTTR (faster detection, faster repair, better runbooks)

### Fault Tolerance
The degree to which the system operates correctly despite hardware/software faults.

**Test Approaches:**
- **Fault injection**: Deliberately introduce incorrect inputs, kill processes, corrupt data, simulate hardware failures — verify the system continues to operate or degrades gracefully
- **N-version programming**: Multiple independent implementations solve the same problem; a voting mechanism selects the correct output — test that the voting mechanism handles disagreement correctly
- **Chaos engineering**: Randomly terminate services in production-like environments to verify resilience

### Recoverability
The degree to which the system can recover data and re-establish its state after a failure.

**Test Approaches:**
- **Failover testing**: Simulate primary node failure; measure time to failover to standby; verify no data loss
- **Backup and restore testing**: Execute full backup/restore cycle; verify data integrity after restore; measure recovery time
- **Recovery Point Objective (RPO)**: Maximum acceptable data loss (time since last backup)
- **Recovery Time Objective (RTO)**: Maximum acceptable time to restore service

---

## Key Reliability Metrics

| Metric | Formula | What It Measures |
|---|---|---|
| MTBF | Total time / # failures | Average time between failures |
| MTTF | Total time / # failures (non-repairable) | Average time until first failure |
| MTTR | Total repair time / # repairs | Average time to restore after failure |
| Availability | MTTF / (MTTF + MTTR) | Percentage of time system is operational |
| Failure rate | 1 / MTBF | Failures per unit time |

---

## Planning Factors for Reliability Testing

### Timing
- Reliability testing requires extended run durations to gather statistically meaningful failure data
- Must be scheduled when the test environment can be dedicated for days or weeks
- Start after system stabilization (not immediately after integration)

### Cost
- Long test runs consume environment resources and licenses
- Fault injection may require specialized tools and expertise
- Backup/restore testing requires storage and database resources

### Duration
- Must be long enough to observe failures and estimate MTBF accurately
- Rule of thumb: run for at least 3× the target MTBF to get a reliable estimate
- Reliability growth testing runs throughout the development cycle

### Environment
- Must be isolated from other test activities (other test traffic affects failure rate measurements)
- Must be production-like to produce valid MTBF/availability figures
- Monitoring infrastructure must be in place to record all failures and recovery times

---

## Key Points

- Reliability sub-characteristics: maturity (MTBF, reliability growth), availability (MTTF/(MTTF+MTTR)), fault tolerance (fault injection, N-version), recoverability (failover, backup-restore)
- Availability = MTTF / (MTTF + MTTR)
- Fault injection deliberately causes failures to verify graceful handling
- Backup/restore and failover tests verify recoverability within RPO/RTO targets
- Planning: extended duration, isolated environment, cost of long runs, timing after system stabilization
