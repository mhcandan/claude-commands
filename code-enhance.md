Enhance code by applying improvements based on review findings or specific enhancement requests.

## Code Enhancement Framework

"AI does not remove the need for compliance. It heightens it." - Controls must be embedded as part of enhancement.

### Enhancement Modes

#### 1. Fix Mode (Address Issues)
Apply fixes for identified issues:
- Security vulnerabilities
- Bug fixes
- Performance optimizations
- Code quality improvements

#### 2. Refactor Mode (Improve Structure)
Restructure code while preserving behavior:
- Extract functions/methods
- Reduce complexity
- Improve naming
- Apply design patterns
- Remove duplication

#### 3. Modernize Mode (Update Patterns)
Bring code up to current standards:
- Update deprecated APIs
- Apply modern language features
- Improve type safety
- Update dependencies

#### 4. Document Mode (Clarify Intent)
Improve specification clarity:
- Add/improve docstrings
- Add type annotations
- Create inline documentation for complex logic
- Generate API documentation

### Safety Controls (Embedded Early)

Before any enhancement:
1. **Verify tests exist** - Don't modify untested code without adding tests first
2. **Preserve behavior** - Unless explicitly changing functionality
3. **Incremental changes** - Small, reviewable modifications
4. **Rollback plan** - Ensure changes can be reverted

### Process

1. Analyze current state
2. Identify enhancement opportunities
3. Propose changes with rationale
4. Apply changes incrementally
5. Verify no regressions

## Output Format

```
## Enhancement Report

### Mode: [Fix/Refactor/Modernize/Document]

### Changes Applied

#### File: [filename]
- [Change description]
- Before: [snippet]
- After: [snippet]
- Rationale: [why]

### Verification
- Tests passing: [Yes/No/N/A]
- Behavior preserved: [Yes/No/Intentionally changed]

### Additional Recommendations
- [Further improvements not applied]
```

Specify the enhancement mode and target file/directory. Can also provide specific issues to fix from a previous code-review or code-health run.
