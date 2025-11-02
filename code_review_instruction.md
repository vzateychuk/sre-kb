# Code & Git History Review Instructions for GitHub Copilot

## Objective
Analyze the codebase and Git commit history to evaluate adherence to software development best practices and provide actionable recommendations for process improvement.

## Part 1: Static Code Analysis

### 1.1 Architecture & Design Evaluation

Analyze the codebase structure and provide findings on:

- **SOLID Principles Compliance**: Check for Single Responsibility, Open/Closed, Liskov Substitution, Interface Segregation, and Dependency Inversion violations
- **Layered Architecture**: Verify proper separation of concerns (controllers, services, repositories/DAOs, domain models)
- **Package Dependencies**: Identify circular dependencies between packages using dependency graphs
- **Code Smells**: Flag God classes (>500 lines), long methods (>50 lines), excessive parameters (>5), deep nesting (>4 levels)
- **API Design**: Evaluate consistency of REST endpoints, method signatures, and public APIs

**Output Format:**
```
Architecture Issues:
- [CRITICAL/HIGH/MEDIUM/LOW] Description of issue
- Location: package/class names
- Impact: explanation of consequences
- Recommendation: specific action to take
```

### 1.2 Code Quality Metrics

Calculate and report:

- **Code Coverage**: Identify modules with <60% test coverage
- **Cyclomatic Complexity**: Flag methods with complexity >10
- **Code Duplication**: Detect duplicated blocks (>6 lines repeated)
- **Dead Code**: Find unused private methods, unreferenced classes
- **Exception Handling**: Check for empty catch blocks, generic exception catching, missing error logging
- **Security Issues**: Identify hardcoded credentials, SQL injection risks, XSS vulnerabilities

**Output Format:**
```
Quality Metrics Summary:
- Average test coverage: X%
- Classes with high complexity: [list with complexity scores]
- Duplication rate: X%
- Critical security issues: [count and severity]

Detailed Findings:
[List specific issues with file:line references]
```

### 1.3 Dependencies & Technical Debt

Review:

- **Outdated Dependencies**: List libraries that are >2 major versions behind
- **Vulnerable Dependencies**: Identify known CVEs in used libraries
- **Unused Dependencies**: Find dependencies declared but not imported
- **TODO/FIXME Comments**: Catalog technical debt markers with age (commit date)
- **Temporary Workarounds**: Search for comments containing "hack", "temporary", "workaround"

**Output Format:**
```
Technical Debt Inventory:
1. Outdated Dependencies: [library: current version -> latest version]
2. Security Vulnerabilities: [CVE IDs with severity]
3. TODO Items: [count by age: <1 month, 1-6 months, >6 months]
4. Workarounds: [list with context and age]
```

### 1.4 Documentation Quality

Assess:

- **JavaDoc Coverage**: Percentage of public methods/classes with documentation
- **README Completeness**: Check for setup instructions, architecture overview, contribution guidelines
- **Code Comments**: Ratio of comment lines to code lines (ideal: 10-20%)
- **Architecture Documentation**: Presence of diagrams, ADRs (Architecture Decision Records)

**Output Format:**
```
Documentation Status:
- JavaDoc coverage: X%
- README sections present: [checklist]
- Over-commented files: [list if comment ratio >30%]
- Under-documented complex modules: [list]
```

## Part 2: Git History Analysis

### 2.1 Commit Quality Assessment

Analyze the last 500 commits for:

- **Commit Message Quality**: 
  - Flag messages <10 characters or generic ("fix", "update", "changes")
  - Check for conventional commit format (feat:, fix:, docs:, etc.)
  - Verify presence of issue/ticket references
  
- **Commit Size**:
  - Count commits with >20 files changed (too large)
  - Count commits with >500 lines changed
  - Identify commits mixing multiple concerns (e.g., feature + refactoring)

- **Commit Frequency**:
  - Calculate average commits per day per developer
  - Identify patterns of "Friday night deployments" or irregular commits

**Output Format:**
```
Commit Quality Report (last 500 commits):
- Poor commit messages: X% (examples: [list 5 worst])
- Oversized commits: X% (threshold: >20 files)
- Commits without ticket references: X%
- Average commit size: X files, Y lines

Recommendations:
[Specific suggestions for improvement]
```

### 2.2 Branching Strategy Analysis

Examine:

- **Branch Patterns**: Identify if team uses feature branches, gitflow, trunk-based development
- **Branch Lifetime**: Calculate average time from branch creation to merge
- **Merge vs Rebase**: Ratio of merge commits vs rebased commits
- **Direct Commits to Main**: Count commits directly to main/master branch
- **Stale Branches**: List branches not updated in >30 days

**Output Format:**
```
Branching Analysis:
- Strategy detected: [gitflow/feature-branch/trunk-based/unclear]
- Average branch lifetime: X days
- Long-lived branches (>14 days): [count and names]
- Direct main commits: X% of total
- Stale branches: [count]

Issues Identified:
[List problematic patterns]
```

### 2.3 Code Review Practices

Analyze Pull Requests:

- **PR Metrics**:
  - Average time from creation to merge
  - Average number of comments per PR
  - Percentage of PRs with 0 comments (rubber-stamp approvals)
  - PR size distribution (small <200 lines, medium <500, large >500)

