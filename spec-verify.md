Verify code implementation against specifications, requirements, or intended behavior.

## Specification Verification Framework

As highlighted in the article: "Describing what to build is harder than coding. Defining the right intent, the 'spec,' will be the core human task."

This skill helps bridge the gap between intent and implementation.

### Verification Process

1. **Gather Specification Sources**
   - README and documentation
   - Code comments and docstrings
   - Test descriptions and assertions
   - Type definitions and interfaces
   - API contracts (OpenAPI, GraphQL schemas)
   - User-provided requirements

2. **Intent Extraction**
   - What is this code supposed to do?
   - What are the expected inputs and outputs?
   - What are the constraints and edge cases?
   - What are the error conditions?

3. **Implementation Verification**
   - Does the code match the stated intent?
   - Are all specified behaviors implemented?
   - Are there undocumented behaviors (spec gaps)?
   - Are error cases handled as specified?

4. **Gap Analysis**
   - Missing implementations
   - Divergent behaviors
   - Ambiguous specifications needing clarification

## Output Format

```
## Specification Verification Report

### Specification Sources Found
- [List of docs, comments, types, tests analyzed]

### Stated Intent
[Summary of what the code should do based on specs]

### Verification Results

#### Implemented as Specified
- [Feature/Behavior]: [Evidence]

#### Deviations Found
| Spec Says | Code Does | Location | Severity |
|-----------|-----------|----------|----------|

#### Unspecified Behaviors
- [Behavior in code not covered by any spec]

#### Missing Implementations
- [Specified but not implemented]

### Recommendations
1. [Spec clarifications needed]
2. [Code fixes required]
3. [Documentation updates]

### Spec Quality Score: [A-F]
- Clarity: [score]
- Completeness: [score]
- Testability: [score]
```

Provide the specification/requirements document or describe the intended behavior. If not provided, the tool will extract intent from existing documentation, comments, and tests.
