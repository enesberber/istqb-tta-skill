---
name: security-testing
description: Security testing — threats (unauthorized access, XSS, buffer overflow, DoS, MITM, logic bombs), planning requirements (written approval, ISO coordination, static analysis), attack vectors (UI/filesystem/OS/external software), ISO 25010 sub-characteristics (confidentiality, integrity, non-repudiation, accountability, authenticity).
type: rule
chapter: "4"
bloom: K2
priority: CRITICAL
syllabus: TTA-4.2
---

# Security Testing

## Definition

Security testing evaluates the degree to which the system protects information and resources from unauthorized access or modification, while ensuring authorized users have appropriate access.

---

## Common Security Threats

| Threat | Description |
|---|---|
| **Unauthorized access** | Gaining access to system resources without valid credentials |
| **Cross-Site Scripting (XSS)** | Injecting malicious scripts into web pages viewed by other users |
| **Buffer overflow** | Writing data beyond allocated buffer boundaries to overwrite adjacent memory / execute arbitrary code |
| **Denial of Service (DoS)** | Overwhelming system resources to make it unavailable to legitimate users |
| **Man-in-the-Middle (MITM)** | Intercepting communications between two parties to eavesdrop or modify data |
| **Logic bombs** | Malicious code inserted into software that activates under specific conditions |
| **SQL injection** | Inserting malicious SQL into input fields to manipulate the database |
| **Session hijacking** | Stealing a valid session token to impersonate an authenticated user |

---

## Planning Security Tests

### Mandatory: Get Explicit Written Approval
Security testing must **never** begin without explicit written authorization from the appropriate authority:
- System/application owner must provide written approval
- Scope of testing must be clearly defined in writing (systems, time window, techniques)
- Any penetration testing or active exploitation must be approved by legal counsel
- Insurance/liability must be confirmed

**Without written approval, security testing is illegal under computer misuse laws in most jurisdictions.**

### Coordinate with Information Security Officer (ISO)
- Involve the organization's security team from the start
- Align test activities with existing security policies and frameworks
- Ensure security test results feed into the organization's vulnerability management process
- Coordinate timing to avoid conflicts with production security monitoring (alerts may be triggered)

### Use Static Analysis as a Complement
- Static analysis tools detect security vulnerabilities without executing the system (e.g., SAST tools)
- Common findings: SQL injection patterns, hard-coded credentials, use of insecure functions
- Static analysis cannot detect all security issues — must be complemented by dynamic testing
- Integrate SAST tools into the CI/CD pipeline for early detection

---

## Attack Vectors for Test Specification

When designing security tests, consider all vectors through which an attacker could interact with the system:

### User Interface (UI)
- Input fields (forms, search boxes, URL parameters)
- File upload mechanisms
- Authentication forms (login, password reset)
- Client-side storage (cookies, localStorage, sessionStorage)

### File System
- File paths (directory traversal attacks)
- Uploaded file content (malicious file types)
- Temporary files with sensitive data
- Permissions on configuration files

### Operating System
- System calls from the application
- Environment variables
- Inter-process communication channels
- Scheduled tasks and services

### External Software and Interfaces
- Third-party libraries (known CVEs)
- Web services / APIs consumed by the system
- Database connections
- Message queues and event streams

---

## ISO 25010 Security Sub-Characteristics

Security is a quality characteristic in ISO 25010 with five sub-characteristics:

| Sub-Characteristic | Definition | Test Approach |
|---|---|---|
| **Confidentiality** | Data accessible only to authorized users | Test access controls, encryption, data masking |
| **Integrity** | Data can only be modified by authorized processes | Test input validation, checksums, audit trails |
| **Non-repudiation** | Actions cannot be denied by the actor | Test audit logging, digital signatures, timestamps |
| **Accountability** | Actions can be traced to the responsible entity | Test logging completeness, user tracking |
| **Authenticity** | Identity of users/components can be verified | Test authentication mechanisms, certificate validation |

---

## Security Test Specification

For each attack vector and sub-characteristic, specify:
1. The asset being protected (data, function, resource)
2. The threat being tested
3. The test approach (static, dynamic, penetration, fuzzing)
4. The expected secure behavior
5. The criteria for pass/fail

---

## Key Points

- Common threats: unauthorized access, XSS, buffer overflow, DoS, MITM, logic bombs
- **Always get written approval** before security testing — required by law
- Coordinate with Information Security Officer for scope and policy alignment
- Use static analysis (SAST) + dynamic testing for comprehensive coverage
- Attack vectors: UI, file system, operating system, external software
- ISO 25010 security sub-chars: confidentiality, integrity, non-repudiation, accountability, authenticity
