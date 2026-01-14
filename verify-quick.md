Run a quick verification workflow for fast feedback.

## Quick Verification Workflow

A streamlined verification for rapid iteration - focuses on the most critical checks.

Execute these checks in parallel where possible:

### Parallel Checks (Run Together)
1. **AI Code Detection** - Is this AI-generated? Apply appropriate scrutiny
2. **Security Quick Scan** - Critical vulnerabilities only (injection, secrets, auth)
3. **Logic Check** - Obvious bugs, edge cases, error handling

### Sequential Check
4. **Trust Quick Check** - Can this safely go to production?

## Output Format

```
## Quick Verification Report

### Verdict: [Ship It / Needs Work / Stop]

### Time: [X seconds]

### Critical Findings
| Issue | Location | Severity | Fix |
|-------|----------|----------|-----|

### AI Assessment
- AI-generated: [Yes/No/Partial]
- Concerns: [None / List]

### Security
- Critical vulnerabilities: [None / Count]
- Secrets exposed: [None / Found]

### Quality
- Obvious bugs: [None / Count]
- Missing error handling: [None / Count]

### Trust Check
- Safe for production: [Yes / No / Conditional]

### Quick Actions
1. [Must do before merge]
```

Specify the file or code to verify. This is ideal for PR reviews and quick iterations.
