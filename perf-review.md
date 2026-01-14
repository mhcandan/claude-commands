Analyze code for performance bottlenecks and optimization opportunities.

## Performance Review Framework

Following "systems thinking" - performance issues in one area can create bottlenecks elsewhere.

### Analysis Areas

1. **Algorithmic Complexity**
   - Identify O(n²) or worse operations
   - Nested loops on large datasets
   - Recursive functions without memoization
   - Inefficient sorting/searching

2. **Database & I/O**
   - N+1 query patterns
   - Missing indexes (based on query patterns)
   - Unbounded queries without pagination
   - Synchronous I/O blocking operations
   - Connection pool sizing

3. **Memory & Resources**
   - Memory leaks (unclosed resources, retained references)
   - Large object allocations in loops
   - Unbounded caches or collections
   - String concatenation in loops

4. **Concurrency**
   - Thread safety issues
   - Lock contention
   - Async/await anti-patterns
   - Missing parallelization opportunities

5. **Caching Opportunities**
   - Repeated expensive computations
   - Frequently accessed static data
   - API response caching potential

6. **Frontend Specific (if applicable)**
   - Bundle size concerns
   - Render blocking resources
   - Unnecessary re-renders
   - Large DOM operations

## Output Format

```
## Performance Analysis Report

### Summary
[Overall performance health assessment]

### Bottlenecks Identified

#### Critical (High Impact)
| Location | Issue | Impact | Fix |
|----------|-------|--------|-----|

#### Moderate
| Location | Issue | Impact | Fix |
|----------|-------|--------|-----|

### Optimization Opportunities
1. [Specific optimization with expected improvement]

### Metrics Recommendations
- [Suggested metrics to track: cycle time, latency, throughput]

### Code Changes
[Provide optimized code snippets for critical issues]
```

Ask the user which file or module to analyze if not specified.
