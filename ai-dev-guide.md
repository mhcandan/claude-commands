Quick reference guide for AI-native software development best practices.

## AI-Native Development Guide

Compiled from McKinsey research and industry leader interviews (Jellyfish, Sonar, Cursor).

---

## Key Statistics

| Metric | Finding |
|--------|---------|
| Performance gap | 15 percentage points between top/bottom performers |
| Productivity gains (leaders) | 16-30% improvement |
| Quality gains (leaders) | 31-45% improvement |
| Adoption threshold for major gains | 80-100% developer adoption → 110%+ gains |
| PDLC use cases at scale (leaders) | 4+ (vs 10% of bottom performers) |
| Time saved with AI | Average 6 hours/week per developer |

---

## Two Key Shifts

### Shift 1: End-to-End PDLC Implementation
Don't limit AI to isolated use cases. Embed across entire life cycle:
- Design → Code → Review → Test → Deploy → Monitor
- Leaders are 6-7x more likely to scale to 4+ use cases

### Shift 2: AI-Native Roles
Roles are evolving:
- **Engineers**: Full-stack fluency + spec communication + architectural thinking
- **PMs**: Less delivery, more design/prototyping/QA/responsible AI
- **New model**: Orchestrators of parallel AI agents

---

## Three Critical Enablers

### 1. Upskilling (57% top vs 20% bottom)
- Hands-on workshops > on-demand courses
- One-on-one coaching
- Training mirrors real work (code reviews, sprints)
- Continuous, not one-off
- Internal "AI guilds" for best practice sharing

### 2. Impact Measurement
**Track outcomes, not adoption**:
- Quality improvements (79% of top performers track)
- Speed gains (57% of top performers track)

**Avoid weak proxies**:
- % of code written by AI
- Tool usage frequency
- Lines of code

### 3. Change Management
- 80% of top performers link AI goals to reviews
- Incentivize behaviors, not just usage
- Connect AI work to broader outcomes

---

## The "Vibe and Verify" Framework

```
VIBE: Generate code quickly with AI
  ↓
VERIFY: Before deployment ensure:
  □ Trust requirements met
  □ Quality verified
  □ Security checked
  □ Compliance confirmed
```

---

## Four Trust Pillars

| Pillar | Question |
|--------|----------|
| Explainability | Can you explain why it works? |
| Transparency | Are there hidden behaviors? |
| Repeatability | Same input = same output? |
| Evidence | Tests, docs, audit trail? |

---

## AI Code Review Essentials

"Code review was something only top engineering companies did. Now, every large organization needs to make it part of their core discipline."

**Watch for AI-generated code patterns**:
- Verbose solutions (newer models use 3x more code)
- Hallucinated APIs/imports
- Confident but incorrect logic
- Hardcoded placeholder secrets
- Missing edge cases

---

## Cursor-Style Workflow

Modern AI-native development elements:
| Element | Description |
|---------|-------------|
| Plan Mode | Plot changes before implementation |
| Background Agents | Parallel task execution |
| Bugbot | AI code review before human review |
| DRI | Dedicated Responsible Individual per release |
| Small Pods | Cross-functional, cross-team projects |
| Voice Dev | Refactor and query via voice |

---

## Measurement Framework

### Three Layers
1. **Adoption**: Are tools being used?
2. **Throughput**: PR rate, cycle time, latency
3. **Outcomes**: Road map progress, defects, customer impact

### Three Steps
1. Select meaningful metrics (outcomes > adoption)
2. Build integrated tracking (tools → repos → CI/CD → production)
3. Report insights regularly (weekly/bi-weekly/monthly by audience)

---

## Systems Thinking

"The PDLC is a flow. If one part accelerates but another lags, you have not truly improved."

Common bottleneck shifts:
| If This Accelerates | This May Become Bottleneck |
|---------------------|---------------------------|
| Code generation | Requirements clarity |
| Code generation | Code review capacity |
| Code generation | Testing/QA |
| All development | Governance/compliance |

---

## Quick Commands Reference

| Command | Use Case |
|---------|----------|
| `/code-health` | Full holistic assessment |
| `/code-review` | Comprehensive code review |
| `/ai-code-audit` | Audit AI-generated code specifically |
| `/trust-verify` | Production readiness check |
| `/security-scan` | Security and compliance |
| `/test-coverage` | Test gaps and generation |
| `/perf-review` | Performance analysis |
| `/spec-verify` | Intent alignment check |
| `/code-enhance` | Apply fixes and improvements |
| `/team-assessment` | Team AI-readiness |
| `/pdlc-audit` | PDLC integration audit |
| `/impact-measure` | Outcome metrics analysis |
| `/dev-metrics` | Development metrics framework |

---

## Key Quotes

> "Describing what to build is harder than coding. Defining the right intent will be the core human task." - Andrew Lau, Jellyfish

> "Lines of code or AI contribution percentages don't reveal whether the output is secure, maintainable, or even useful." - Tariq Shaukat, Sonar

> "AI does not remove the need for compliance. It heightens it." - Andrew Lau, Jellyfish

> "Over the next decade, AI-assisted programming will let developers specify intent through a mix of formal programming languages and natural language." - Michael Truell, Cursor

---

This guide is a quick reference. Use specific `/commands` for detailed analysis and implementation.