- **Review Participation**:
  - List reviewers and number of reviews conducted
  - Identify if reviews are distributed or concentrated
  - Check if PRs are approved by >1 person

- **Iteration Patterns**:
  - Count average revisions per PR
  - Identify PRs with >5 revision cycles

**Output Format:**
```
Code Review Health:
- Average PR merge time: X hours/days
- PRs merged without review: X%
- Large PRs (>500 lines): X%
- Review distribution: [name: review count]
- Bottlenecks: [identify slow reviewers or approval patterns]

Recommendations:
- [Specific process improvements]
```

### 2.4 Team Collaboration Patterns

Analyze contributor data:

- **Code Ownership**:
  - Calculate Bus Factor (minimum number of people who know >50% of codebase)
  - Identify modules with single contributor (>80% commits)
  - Map which developers work on which modules

- **Workload Distribution**:
  - Count commits per author in last 90 days
  - Identify imbalances (one person >50% of commits)

- **Merge Conflicts**:
  - Frequency of merge conflicts by file/module
  - Identify conflict hotspots

**Output Format:**
```
Team Collaboration Report:
- Bus Factor: X people (RISK if <3)
- Single-owner modules: [list]
- Commit distribution: [name: percentage]
- Conflict hotspots: [files with >5 conflicts in 90 days]

Collaboration Issues:
[List knowledge silos and bottlenecks]
```

### 2.5 Release & Deployment Patterns

Review:

- **Release Frequency**: Count tagged releases, calculate average time between releases
- **Hotfix Pattern**: Identify emergency commits outside normal flow
- **Rollback History**: Search for "revert" commits, count frequency
- **Breaking Changes**: Track commits that modify public APIs

**Output Format:**
```
Release Management:
- Average release cycle: X days
- Hotfixes in last 90 days: X (indicates instability if >10%)
- Rollbacks: X occurrences
- Breaking changes: [list with dates]

Stability Indicators:
[Assessment of release maturity]
```

## Part 3: Synthesis & Recommendations

### 3.1 Priority Matrix

Categorize findings:

```
CRITICAL (Fix Immediately):
- Security vulnerabilities
- Code with >20 cyclomatic complexity
- Modules with <30% test coverage and high churn

HIGH (Address in Next Sprint):
- Architectural violations
- Large PRs (>500 lines)
- Single points of failure (Bus Factor = 1)

MEDIUM (Plan for Next Quarter):
- Outdated dependencies (no CVEs)
- Documentation gaps
- Code duplication >10%

LOW (Continuous Improvement):
- Code style inconsistencies
- Missing JavaDocs on internal methods
```

### 3.2 Actionable Recommendations

For each issue category, provide:

1. **Current State**: Metrics and specific examples
2. **Target State**: Measurable goals
3. **Implementation Steps**: Specific actions with tools/processes
4. **Expected Impact**: Benefits to quality, velocity, maintainability
5. **Effort Estimate**: Time/resources required

**Example Template:**
```
Issue: Low Test Coverage (current: 45%)
Target: >70% coverage for critical modules

Steps:
1. Implement JaCoCo with PR checks blocking <60% coverage
2. Dedicate 20% of sprint capacity to writing tests for modules X, Y, Z
3. Conduct testing workshop for team

Impact: 
- Reduce production bugs by ~40%
- Enable safer refactoring
- Improve confidence in deployments

Effort: 2-3 sprints for initial improvement
```

### 3.3 Process Improvement Roadmap

Create a phased approach:

**Phase 1 (Month 1): Quick Wins**
- Enable automated code quality checks (SonarQube, Checkstyle)
- Implement commit message template
- Set PR size guidelines (<300 lines)

**Phase 2 (Months 2-3): Process Standardization**
- Adopt branching strategy (recommend trunk-based or gitflow)
- Establish code review SLAs
- Implement automated dependency scanning

**Phase 3 (Months 4-6): Cultural Change**
- Rotate code ownership
- Conduct architecture review sessions
- Build comprehensive test suite

## Output Structure

Provide final report in this format:

```markdown
# Development Process Review Report
**Repository**: [name]
**Analysis Date**: [date]
**Commits Analyzed**: [count, date range]

## Executive Summary
- Overall Code Quality Score: X/10
- Process Maturity Level: [1-5]
- Critical Issues: [count]
- Top 3 Recommendations

## Detailed Findings

### Code Quality
[Section 1.1-1.4 findings]

### Git & Collaboration
[Section 2.1-2.5 findings]

### Team Health
[Section 2.4 findings]

## Recommendations by Priority
[Section 3.1 priority matrix]

## Implementation Roadmap
[Section 3.3 phased approach]

## Appendix
- Detailed metrics tables
- Examples of good/bad patterns found
- Tool recommendations
```

## Notes for AI Analysis

- Maintain objectivity; report facts without blame
- Provide context: explain *why* each practice matters
- Include both quantitative metrics and qualitative observations
- Reference specific files/commits as evidence
- Compare against industry benchmarks when possible
- Focus on actionable items, not just problems
- Consider team size and project maturity in recommendations