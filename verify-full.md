Run the complete code verification workflow in sequence.

## Full Verification Workflow

This workflow chains together all verification steps automatically.

Execute the following steps in order:

### Step 1: Quick Health Scan
First, get an overview of the codebase health:
- Identify structure and dependencies
- Detect obvious issues
- Assess AI-generated code presence

### Step 2: AI Code Audit
Check for AI-specific patterns:
- Hallucinated APIs/imports
- Verbose/over-engineered solutions
- Placeholder credentials
- Confident but incorrect logic

### Step 3: Security Scan
Run OWASP Top 10 and security checks:
- Injection vulnerabilities
- Authentication issues
- Sensitive data exposure
- Dependency vulnerabilities

### Step 4: Code Review
Comprehensive quality review:
- Logic errors and edge cases
- Error handling
- Maintainability
- Style consistency

### Step 5: Test Coverage Analysis
Assess testing health:
- Identify untested code
- Coverage gaps
- Test quality

### Step 6: Performance Review
Check for bottlenecks:
- Algorithmic complexity
- N+1 queries
- Memory issues

### Step 7: Trust Verification
Final production readiness check:
- Explainability
- Transparency
- Repeatability
- Evidence

## Output Format

Provide a unified report combining all findings:

```
## Full Verification Report

### Overall Verdict: [Ready/Conditional/Not Ready]
### Health Score: [0-100] | Trust Score: [0-100]

### Executive Summary
[2-3 sentences on overall state]

### Critical Issues (Block Deployment)
| # | Category | Issue | Location | Fix |
|---|----------|-------|----------|-----|

### High Priority (Fix Soon)
| # | Category | Issue | Location | Fix |
|---|----------|-------|----------|-----|

### Recommendations
| # | Category | Issue | Location | Suggestion |
|---|----------|-------|----------|------------|

### Scores by Category
| Category | Score | Issues |
|----------|-------|--------|
| AI Code Quality | X/100 | X |
| Security | X/100 | X |
| Code Quality | X/100 | X |
| Test Coverage | X/100 | X |
| Performance | X/100 | X |
| Trust | X/100 | X |

### Action Items
1. [ ] [Immediate action]
2. [ ] [Before next release]
3. [ ] [Technical debt]

### Production Checklist
- [ ] All critical issues resolved
- [ ] Security requirements met
- [ ] Tests adequate
- [ ] Trust verified
- [ ] Ready for deployment
```

Ask which file, directory, or project to verify if not specified.
