---
name: maintainability-testing
description: Maintainability testing — sub-characteristics (analyzability, modifiability, testability, modularity, reusability) using static and dynamic approaches. Start when design documents are available. Goal is to minimize maintenance cost and downtime.
type: rule
chapter: "4"
bloom: K2
priority: MEDIUM
syllabus: TTA-4.5
---

# Maintainability Testing

## Definition

Maintainability testing evaluates the degree to which the system can be modified by intended maintainers. A maintainable system reduces the cost and risk of corrections, adaptations, and enhancements over its lifecycle.

---

## ISO 25010 Maintainability Sub-Characteristics

### Analyzability
The degree to which a system can be diagnosed for deficiencies or causes of failure.

**What to assess:**
- Can maintainers understand the code structure without excessive effort?
- Are logs, error messages, and diagnostic outputs meaningful?
- Is the system modular enough to isolate the source of a defect?
- Is documentation current and accurate?

### Modifiability
The degree to which the system can be changed without introducing defects.

**What to assess:**
- Low coupling between modules (changes in one module don't cascade)
- High cohesion within modules (single responsibility)
- Absence of magic numbers and hard-coded values
- Meaningful variable/function/class names

### Testability
The degree to which test criteria can be established and tests run to determine if the system meets those criteria.

**What to assess:**
- Functions/methods are independently testable (no hidden global state)
- Interfaces are well-defined (dependency injection, mock-friendly)
- Cyclomatic complexity is within acceptable thresholds
- Observable outputs for given inputs

### Modularity
The degree to which the system is composed of discrete components such that changes to one have minimal impact on others.

**What to assess:**
- Clear module boundaries and interfaces
- Low inter-module dependencies
- High intra-module cohesion
- No circular dependencies

### Reusability
The degree to which an asset can be used in more than one system or in building other assets.

**What to assess:**
- Generic interfaces not tied to specific contexts
- No embedded assumptions about caller context
- Well-documented contracts (pre/post conditions)

---

## Testing Approaches

### Static Approaches
Static analysis tools measure maintainability characteristics without running the code:

- **Cyclomatic complexity**: High values indicate poor analyzability and testability
- **Coupling metrics** (afferent/efferent coupling, instability index): Low coupling = high modularity
- **Cohesion metrics**: High cohesion = good modularity and reusability
- **Code duplication**: Repeated code reduces modifiability
- **Coding standards**: Naming, commenting, formatting violations reduce analyzability
- **Dependency graphs**: Circular dependencies indicate poor modularity

Tools: SonarQube, Checkstyle, PMD, NDepend, Understand

### Dynamic Approaches
Some maintainability characteristics can only be assessed by executing the system:

- **Diagnostic output testing**: Trigger known errors and verify log messages are actionable
- **Debug mode testing**: Verify diagnostic interfaces provide useful state information
- **Change impact testing**: Make a small, isolated change and measure test re-run time
- **Test harness coverage**: Verify unit test coverage levels (a proxy for testability)

---

## When to Start

Maintainability testing should begin as soon as **design documents** are available:

| Phase | Activity |
|---|---|
| Design phase | Review architecture for modularity, coupling, cohesion |
| Implementation | Static analysis in CI/CD pipeline (coding standards, complexity) |
| Component test | Unit test coverage measurement (testability proxy) |
| System test | Dynamic diagnostic output and change impact tests |
| Acceptance | Verify maintainability criteria in acceptance criteria |

**Starting early is critical** — maintainability defects discovered late require architectural rework.

---

## Goals

- **Minimize maintenance cost**: Analyzable, modifiable code takes less time to change correctly
- **Minimize downtime**: Analyzable systems are diagnosed faster; modifiable systems are patched faster
- **Enable safe evolution**: Modular, testable systems can be changed with confidence

---

## Key Points

- Sub-characteristics: analyzability, modifiability, testability, modularity, reusability
- Static analysis (complexity, coupling, duplication) is the primary tool for maintainability testing
- Dynamic analysis assesses diagnostic outputs and change impact
- Start at design phase — architectural maintainability problems are expensive to fix late
- Goal: minimize cost and risk of maintenance over the system lifecycle
