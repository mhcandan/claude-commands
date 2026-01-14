Display the complete guide for code verification and enhancement commands.

---

# Code Verification & Enhancement Command Guide

A comprehensive skill set for AI-native software development, built on insights from McKinsey research, Jellyfish, Sonar, and Cursor.

---

## Quick Start

```bash
# New to this? Start here:
/verify-quick myfile.ts          # Quick check on a file
/pr-review                       # Review a pull request
/ai-dev-guide                    # See all best practices
```

---

## Command Categories

### 1. Workflow Commands (Multi-Step)
These run multiple checks automatically - use these for efficiency.

| Command | Description | Best For |
|---------|-------------|----------|
| `/verify-quick` | Fast critical checks (parallel) | PR feedback, quick iterations |
| `/verify-full` | All checks in sequence | Major releases, thorough review |
| `/pre-deploy` | Gate-based deployment checklist | Before production deployment |
| `/pr-review` | AI code review (Bugbot-style) | Every pull request |
| `/fix-all` | Find issues + auto-fix them | Code cleanup sessions |
| `/org-assess` | Full team/process assessment | Quarterly planning |

### 2. Code Verification Commands (Single Focus)
Deep-dive into specific aspects.

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/code-health` | Holistic health assessment | Overall codebase checkup |
| `/code-review` | Comprehensive quality review | Detailed code analysis |
| `/ai-code-audit` | Audit AI-generated code | When code is AI-written |
| `/trust-verify` | "Vibe and Verify" trust check | Production readiness |
| `/security-scan` | OWASP Top 10 + vulnerabilities | Security audit |
| `/test-coverage` | Test gaps and generation | Improve testing |
| `/perf-review` | Performance bottlenecks | Optimization work |
| `/spec-verify` | Code vs specification check | Verify intent match |
| `/code-enhance` | Apply fixes and improvements | After finding issues |

### 3. Team & Process Commands
Organizational readiness and metrics.

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/team-assessment` | Team AI-readiness evaluation | Assess team maturity |
| `/pdlc-audit` | Pipeline integration audit | Find PDLC gaps |
| `/impact-measure` | Outcome metrics analysis | Improve measurement |
| `/dev-metrics` | Metrics framework setup | Build dashboards |
| `/ai-dev-guide` | Quick reference guide | Learn best practices |

---

## Common Workflows

### Daily Development Flow
```
Write Code
    ↓
/verify-quick src/myfeature/     # Fast feedback
    ↓
Fix issues found
    ↓
/pr-review                       # AI review before human review
    ↓
Submit PR
```

### Pre-Release Flow
```
Feature Complete
    ↓
/verify-full src/                # Comprehensive verification
    ↓
/fix-all src/                    # Auto-fix what's possible
    ↓
/pre-deploy                      # Final gate checks
    ↓
Deploy ✓
```

### Code Cleanup Session
```
/code-health src/                # Get overall picture
    ↓
/fix-all src/                    # Auto-fix issues
    ↓
/verify-full src/                # Confirm improvements
```

### AI-Generated Code Review
```
/ai-code-audit path/to/file.ts   # Check for AI patterns
    ↓
/trust-verify path/to/file.ts    # Verify trustworthiness
    ↓
/code-enhance path/to/file.ts    # Fix AI-specific issues
```

### Security Audit
```
/security-scan src/              # Find vulnerabilities
    ↓
/code-enhance --critical-only    # Fix security issues
    ↓
/pre-deploy                      # Verify gates pass
```

### Team Assessment (Quarterly)
```
/org-assess                      # Full assessment
    ↓
/pdlc-audit                      # Pipeline gaps
    ↓
/impact-measure                  # Metrics health
    ↓
Create improvement roadmap
```

---

## Command Details

### `/verify-quick` - Fast Verification
**Purpose**: Rapid feedback during development
**Runs**: AI detection + Security quick scan + Logic check + Trust check (parallel)
**Output**: Ship It / Needs Work / Stop verdict
**Use when**: You want fast feedback, PR reviews, iterating quickly

```bash
/verify-quick src/components/Button.tsx
/verify-quick src/api/
```

### `/verify-full` - Complete Verification
**Purpose**: Thorough verification before releases
**Runs**: All 7 verification steps in sequence
**Output**: Comprehensive report with scores and action items
**Use when**: Before major releases, thorough code review needed

```bash
/verify-full src/
/verify-full src/features/auth/
```

### `/pre-deploy` - Deployment Gates
**Purpose**: Final check before production
**Runs**: Security → Quality → Test → Trust → Compliance gates
**Output**: APPROVED / BLOCKED / CONDITIONAL decision
**Use when**: About to deploy to production

```bash
/pre-deploy
/pre-deploy feature-branch
```

