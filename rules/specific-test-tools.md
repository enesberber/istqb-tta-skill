---
name: specific-test-tools
description: Specific test tool categories — fault seeding (modify code to check test quality), fault injection (incorrect inputs for error handling). Performance tools (load generation, measurement/monitoring). Web tools (hyperlink checker, HTML/XML validator, CSS checker, security scanners). MBT, component/build, and mobile tools (simulators vs emulators).
type: rule
chapter: "6"
bloom: K2
priority: MEDIUM
syllabus: TTA-6.3
---

# Specific Test Tools

## Fault Seeding Tools

**Purpose**: Assess the quality of an existing test suite by measuring how many artificially introduced defects the tests can detect.

### How It Works
1. Automatically modify (mutate) the production code to introduce a **fault seed** (e.g., change `>` to `>=`, replace `+` with `-`)
2. Run the existing test suite against the mutated code
3. If the test suite detects the mutation (at least one test fails): mutation **killed** ✓
4. If all tests pass despite the mutation: mutation **survived** ✗
5. Mutation score = Killed / (Killed + Survived)

### What It Reveals
- Test suite gaps: surviving mutations indicate code paths not adequately tested
- Test effectiveness: higher mutation score → better test quality
- Not a substitute for test design — reveals where to add tests

### Tools
- PIT (PITest) for Java
- mutmut for Python
- Stryker for JavaScript/TypeScript/.NET

---

## Fault Injection Tools

**Purpose**: Test error handling by introducing **incorrect inputs or runtime faults** into the system during execution.

### How It Works
- **Input-level injection**: Send malformed data, invalid parameters, out-of-range values
- **Protocol-level injection**: Corrupt network packets, simulate timeouts, drop messages
- **Hardware-level injection**: Simulate hardware failures (disk error, memory bit flip)
- **OS-level injection**: Kill processes, exhaust file descriptors, fill disk

### What It Tests
- Error detection and propagation: does the system detect the fault?
- Error handling: does the system respond gracefully rather than crashing?
- Recovery: does the system return to a correct state after the injected fault?

### Tools
- Chaos Monkey / Chaos Engineering tools (Netflix, Gremlin)
- BFT (Byzantine Fault Tolerant) test frameworks
- Hardware-in-loop (HIL) fault injection for embedded systems

---

## Performance Testing Tools

### Load Generation
Generate concurrent users/transactions to simulate production load:
- Apache JMeter (open-source, Java)
- Gatling (open-source, Scala/Kotlin DSL)
- Locust (open-source, Python)
- k6 (open-source, JavaScript)
- NeoLoad, LoadRunner, BlazeMeter (commercial)

### Measurement and Monitoring
Measure system response and resource utilization during load:
- Grafana + Prometheus (metrics collection and visualization)
- Datadog, New Relic, Dynatrace (APM — Application Performance Monitoring)
- JVM Flight Recorder / VisualVM (JVM profiling)
- perf, gprof (Linux profiling)
- py-spy (Python profiling)

---

## Web Testing Tools

### Hyperlink Checker
- Crawls website and verifies all hyperlinks resolve correctly
- Detects: 404 errors, broken internal links, broken external links
- Tools: W3C Link Checker, Screaming Frog, Broken Link Checker

### HTML/XML Validator
- Verifies markup conforms to the HTML/XML specification
- Detects: unclosed tags, invalid attributes, malformed structure
- Tools: W3C Markup Validation Service, HTMLHint, xmllint

### CSS Checker
- Verifies CSS conforms to CSS specifications
- Detects: invalid properties, browser compatibility issues, unused rules
- Tools: W3C CSS Validation Service, Stylelint

### Security Scanners
- Automated web application security assessment
- Detects: XSS vulnerabilities, SQL injection, CSRF, insecure headers, outdated libraries
- Tools: OWASP ZAP (open-source), Burp Suite (commercial), Nikto, Nessus

---

## Model-Based Testing (MBT) Tools

**Purpose**: Generate test cases automatically from a formal model of the system's behavior.

### Common Model Types
- **Finite State Machine (FSM)**: States and transitions; tools generate paths through the state space
- **Executable UML / activity diagrams**: Model system behavior; auto-generate tests
- **Decision tables**: Auto-generate test cases from rules

### Benefits
- Systematic test generation covering all modeled paths
- Easy to update: change the model → new tests generated automatically
- Coverage metrics on the model (state coverage, transition coverage)

### Tools
- Conformiq, GraphWalker, OSMO, Spec Explorer, ModelJUnit

---

## Component and Build Tools

### xUnit Frameworks
Unit test frameworks for all major languages:
- JUnit (Java), NUnit/.NET xUnit (C#), pytest (Python), Jest (JavaScript), GoogleTest (C++)

### CI/CD Build Integration
- Trigger test execution on code commit
- Tools: Jenkins, GitHub Actions, GitLab CI, Azure DevOps, CircleCI

---

## Mobile Testing Tools

### Simulators
- Software-only simulation of a mobile device
- Runs on the development machine without physical hardware
- **Faster to set up**; good for functional testing during development
- **Less accurate**: does not simulate real hardware behavior (sensors, battery, network chips)
- Platform: iOS Simulator (Xcode)

### Emulators
- More faithful reproduction of the target device hardware and software stack
- Typically slower than simulators but more accurate
- **More realistic**: emulates hardware components (camera, GPS, accelerometer)
- Platform: Android Emulator (Android Studio / AVD)

| Aspect | Simulator | Emulator |
|---|---|---|
| Accuracy | Lower (software only) | Higher (hardware emulation) |
| Speed | Faster | Slower |
| Platform | iOS (typically) | Android (typically) |
| Use case | Rapid dev/debug | Realistic behavior testing |
| Hardware features | Limited simulation | More faithfully emulated |

---

## Key Points

- **Fault seeding**: mutate code → run tests → measure mutation score (test quality)
- **Fault injection**: inject faults at runtime → verify error handling and recovery
- **Performance tools**: load generators (JMeter/Gatling/Locust) + monitoring (Grafana/Prometheus/APM)
- **Web tools**: hyperlink checker, HTML/XML validator, CSS checker, security scanner
- **MBT tools**: generate tests from FSM or executable models automatically
- **Component/build**: xUnit frameworks + CI/CD integration
- **Mobile**: simulators (faster, less accurate — iOS) vs. emulators (slower, more accurate — Android)
