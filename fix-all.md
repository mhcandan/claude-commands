Run full verification and automatically apply fixes workflow.

## Verify and Fix Workflow

This workflow combines verification with automated fixes - find issues and resolve them in one pass.

### Phase 1: Comprehensive Scan
Run all verification checks to identify issues:
- Security vulnerabilities
- Code quality issues
- Performance problems
- AI-generated code patterns
- Test gaps

### Phase 2: Issue Prioritization
Categorize and prioritize findings:
- **Critical**: Security, breaking bugs - fix immediately
- **High**: Quality issues, maintainability - fix before merge
- **Medium**: Performance, style - fix when possible
- **Low**: Suggestions - consider for future

### Phase 3: Automated Fixes
Apply fixes in order of priority:

**Auto-fixable issues**:
- Security vulnerabilities with clear fixes
- Code style/formatting issues
- Simple bug fixes
- Missing error handling
- Type annotations
- Import cleanup

**Manual review required**:
- Architectural changes
- Logic modifications
- Performance optimizations
- Test additions

### Phase 4: Verification
Re-run checks to confirm fixes:
- All critical issues resolved
- No regressions introduced
- Tests still passing

### Safety Controls
Before any fix:
- [ ] File backed up / git status clean
- [ ] Tests exist for modified code
- [ ] Changes are incremental and reviewable

## Output Format

```
## Verify and Fix Report

### Summary
- Issues found: [X]
- Issues fixed: [X]
- Issues requiring manual review: [X]

### Scan Results

| Category | Found | Fixed | Remaining |
|----------|-------|-------|-----------|
| Security | X | X | X |
| Quality | X | X | X |
| Performance | X | X | X |
| AI Patterns | X | X | X |
| Testing | X | X | X |

### Fixes Applied

#### File: [filename]
| Line | Issue | Fix Applied |
|------|-------|-------------|
| X | [issue] | [fix description] |

[Show code diff for each fix]

### Remaining Issues (Manual Review Required)

| # | Category | Issue | Location | Why Manual |
|---|----------|-------|----------|------------|
| 1 | [cat] | [issue] | [loc] | [reason] |

### Verification Results
- Pre-fix score: [X]/100
- Post-fix score: [X]/100
- Improvement: +[X] points

### Test Results
- Tests passing: [Yes/No]
- New tests needed: [Yes/No]

### Next Steps
1. [ ] Review applied fixes
2. [ ] Address remaining manual items
3. [ ] Run tests
4. [ ] Commit changes
```

Specify the file or directory to verify and fix. You can also specify:
- `--dry-run`: Show what would be fixed without applying
- `--critical-only`: Only fix critical/security issues
- `--no-style`: Skip style/formatting fixes
