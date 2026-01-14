Verify code trustworthiness using the "Vibe and Verify" framework for production readiness.

## Trust Verification Framework

"Until organizations define what 'trustworthy code' means for them, they cannot assign accountability properly." - Tariq Shaukat

### Define Your Trust Threshold

Different organizations have different standards:
- **Start-up**: Speed-focused, higher risk tolerance
- **Enterprise**: Compliance, explainability, audit trails
- **Regulated Industry**: Evidence, reproducibility, documentation

### Four Pillars of Code Trust

#### 1. Explainability
- Can you explain why the code works?
- Is the logic clear and followable?
- Are decisions documented?
- Would a new team member understand it?

#### 2. Transparency
- Are there hidden behaviors?
- Is state mutation visible?
- Are side effects documented?
- Is the data flow traceable?

#### 3. Repeatability
- Does the same input produce the same output?
- Are there race conditions?
- Is behavior deterministic?
- Are external dependencies stable?

#### 4. Evidence
- Are there tests proving correctness?
- Is there documentation of intent?
- Are edge cases covered?
- Is there audit trail for changes?

### Independent Verification

Best practice: Use independent verification rather than having the same system evaluate its own output.

This skill will:
1. Cross-reference code against specifications
2. Verify external API/package existence
3. Check for logical consistency
4. Validate against coding standards
5. Ensure compliance requirements are met

### Trust Verification Process

```
Specification → Implementation → Verification → Trust Score
     ↓              ↓               ↓              ↓
  [Intent]      [Code]        [Evidence]      [Decision]
```

## Output Format

```
## Trust Verification Report

### Trust Score: [0-100] - [Trusted/Conditional/Untrusted]

### Organization Profile
- Trust threshold applied: [Start-up/Enterprise/Regulated]
- Compliance requirements: [list]

### Four Pillars Assessment

#### Explainability: [score]/100
- Logic clarity: [assessment]
- Documentation: [assessment]
- Findings: [issues]

#### Transparency: [score]/100
- Hidden behaviors: [none found / list]
- Side effects: [documented / undocumented]
- Data flow: [traceable / opaque]

#### Repeatability: [score]/100
- Determinism: [assessment]
- External dependencies: [stable / volatile]
- Race conditions: [none / potential / confirmed]

#### Evidence: [score]/100
- Test coverage: [percentage]
- Specification match: [percentage]
- Audit trail: [complete / partial / missing]

### Independent Verification Results
- External APIs verified: [count checked / count valid]
- Package dependencies verified: [count checked / count valid]
- Logic cross-check: [pass / issues found]

### Production Readiness
- [ ] Explainability requirements met
- [ ] Transparency requirements met
- [ ] Repeatability requirements met
- [ ] Evidence requirements met
- [ ] Compliance requirements met

### Recommendation
[Deploy / Deploy with conditions / Do not deploy]

### Required Actions Before Deployment
1. [Action items if conditional]
```

Specify the code to verify and optionally your organization's trust profile (start-up/enterprise/regulated).
