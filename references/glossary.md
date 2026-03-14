---
name: glossary
description: ISTQB Glossary v4.7 terms relevant to the Technical Test Analyst — white-box techniques, static/dynamic analysis, quality characteristics, and test tools.
type: reference
source: ISTQB Glossary v4.7
---

# ISTQB TTA Glossary

Terms from ISTQB Glossary v4.7 relevant to the Technical Test Analyst (CTAL-TTA v4.0).

---

## White-Box Test Techniques

**white-box test technique**
A test technique based on analysis of the internal structure of the test object.

**statement testing**
A white-box test technique in which test cases are designed to execute statements.

**statement coverage**
The coverage of executable statements achieved by a test suite, expressed as a percentage of the total number of executable statements.

**decision testing**
A white-box test technique in which test cases are designed to exercise decision outcomes.

**decision coverage**
The coverage of decision outcomes achieved by a test suite, expressed as a percentage of the total number of decision outcomes.

**branch testing**
A white-box test technique in which test cases are designed to exercise branches. Synonym: decision testing.

**modified condition/decision coverage (MC/DC)**
The coverage of all unique single condition changes that result in a change in decision outcomes, achieved by a test suite, expressed as a percentage of the total number of unique single condition changes.

**atomic condition**
A condition that does not contain a logical operator. The smallest testable unit within a compound decision.

**multiple condition testing**
A white-box test technique in which test cases are designed to exercise all combinations of all atomic condition values within a decision.

**API testing**
A type of testing in which the test items are application programming interfaces (APIs). May be applied at component, integration, or system test level.

---

## Static and Dynamic Analysis

**control flow analysis**
A form of static analysis based on the control flow graph of the test object. Used to detect structural anomalies and compute cyclomatic complexity.

**cyclomatic complexity**
The number of independent paths through a graph. For a control flow graph: V(G) = E - N + 2P. A measure of the complexity of a program's control flow.

**data flow analysis**
A form of static analysis based on the definition and use of variables in the test object.

**definition-use pair**
An association of a definition of a variable with a use of that variable in the test object, with no redefinition of the variable on any path from the definition to the use.

**dynamic analysis**
The process of evaluating a test object based on its behavior during execution.

**memory leak**
A fault in memory management in which a computer program does not release memory that is no longer needed. Results in progressively worsening performance over time.

**wild pointer**
A pointer that references a memory location that is no longer validly allocated or has never been initialized. Also: dangling pointer, stale pointer.

---

## Quality Characteristics (ISO 25010)

**availability**
The degree to which a component or system is operational and accessible when required for use.
Formula: MTTF / (MTTF + MTTR)

**maturity**
Sub-characteristic of reliability. The degree to which a system meets reliability needs under normal operation. Key metric: MTBF.

**fault tolerance**
The degree to which a system operates as intended despite the presence of hardware or software faults.

**recoverability**
The degree to which a system can recover data directly affected and re-establish the desired state of the system in the case of an interruption or failure.

**mean time between failures (MTBF)**
The average time between consecutive failures of a component or system. MTBF = total operating time / number of failures.

**mean time to repair (MTTR)**
The average time to restore a component or system from a failure to its defined operational state.

**mean time to failure (MTTF)**
The average time from the start of operation or repair to the next failure of a component or system (for non-repairable items).

**performance efficiency**
ISO 25010 quality characteristic. The performance relative to the amount of resources used under stated conditions. Sub-characteristics: time behavior, resource utilization, capacity.

**time behavior**
Sub-characteristic of performance efficiency. The degree to which the response and processing times and throughput rates of a product or system meet requirements.

**resource utilization**
Sub-characteristic of performance efficiency. The degree to which the amounts and types of resources used by a product or system meet requirements.

**capacity**
Sub-characteristic of performance efficiency. The degree to which the maximum limits of a product or system parameter meet requirements.

**maintainability**
ISO 25010 quality characteristic. The degree of effectiveness and efficiency with which a product or system can be modified. Sub-characteristics: modularity, reusability, analyzability, modifiability, testability.

**portability**
ISO 25010 quality characteristic. The degree of effectiveness and efficiency with which a system can be transferred from one hardware, software, or other operational or usage environment to another. Sub-characteristics: adaptability, installability, replaceability.

**coexistence**
Sub-characteristic of compatibility. The degree to which a product can perform its required functions efficiently while sharing a common environment and resources with other products.

**security**
ISO 25010 quality characteristic. The degree to which a product or system protects information and data so that persons or other products or systems have the degree of data access appropriate to their types and levels of authorization. Sub-characteristics: confidentiality, integrity, non-repudiation, accountability, authenticity.

**confidentiality**
Sub-characteristic of security. The degree to which a product or system ensures that data is accessible only to those authorized to have access.

**integrity**
Sub-characteristic of security. The degree to which a system, product, or component prevents unauthorized access to or modification of computer programs or data.

**non-repudiation**
Sub-characteristic of security. The degree to which actions or events can be proven to have taken place, so that they cannot be repudiated later.

**accountability**
Sub-characteristic of security. The degree to which the actions of an entity can be traced uniquely to that entity.

**authenticity**
Sub-characteristic of security. The degree to which the identity of a subject or resource can be proved to be the one claimed.

---

## Reliability and Performance Metrics

**operational profile**
The representation of the actual or anticipated usage of a software product. Defines user types and the frequency of operations performed.

**reliability growth model**
A model used to predict the improvement in reliability as defects are removed during testing.

**fault injection**
A method of dynamic analysis in which faults are deliberately introduced into a component or system to observe consequences and test fault tolerance.

**fault seeding**
The process of intentionally adding known defects to those already in a component or system to evaluate the efficacy of a test suite in detecting them.

---

## Safety

**safety integrity level (SIL)**
A discrete level (1–4) for specifying the safety integrity requirements of the safety functions allocated to the safety-related system. SIL 4 is the most demanding.

---

## Test Tools and Automation

**simulator**
A device, computer program, or system that, during testing, behaves or operates like a given system when provided with a set of controlled inputs. Typically software-only; faster but less hardware-accurate than an emulator.

**emulator**
A device, computer program, or system that accepts the same inputs and produces the same outputs as a given system. More accurately replicates hardware behavior than a simulator.

**keyword-driven testing**
A scripting technique in which test cases are defined using keywords. A keyword library maps keywords to automation code; test case authors need not write code.

**data-driven testing**
A scripting technique in which test input and expected results are stored in a data source, separate from the test script. The test script reads data and executes the same logic with multiple data sets.
