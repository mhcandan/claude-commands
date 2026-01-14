Analyze test coverage and generate tests to improve code quality verification.

## Testing Framework (Defining "Truth" in Code)

The article highlights: "You cannot fully automate quality without defining 'truth'" - tests are how we formalize intent and correctness.

### Analysis Phase

1. **Existing Test Assessment**
   - Identify existing test files and frameworks
   - Calculate approximate coverage by examining test-to-source ratios
   - Identify untested functions, classes, and modules
   - Check for test quality (assertions, edge cases, mocking)

2. **Gap Analysis**
   - Critical paths without tests
   - Edge cases not covered
   - Error handling scenarios missing
   - Integration points untested

### Test Generation

Generate tests following these principles:

1. **Unit Tests** - Test individual functions/methods in isolation
   - Happy path scenarios
   - Edge cases (null, empty, boundary values)
   - Error conditions and exceptions

2. **Integration Tests** - Test component interactions
   - API endpoint tests
   - Database operations
   - External service interactions (mocked)

3. **Specification Tests** - Define expected behavior as tests
   - Business logic validation
   - Acceptance criteria verification

## Output Format

```
## Test Coverage Analysis

### Current State
- Test files found: [count]
- Estimated coverage: [percentage or qualitative]
- Testing framework: [detected framework]

### Coverage Gaps
| File/Module | Functions Untested | Priority |
|-------------|-------------------|----------|

### Generated Tests

[Provide test code for the highest priority gaps]

### Recommendations
1. [Priority test additions]
2. [Test infrastructure improvements]
```

Ask the user which file or module to analyze if not specified.
