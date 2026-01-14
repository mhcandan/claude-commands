Run AI code review workflow for pull requests.

## PR Review Workflow

Automated code review for pull requests - like Bugbot from Cursor, providing an AI review layer before human review.

"Code review is now something every large organization needs to make part of their core discipline." - Tariq Shaukat, Sonar

### Review Process

#### Step 1: Change Analysis
Understand the PR:
- What files changed?
- What's the intent of the change?
- How large is the diff?

#### Step 2: AI Code Detection
Assess if changes are AI-generated:
- Verbosity patterns
- Common AI artifacts
- Hallucination risks

#### Step 3: Security Review
Check for security issues in changed code:
- New vulnerabilities introduced?
- Secrets added?
- Auth changes safe?

#### Step 4: Quality Review
Assess code quality:
- Logic correct?
- Edge cases handled?
- Error handling complete?
- Tests included?

#### Step 5: Spec Alignment
Verify changes match intent:
- Does this do what PR claims?
- Any scope creep?
- Unintended side effects?

#### Step 6: Maintainability Check
Long-term health:
- Follows codebase patterns?
- Readable and clear?
- Technical debt impact?

### Review Output

Provide actionable feedback in standard PR review format.

## Output Format

```
## PR Review: [PR Title/Branch]

### Review Summary
| Aspect | Status | Issues |
|--------|--------|--------|
| Security | [Pass/Warn/Fail] | X |
| Quality | [Pass/Warn/Fail] | X |
| Tests | [Pass/Warn/Fail] | X |
| Maintainability | [Pass/Warn/Fail] | X |

### Verdict: [Approve / Request Changes / Comment]

### AI Assessment
- AI-generated content detected: [Yes/No/Partial]
- Confidence: [High/Medium/Low]
- Extra scrutiny applied: [Yes/No]

---

### Critical Issues (Must Fix)

#### File: `path/to/file.ts`

**Line X-Y**: [Issue Title]
```
[code snippet]
```
**Problem**: [Explanation]
**Suggestion**: [How to fix]

---

### Suggestions (Should Consider)

#### File: `path/to/file.ts`

**Line X**: [Suggestion]
[Explanation and recommendation]

---

### Nitpicks (Optional)

- `file.ts:X` - [Minor suggestion]

---

### Questions for Author

1. [Question about design decision]
2. [Clarification needed]

---

### Test Coverage
- New code tested: [Yes/No/Partial]
- Suggested tests: [List if needed]

---

### Summary

**What's good:**
- [Positive feedback]

**What needs work:**
- [Key changes requested]

**Recommendation**: [Approve after X / Block until Y]
```

Provide the PR diff, files changed, or point to a git branch to review.
