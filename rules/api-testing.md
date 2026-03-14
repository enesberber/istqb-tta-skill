---
name: api-testing
description: API testing as a test type (not coverage technique) — evaluating inputs/outputs, negative testing, combinatorial interface testing, error/retry handling, RESTful coverage criteria. Typical defect types: interface issues, timing, lost transactions.
type: rule
chapter: "2"
bloom: K2
priority: HIGH
syllabus: TTA-2.7
---

# API Testing

## Definition

API testing evaluates **application programming interfaces** by sending requests and verifying responses. Unlike white-box coverage techniques, API testing is a **test type** focused on the contract between components, not on internal code coverage.

APIs include:
- RESTful HTTP APIs
- SOAP web services
- Library/module interfaces (function calls)
- Message-based interfaces (queues, events)
- Database interfaces

---

## Test Design Approaches

### Input/Output Evaluation
- Verify that valid inputs produce expected outputs
- Verify data types, formats, and value ranges in responses
- Check headers, status codes, and response structure

### Negative Testing
- Send invalid data types (e.g., string where integer expected)
- Send out-of-range values (boundary violations)
- Send malformed requests (missing required fields)
- Test behavior when required parameters are absent
- Verify appropriate error codes and error messages are returned

### Combinatorial Interface Testing
- Combine multiple parameters to test interaction effects
- Apply equivalence partitioning and boundary value analysis to API parameters
- Use pairwise testing to reduce the combination space for many parameters

### Error and Retry Testing
- Simulate network failures and verify retry logic
- Verify timeout handling (what happens when backend is slow)
- Verify circuit breaker patterns (if applicable)
- Test idempotency for operations that may be retried (PUT, DELETE)

---

## RESTful API Coverage Criteria

For REST APIs, coverage can be defined by:

### Input-Based Coverage
- All endpoints called (at minimum)
- All HTTP methods exercised (GET, POST, PUT, PATCH, DELETE)
- All required parameters provided with valid values
- All optional parameters tested present and absent
- All valid authentication tokens / unauthorized scenarios

### Output-Based Coverage
- All documented response status codes triggered (200, 201, 400, 401, 403, 404, 409, 500...)
- All documented response body structures returned
- Error response formats verified

---

## Typical API Defect Classes

| Defect Type | Description | Example |
|---|---|---|
| Interface issues | Wrong data type, format, or encoding | API returns integer string instead of number |
| Incorrect parameter handling | Ignored or misprocessed parameters | Optional filter parameter has no effect |
| Timing/race conditions | Concurrent calls produce inconsistent results | Two simultaneous POSTs create duplicate records |
| Lost transactions | Request received but response not sent, or processing silently fails | Order submitted, no confirmation, no DB record |
| Missing error handling | Invalid input causes unhandled exception / 500 | Null field causes NullPointerException returned as 500 |
| Security misconfigurations | Unauthorized access to resources | Resource accessible without authentication token |

---

## Relation to White-Box Techniques

API testing is **complementary** to white-box coverage techniques:
- White-box techniques (statement, decision, MC/DC) measure internal code coverage
- API testing validates the **external contract** from the caller's perspective
- An API test suite may drive white-box coverage measurement if the code under test is accessible
- API tests can be part of component testing, integration testing, or system testing

---

## Key Points

- API testing is a **test type**, not a coverage measurement technique
- Applies input/output evaluation, negative testing, combinatorial testing, error/retry testing
- RESTful coverage: input criteria (endpoints, methods, params) + output criteria (status codes, response structures)
- Primary defect types: interface issues, timing/race conditions, lost transactions
- Complements white-box techniques — provides external contract validation
