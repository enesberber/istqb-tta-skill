---
name: automation-approaches
description: Test automation approaches — GUI/API/CLI interfaces, capture/playback (fragile, high maintenance), data-driven (external data store, harness needed), keyword-driven (separates action/data/script, reduces maintenance, higher initial cost).
type: rule
chapter: "6"
bloom: K3
priority: HIGH
syllabus: TTA-6.2
---

# Automation Approaches

## Test Interfaces

Before choosing an automation approach, select the appropriate system interface:

| Interface | Description | Typical Tools |
|---|---|---|
| **GUI** | Drive the graphical user interface (buttons, forms, menus) | Selenium, Playwright, Cypress |
| **API** | Call the application's APIs directly (REST, SOAP, GraphQL) | Postman, RestAssured, requests |
| **CLI** | Execute command-line interfaces and check output | Shell scripts, Pexpect |

**Recommendation**: Prefer API over GUI automation where possible — APIs are more stable, faster, and less brittle than GUI interactions.

---

## Approach 1: Capture/Playback

### How It Works
A recording tool captures user interactions with the SUT (mouse clicks, keyboard input) and generates a script that replays them.

### Characteristics
- **Fast to create initially**: No programming required — just record and replay
- **Fragile**: Scripts break when UI elements change position, ID, or label
- **High maintenance burden**: Every UI change potentially breaks multiple recorded scripts
- **No abstraction**: Test logic is intertwined with UI details
- **Limited parameterization**: Handling different data requires script duplication

### When It May Be Acceptable
- Very short-lived automation (one-time regression run before a deadline)
- Systems with extremely stable UIs
- As a quick start that is immediately refactored into a more maintainable form

### Drawbacks
- ROI is typically poor for anything beyond a few months of use
- Maintenance cost can exceed manual test cost quickly
- Provides false confidence: passing scripts may not actually verify correct behavior

---

## Approach 2: Data-Driven Testing

### How It Works
Test logic (the script/harness) is separated from test data. Data is stored in an external source (spreadsheet, CSV, database, YAML/JSON file). The harness reads data and drives the same test script with multiple data sets.

### Structure
```
External Data Source → Test Harness → System Under Test
(CSV / Excel / DB)     (script)        (via GUI/API/CLI)
```

### Characteristics
- **Reduced duplication**: One script handles many data combinations
- **Non-technical users can add test cases**: Add a row to the spreadsheet without touching code
- **Harness required**: A test harness (framework code) must be developed to read data and drive tests
- **Data management**: Data files must be maintained alongside the test scripts
- **Parameterization**: Easy to test boundary values by adding data rows

### When to Use
- When the same test logic applies to many different data combinations
- When business users need to contribute test cases without programming
- For equivalence partitioning and boundary value testing at scale

### Example Data Table (Login Test)
| Username | Password | Expected Result |
|---|---|---|
| valid_user | correct_pw | Login success |
| valid_user | wrong_pw | Login failed |
| nonexistent | any_pw | User not found |
| valid_user | (empty) | Password required |

---

## Approach 3: Keyword-Driven Testing

### How It Works
Tests are expressed as sequences of **keywords** (actions) and their associated data. The keyword library translates keywords into automation code. Test cases are written in a high-level, human-readable table format.

### Structure
```
Test Case Table          Keyword Library         System Under Test
(Keywords + Data)   →   (Automation Code)   →   (via GUI/API/CLI)
```

### Example Test Case (keyword-driven style)
| Keyword | Parameter 1 | Parameter 2 |
|---|---|---|
| Open Browser | https://example.com | Chrome |
| Enter Text | username_field | test_user |
| Enter Text | password_field | secret123 |
| Click | login_button | |
| Verify Text | welcome_message | Welcome, test_user |

Tools: Robot Framework, Cucumber (Gherkin), FitNesse

### Characteristics
- **Separation of concerns**: Test cases (keywords) are separate from automation code (keyword implementation) and data
- **Reduces maintenance**: UI or API changes → update keyword implementation; test cases unchanged
- **Non-technical users can write tests**: Keywords read like plain English; no programming required for test case authoring
- **Higher initial cost**: Keyword library must be developed before test cases can be written
- **Reusability**: Keywords are reused across many test cases

### When to Use
- Projects requiring significant collaboration between technical and non-technical team members
- Long-lived automation suites where maintenance cost reduction justifies initial investment
- When business analysts or domain experts need to contribute test specifications

---

## Approach Comparison

| Criterion | Capture/Playback | Data-Driven | Keyword-Driven |
|---|---|---|---|
| Initial effort | Low | Medium | High |
| Maintenance effort | Very High | Medium | Low–Medium |
| Technical skill required | Low | Medium | Medium (library dev: High) |
| Non-technical contribution | No | Partial (data) | Yes (test cases) |
| Reusability | Low | Medium | High |
| Long-term ROI | Poor | Good | Best (for large suites) |
| Recommended for | Never (except short-term) | Data-intensive tests | Large, long-lived suites |

---

## Key Points

- Interfaces: GUI (fragile), API (preferred), CLI (simple)
- Capture/playback: fast to create, fragile, high maintenance, poor ROI — avoid for long-lived automation
- Data-driven: separates test data from test logic in external files; requires a test harness; good for data-intensive testing
- Keyword-driven: separates action (keywords) from data from implementation; reduces maintenance; higher initial cost; best for large, long-lived, cross-functional suites
- Prefer API automation over GUI automation for stability and speed