### `/pr-review` - AI Code Review
**Purpose**: Automated PR review (like Cursor's Bugbot)
**Runs**: Change analysis → AI detection → Security → Quality → Spec alignment
**Output**: Approve / Request Changes / Comment with detailed feedback
**Use when**: Every pull request, before human review

```bash
/pr-review
/pr-review feature/new-dashboard
```

### `/fix-all` - Verify and Fix
**Purpose**: Find issues and automatically fix them
**Runs**: Full scan → Prioritize → Auto-fix → Re-verify
**Output**: Report of what was found, fixed, and remaining
**Use when**: Code cleanup sessions, addressing tech debt

```bash
/fix-all src/
/fix-all src/ --dry-run          # Preview without changes
/fix-all src/ --critical-only    # Only fix critical issues
```

### `/ai-code-audit` - AI Code Audit
**Purpose**: Specifically audit AI-generated code
**Checks**: Hallucinations, verbosity, placeholder secrets, AI patterns
**Output**: Trust assessment with specific AI-related findings
**Use when**: Reviewing code generated by AI tools

```bash
/ai-code-audit src/newFeature.ts
```

### `/trust-verify` - Trust Verification
**Purpose**: Check production readiness via trust pillars
**Checks**: Explainability, Transparency, Repeatability, Evidence
**Output**: Trust score and production readiness decision
**Use when**: Final verification before deployment

```bash
/trust-verify src/critical-module/
```

### `/org-assess` - Organization Assessment
**Purpose**: Evaluate team AI-readiness
**Checks**: Two shifts + Three enablers + PDLC coverage + Metrics
**Output**: Maturity level and improvement roadmap
**Use when**: Quarterly planning, transformation initiatives

```bash
/org-assess
```

---

## Key Concepts

### The "Vibe and Verify" Framework
- **Vibe**: Generate code quickly with AI
- **Verify**: Always verify before deployment
  - Trust requirements met?
  - Quality verified?
  - Security checked?
  - Compliance confirmed?

### Four Trust Pillars
1. **Explainability**: Can you explain why the code works?
2. **Transparency**: Are there hidden behaviors?
3. **Repeatability**: Same input = same output?
4. **Evidence**: Tests, docs, audit trail exist?

### Two Key Shifts (Top Performers)
1. **End-to-End PDLC**: AI across Design → Code → Review → Test → Deploy → Monitor
2. **AI-Native Roles**: Engineers as orchestrators, PMs in design/QA

### Three Critical Enablers
1. **Upskilling**: Hands-on training, not just courses
2. **Impact Measurement**: Track outcomes, not just adoption
3. **Change Management**: AI goals in performance reviews

### AI Code Patterns to Watch
- Verbose solutions (newer models use 3x more code)
- Hallucinated APIs/imports that don't exist
- Hardcoded placeholder credentials
- Confident but incorrect logic
- Missing edge case handling

---

## Performance Benchmarks

What top performers achieve:
| Metric | Improvement |
|--------|-------------|
| Team Productivity | 16-30% |
| Customer Experience | 16-30% |
| Time to Market | 16-30% |
| Software Quality | 31-45% |

Key threshold: 80-100% developer adoption → 110%+ productivity gains

---

## Tips for Best Results

1. **Start with workflows**: Use `/verify-quick` or `/verify-full` instead of individual commands
2. **Be specific**: Point to specific files/directories for focused analysis
3. **Use quick for iteration**: `/verify-quick` for fast feedback loops
4. **Use full before releases**: `/verify-full` for comprehensive checks
5. **Fix in batches**: Use `/fix-all` to address multiple issues at once
6. **Review AI code extra carefully**: Use `/ai-code-audit` for AI-generated code
7. **Quarterly assessments**: Run `/org-assess` to track team maturity

---

## Command Reference Card

```
WORKFLOWS (use these most often)
├── /verify-quick     Fast checks for daily work
├── /verify-full      Complete checks for releases
├── /pre-deploy       Final deployment gates
├── /pr-review        AI code review for PRs
├── /fix-all          Find and fix issues
└── /org-assess       Team/process assessment

CODE VERIFICATION (deep dives)
├── /code-health      Overall health check
├── /code-review      Quality review
├── /ai-code-audit    AI-generated code audit
├── /trust-verify     Production readiness
├── /security-scan    Security vulnerabilities
├── /test-coverage    Testing gaps
├── /perf-review      Performance issues
├── /spec-verify      Specification alignment
└── /code-enhance     Apply improvements

TEAM & PROCESS
├── /team-assessment  Team readiness
├── /pdlc-audit       Pipeline integration
├── /impact-measure   Metrics analysis
├── /dev-metrics      Metrics framework
└── /ai-dev-guide     Best practices reference
```

---

## Sources

This command set is built on insights from:
- McKinsey research on AI in software development
- Interview with Andrew Lau, CEO of Jellyfish
- Interview with Tariq Shaukat, CEO of Sonar
- Cursor workflow patterns (Plan Mode, Bugbot, Background Agents)

---

Run `/ai-dev-guide` for a quick reference of all best practices and key statistics.
