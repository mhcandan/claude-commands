Audit AI-generated code for quality, trust, and production-readiness.

## AI Code Audit Framework

"We have moved beyond code generation being the bottleneck. The challenge now is clarity and trust." - Tariq Shaukat, Sonar CEO

AI-generated code requires special scrutiny because models have "personalities" - some are verbose, some introduce security issues, some are elegant but brittle.

### The "Vibe and Verify" Approach

You can "vibe" (generate code quickly), but you MUST verify before deployment.

### AI-Specific Code Patterns to Check

#### 1. Verbosity & Complexity
- Newer models (like GPT-5) use ~3x more lines of code
- Check for over-engineered solutions
- Identify unnecessary abstractions
- Flag bloated implementations that could be simpler

#### 2. Common AI Code Smells
- **Hallucinated APIs**: Functions/methods that don't exist
- **Version mismatches**: Using deprecated or future syntax
- **Phantom imports**: Importing non-existent packages
- **Confident incorrectness**: Plausible but wrong logic
- **Copy-paste artifacts**: Repeated patterns that should be abstracted
- **Incomplete error handling**: Happy path only
- **Generic variable names**: x, data, result, temp overuse

#### 3. Security Red Flags in AI Code
- Hardcoded credentials (AI often generates placeholder secrets)
- Disabled security features "for simplicity"
- SQL string concatenation
- Unvalidated user input
- Overly permissive CORS/permissions

#### 4. Maintainability Concerns
- Lack of comments on complex logic
- Missing type annotations
- Inconsistent coding style with existing codebase
- Magic numbers and strings
- Tight coupling

#### 5. Trust Verification
- Does the code do what was requested?
- Are there hidden behaviors?
- Is the logic explainable?
- Can results be reproduced?

### Audit Process

1. **Identify AI-generated sections** (if known)
2. **Compare against specification** - AI is literal, not creative
3. **Check for model artifacts** - Common patterns from specific models
4. **Verify external references** - APIs, packages, functions exist
5. **Test edge cases** - AI often misses boundaries
6. **Review for "elegant but brittle"** - Clever code that breaks easily

## Output Format

```
## AI Code Audit Report

### Code Origin
- Identified as AI-generated: [Yes/No/Partial/Unknown]
- Likely model characteristics: [verbose/concise/security-prone/etc.]

### Trust Assessment: [Trusted/Needs Review/Untrusted]

### Verification Results

#### Hallucination Check
| Issue | Location | Description |
|-------|----------|-------------|
| [Phantom API/Import/etc.] | [file:line] | [details] |

#### Quality Issues
- Verbosity score: [Low/Medium/High]
- Lines that could be simplified: [count]
- Unnecessary complexity: [examples]

#### Security Findings
- [Critical issues from AI patterns]

#### Maintainability
- Style consistency: [percentage match with codebase]
- Documentation level: [adequate/insufficient]
- Type safety: [strong/weak/none]

### Recommendations
1. [Must fix before production]
2. [Should improve]
3. [Consider for future]

### Trustworthiness Checklist
- [ ] Logic is explainable
- [ ] Behavior matches specification
- [ ] No hidden side effects
- [ ] Results are reproducible
- [ ] External dependencies verified
- [ ] Error handling complete
```

Specify the file or code block to audit. If code origin is known (which AI model generated it), provide that context for better analysis.
