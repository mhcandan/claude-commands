Audit AI integration across the entire Product Development Life Cycle (PDLC).

## PDLC Audit Framework

"Top performers take a holistic approach, embedding AI across the entire development life cycle rather than limiting themselves to isolated use cases." - McKinsey Research

**Key Finding**: Leaders are 6-7x more likely to scale to 4+ use cases. Nearly two-thirds of leaders report 4+ use cases at scale vs just 10% of bottom performers.

### The AI-Native PDLC Vision

Moving from "sparse documentation to a paved-path PDLC" (Cursor model):

```
┌─────────────────────────────────────────────────────────────────┐
│                    AI-NATIVE PDLC PIPELINE                      │
├─────────┬─────────┬─────────┬─────────┬─────────┬──────────────┤
│ DESIGN  │  CODE   │ REVIEW  │  TEST   │ DEPLOY  │   MONITOR    │
├─────────┼─────────┼─────────┼─────────┼─────────┼──────────────┤
│ AI-     │ AI      │ AI Code │ AI Test │ AI      │ AI           │
│ assisted│ Agents  │ Review  │ Gen &   │ Deploy  │ Observability│
│ specs   │ & Pair  │ (Bugbot)│ QA      │ Checks  │ & Alerting   │
│ & proto │ coding  │         │         │         │              │
└─────────┴─────────┴─────────┴─────────┴─────────┴──────────────┘
```

### PDLC Stage Assessment

#### Stage 1: Requirements & Design
**AI Opportunities**:
- Natural language to specification conversion
- Design document generation
- Prototype generation (Figma → code)
- Architecture recommendations
- User story refinement

**Assess**:
- [ ] AI used for spec writing
- [ ] AI-assisted prototyping
- [ ] Design-to-code workflows
- [ ] Architecture planning with AI

#### Stage 2: Coding
**AI Opportunities**:
- Code generation and completion
- Real-time collaboration with agents
- Background agents for parallel tasks
- Voice-driven development
- Multi-file refactoring

**Assess**:
- [ ] IDE-integrated AI (Cursor, Copilot, etc.)
- [ ] Plan Mode for change plotting
- [ ] Background agent usage
- [ ] Agent orchestration (parallel execution)

#### Stage 3: Code Review
**AI Opportunities**:
- Automated code review (Bugbot-style)
- Security scanning
- Quality checks
- Independent verification (AI checking AI)
- Pre-human validation layer

**Assess**:
- [ ] AI code review tools deployed
- [ ] AI as first reviewer before human
- [ ] Security/quality gates automated
- [ ] Review bottleneck reduced

#### Stage 4: Testing
**AI Opportunities**:
- Test generation
- Test case expansion
- Visual/browser-based testing
- Accessibility auditing
- Edge case discovery

**Assess**:
- [ ] AI-generated test cases
- [ ] Automated regression testing
- [ ] Visual testing in editor
- [ ] Coverage gap identification

#### Stage 5: Deployment
**AI Opportunities**:
- Deployment automation
- Rollback decisions
- Configuration validation
- Release notes generation
- DRI coordination

**Assess**:
- [ ] AI-assisted deployment checks
- [ ] Automated rollback triggers
- [ ] Release documentation generated
- [ ] DRI model implemented

#### Stage 6: Monitoring & Operations
**AI Opportunities**:
- Anomaly detection
- Incident classification
- Root cause analysis
- Performance optimization suggestions
- Proactive alerting

**Assess**:
- [ ] AI-driven observability
- [ ] Automated incident triage
- [ ] Performance insights
- [ ] Predictive monitoring

### Bottleneck Analysis

As AI accelerates coding, bottlenecks shift. Common new bottlenecks:
1. **Requirements clarity** - AI is literal, specs must be precise
2. **Code review** - Human review becomes constraint
3. **Testing** - Defining "truth" for validation
4. **Governance/Compliance** - Audit and approval processes

### Cursor-Style Workflow Elements

Modern PDLC integration patterns:
| Element | Description | Implemented? |
|---------|-------------|--------------|
| Plan Mode | Plot changes before implementation | |
| Background Agents | Parallel task execution | |
| In-Editor Browser | Visual testing during development | |
| Bugbot | AI code review pre-human | |
| Voice Collaboration | Refactor via voice commands | |
| Team Commands | Shared prompts/rules at various scopes | |

## Output Format

```
## PDLC Audit Report

### Overall Integration Level: [Isolated/Partial/Scaled/AI-Native]
### Use Cases at Scale: [count]/6+ (Target: 4+)

### Stage-by-Stage Assessment

| Stage | AI Integration | Maturity | Bottleneck? | Priority |
|-------|----------------|----------|-------------|----------|
| Design | [tools/none] | [1-5] | [Yes/No] | [H/M/L] |
| Code | [tools/none] | [1-5] | [Yes/No] | [H/M/L] |
| Review | [tools/none] | [1-5] | [Yes/No] | [H/M/L] |
| Test | [tools/none] | [1-5] | [Yes/No] | [H/M/L] |
| Deploy | [tools/none] | [1-5] | [Yes/No] | [H/M/L] |
| Monitor | [tools/none] | [1-5] | [Yes/No] | [H/M/L] |

### Pipeline Flow Visualization

```
Design ──▶ Code ──▶ Review ──▶ Test ──▶ Deploy ──▶ Monitor
  [2]       [5]      [2]       [3]      [2]        [1]
           ▲
           │
     BOTTLENECK
```

### Bottleneck Analysis
- Primary bottleneck: [Stage] - [Reason]
- Secondary bottleneck: [Stage] - [Reason]
- Root cause: [Analysis]

### Gap Analysis vs Top Performers
| Stage | Your Level | Top Performer Level | Gap |
|-------|------------|---------------------|-----|

### Recommended Tools/Practices

#### Immediate Additions
1. [Tool/Practice]: [Stage] - [Expected Impact]

#### Short-term Implementation
1. [Tool/Practice]: [Stage] - [Expected Impact]

### Integration Roadmap
1. [Phase 1 - Address bottleneck]
2. [Phase 2 - Scale existing]
3. [Phase 3 - Full AI-native]

### Expected Outcomes
- Productivity improvement: [estimate]%
- Quality improvement: [estimate]%
- Cycle time reduction: [estimate]%
```

Provide details about your current development workflow, tools used at each stage, and any known bottlenecks.
