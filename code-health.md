Run a comprehensive code health check combining all verification and enhancement analyses.

## Holistic Code Health Framework

"Software productivity measurement is 'systems thinking.' The PDLC is a flow. If one part accelerates but another lags, you have not truly improved." - Andrew Lau, Jellyfish CEO

"Productivity is not just about output; it is about maintainability, quality, and reduced rework." - Tariq Shaukat, Sonar CEO

This is an all-in-one analysis covering the complete verification pipeline with trust verification.

### Three-Layer Assessment (from AI Transformation Framework)

#### Layer 1: Adoption & Tooling
- What tools/frameworks are in use?
- Are modern practices being followed?
- Is the codebase AI-ready (clear, well-structured)?

#### Layer 2: Throughput & Process Efficiency
- Code quality metrics
- Test coverage health
- Security posture
- Performance characteristics
- Review readiness

#### Layer 3: Outcome Alignment
- Does code align with specifications?
- Technical debt assessment
- Maintainability forecast
- Trust verification

### Trust Assessment (Four Pillars)

1. **Explainability** - Can you explain why the code works?
2. **Transparency** - Are there hidden behaviors?
3. **Repeatability** - Same input = same output?
4. **Evidence** - Tests, docs, audit trail?

### Analysis Components

Run these analyses in sequence:

1. **Quick Scan**: Structure, dependencies, obvious issues
2. **AI Code Detection**: Identify likely AI-generated sections
3. **Code Review**: Quality, clarity, correctness
4. **Security Scan**: Vulnerabilities, compliance
5. **Test Coverage**: Gaps, quality of tests
6. **Performance Review**: Bottlenecks, optimization opportunities
7. **Spec Verification**: Intent alignment
8. **Trust Verification**: Production readiness

### "Vibe and Verify" Checkpoint

Before any code reaches production:
- [ ] Code has been vibed (generated/written efficiently)
- [ ] Code has been verified (reviewed, tested, validated)
- [ ] Trust requirements met for organization type

## Output Format

```
## Code Health Report

### Executive Summary
[2-3 sentence overall assessment]

### Health Score: [A-F] ([0-100])
### Trust Score: [0-100] - [Trusted/Conditional/Untrusted]

### Dashboard
| Category | Score | Status | Priority Issues |
|----------|-------|--------|-----------------|
| Quality | X/100 | [emoji] | [count] |
| Security | X/100 | [emoji] | [count] |
| Testing | X/100 | [emoji] | [count] |
| Performance | X/100 | [emoji] | [count] |
| Spec Alignment | X/100 | [emoji] | [count] |
| Trust | X/100 | [emoji] | [count] |

### AI-Generated Code Assessment
- Detected AI-generated sections: [count/percentage]
- AI code quality: [Good/Needs Review/Poor]
- Hallucination check: [Pass/Issues Found]

### Trust Pillars
| Pillar | Score | Status |
|--------|-------|--------|
| Explainability | X/100 | [status] |
| Transparency | X/100 | [status] |
| Repeatability | X/100 | [status] |
| Evidence | X/100 | [status] |

### Critical Issues (Action Required)
1. [Issue + location + fix]

### Technical Debt Summary
- Current level: [Low/Medium/High/Critical]
- Key contributors: [list]
- Recommended paydown: [priorities]

### Pipeline Flow Analysis (Systems Thinking)
```
Requirements → Design → Code → Review → Test → Deploy
    [X]         [X]      [X]     [X]      [X]     [X]
```
Bottleneck identified: [stage]

### Improvement Roadmap
1. [Immediate actions - critical fixes]
2. [Short-term improvements - quality/trust]
3. [Long-term investments - architecture/process]

### Production Readiness
- [ ] Quality gates passed
- [ ] Security requirements met
- [ ] Test coverage adequate
- [ ] Trust verification complete
- [ ] Ready for deployment: [Yes/No/Conditional]

### Metrics to Track
- [Suggested KPIs for ongoing monitoring]
```

Ask the user which project, directory, or file to analyze if not specified. For large codebases, offer to focus on specific areas.
