Perform a comprehensive code review on the specified file or directory.

## Why Code Review Matters Now More Than Ever

"In the past, code review was something only top engineering companies did. Now, every large organization needs to make it part of their core discipline." - Tariq Shaukat, Sonar CEO

As AI generates more code, humans must verify larger volumes for subtle issues that are harder to spot.

## Review Framework (Based on AI-native PDLC principles)

### 0. AI-Generated Code Detection
First, assess if code appears AI-generated and apply extra scrutiny:
- Unusual verbosity or over-engineering
- Hallucinated APIs or phantom imports
- Confident but incorrect logic
- Generic naming patterns (data, result, temp)
- Missing edge case handling

### 1. Intent & Specification Clarity
- Does the code clearly express its intent?
- Are there ambiguous behaviors that need specification?
- Is the "truth" (expected behavior) well-defined?
- AI is literal, not creative - does the implementation match what was specified?

### 2. Quality & Correctness
- Logic errors and edge cases
- Error handling completeness
- Type safety and null checks
- Resource management (memory, connections, handles)
- Verify external APIs/packages actually exist

### 3. Security (Embedded Early)
- Input validation and sanitization
- Authentication/authorization gaps
- Injection vulnerabilities (SQL, command, XSS)
- Sensitive data exposure
- OWASP Top 10 compliance
- AI-specific: hardcoded placeholder credentials, disabled security "for simplicity"

### 4. Performance & Efficiency
- Algorithmic complexity concerns
- Unnecessary computations or allocations
- N+1 queries or inefficient data access
- Caching opportunities
- AI-specific: verbose solutions using 3x more code than needed

### 5. Maintainability & Clarity
- Code readability and naming
- Function/method size and complexity
- DRY violations
- Dead code or unused imports
- Style consistency with existing codebase

### 6. Trust & Accountability
- Is the logic explainable?
- Are there hidden behaviors or side effects?
- Is behavior reproducible and deterministic?
- Would this pass independent verification?

## Output Format

```
## Code Review Summary

### AI-Generated Assessment
- Appears AI-generated: [Yes/No/Partial]
- Extra scrutiny applied: [Yes/No]

### Overall Verdict: [Approve/Request Changes/Reject]

### Trust Score: [0-100]

## Critical Issues (Must Fix)
- [Issue]: [Location] - [Explanation]
  - Impact: [Security/Correctness/Performance]
  - Fix: [Suggested resolution]

## Recommendations (Should Fix)
- [Issue]: [Location] - [Explanation]

## Suggestions (Nice to Have)
- [Suggestion]: [Location] - [Explanation]

## Metrics
- Files reviewed: X
- Critical issues: X
- Recommendations: X
- Estimated technical debt: [Low/Medium/High]
- Production readiness: [Ready/Conditional/Not Ready]
```

Ask the user which file or directory to review if not specified.
