---
name: static-analysis-maintainability
description: Static analysis for maintainability verifies coding standards (naming, commenting, indentation, modularization), coupling/cohesion metrics, repeated code detection, structural complexity, and website tree balance.
type: rule
chapter: "3"
bloom: K3
priority: MEDIUM
syllabus: TTA-3.4
---

# Static Analysis for Maintainability

## Definition

Static analysis for maintainability examines **source code structure and style** without execution to identify characteristics that make code harder to understand, modify, test, or maintain over time.

---

## Coding Standards Verification

Static analysis tools enforce organizational or industry coding standards:

### Naming Conventions
- Variable, function, class names follow agreed conventions (camelCase, snake_case, PascalCase)
- Names are meaningful and not abbreviated cryptically
- Constants are distinguished from variables (e.g., ALL_CAPS)

### Commenting and Documentation
- Public APIs have documentation comments (Javadoc, docstrings, XML docs)
- Complex logic has inline explanations
- TODO/FIXME comments are tracked
- Absence of useless comments that merely restate the code

### Indentation and Formatting
- Consistent indentation (tabs vs. spaces, indentation depth)
- Line length limits respected
- Consistent brace placement

### Modularization
- Functions/methods have single responsibility
- Functions do not exceed a maximum length (e.g., 50 lines)
- No deeply nested structures beyond a threshold

---

## Coupling and Cohesion Metrics

### Coupling (Between Modules)
Measures how strongly different modules depend on each other.

| Metric | Description | Good Value |
|---|---|---|
| Afferent coupling (Ca) | Number of classes that depend on this class | Lower is more stable |
| Efferent coupling (Ce) | Number of classes this class depends on | Lower is more independent |
| Instability (I = Ce/(Ca+Ce)) | How likely to change due to dependencies | Stable = low I |

**High coupling** indicates:
- Changes in one module likely break others
- Difficult to test in isolation
- Difficult to reuse

### Cohesion (Within a Module)
Measures how closely related the responsibilities within a module are.

- **High cohesion**: Module has a single, well-defined purpose (desirable)
- **Low cohesion**: Module does many unrelated things (utility classes, god objects)

---

## Repeated Code Detection

Also called **clone detection**:
- Identifies duplicate or near-duplicate code blocks
- Types: exact copies, renamed variables, structurally similar
- Tools: SonarQube, PMD Copy/Paste Detector, Simian, Checkstyle

**Impact of repeated code:**
- Bug fixes must be applied to all copies
- Changes in requirements require multiple updates
- Increased maintenance cost proportional to clone count

---

## Structural Complexity

Beyond cyclomatic complexity (see control-flow-analysis), static analysis highlights:

- **Nesting depth**: Deeply nested if/loop structures are hard to understand
- **Fan-in / fan-out**: Functions called by many (high fan-in) or calling many (high fan-out) are harder to maintain
- **Class size**: Classes with too many methods or too many lines
- **Parameter count**: Functions with many parameters are harder to call correctly

---

## Website / Tree Structure Balance

For web applications, static analysis can evaluate:
- **Navigation tree balance**: Depth of site hierarchy (flat vs. deep)
- **Broken internal links**: Static analysis of href targets
- **Orphaned pages**: Pages not reachable from navigation
- **Consistent page structure**: Template compliance across pages

---

## Applying Static Analysis for Maintainability

### Tool Examples
- SonarQube: coding standards, complexity, duplication, coupling
- Checkstyle / PMD: Java standards enforcement
- ESLint / TSLint: JavaScript/TypeScript style
- Pylint / Flake8: Python style and conventions
- StyleCop / ReSharper: C# conventions

### Integration
- Run in CI/CD pipeline on every commit
- Enforce quality gates (build fails if thresholds exceeded)
- Report trends over time (maintainability index improving or degrading)

---

## Key Points

- Static analysis for maintainability verifies coding standards, naming, commenting, modularization
- Coupling and cohesion metrics indicate structural quality
- Repeated code detection identifies maintenance liabilities
- Structural complexity (nesting depth, fan-in/fan-out) highlights risk areas
- Tools integrate into CI/CD; set quality gates to prevent maintainability degradation
