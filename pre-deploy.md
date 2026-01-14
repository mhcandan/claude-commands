Run pre-deployment verification workflow with "Vibe and Verify" checklist.

## Pre-Deployment Workflow

Final verification before code reaches production. Based on the principle: "You can vibe (generate quickly), but you must verify before deployment."

### Phase 1: Security Gate
Critical security checks that block deployment:
- [ ] No hardcoded secrets
- [ ] No injection vulnerabilities
- [ ] Authentication/authorization intact
- [ ] Dependencies secure

### Phase 2: Quality Gate
Quality checks for production readiness:
- [ ] No critical bugs
- [ ] Error handling complete
- [ ] Edge cases covered
- [ ] No obvious regressions

### Phase 3: Test Gate
Testing verification:
- [ ] Critical paths tested
- [ ] No failing tests
- [ ] Coverage acceptable for changed code

### Phase 4: Trust Gate (Four Pillars)
Final trust verification:
- [ ] **Explainable**: Logic is clear and documented
- [ ] **Transparent**: No hidden behaviors
- [ ] **Repeatable**: Deterministic results
- [ ] **Evidenced**: Tests and docs exist

### Phase 5: Compliance Gate (if applicable)
For regulated environments:
- [ ] Audit trail exists
- [ ] Change documented
- [ ] Approvals recorded

## Output Format

```
## Pre-Deployment Report

### DEPLOYMENT DECISION: [APPROVED / BLOCKED / CONDITIONAL]

### Gate Status

| Gate | Status | Blockers |
|------|--------|----------|
| Security | [Pass/Fail] | [count] |
| Quality | [Pass/Fail] | [count] |
| Testing | [Pass/Fail] | [count] |
| Trust | [Pass/Fail] | [count] |
| Compliance | [Pass/Fail/N/A] | [count] |

### Blockers (Must Resolve)
| # | Gate | Issue | Location | Resolution |
|---|------|-------|----------|------------|

### Warnings (Should Resolve)
| # | Gate | Issue | Location | Risk |
|---|------|-------|----------|------|

### Deployment Checklist
- [ ] All blockers resolved
- [ ] Warnings acknowledged
- [ ] Rollback plan ready
- [ ] Monitoring in place
- [ ] Team notified

### Sign-Off
- Verified by: [AI verification system]
- Timestamp: [datetime]
- Recommendation: [Deploy / Do not deploy / Deploy with monitoring]
```

Specify the code, branch, or PR to verify for deployment.
