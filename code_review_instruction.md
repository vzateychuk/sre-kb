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

## Combined Platform & Technology Matrix

Use this matrix to guide platform-specific checks for each technology stack.

### GitHub + Java Analysis Checklist
✓ Analyze GitHub Actions for Maven/Gradle builds (`.github/workflows/`)
✓ Check Dependabot for Java dependency updates (Maven/Gradle)
✓ Review Java-specific GitHub workflows (SonarQube/CodeQL integration, JaCoCo reports)
✓ Check GitHub Packages usage for artifact publishing

### GitHub + Angular Analysis Checklist
✓ Analyze GitHub Actions for Angular builds (`ng build --prod`, `ng test`)
✓ Check npm audit integration in workflows
✓ Review Lighthouse CI integration for performance
✓ Analyze bundle size tracking comments on PRs
✓ Check GitHub Pages deployment for Angular apps (if applicable)

### Bitbucket + Java Analysis Checklist
✓ Analyze Bitbucket Pipelines for Maven/Gradle (`bitbucket-pipelines.yml`)
✓ Check Jira issue integration with Java commits (PROJ-123)
✓ Review Artifactory/Nexus integration as pipeline steps
✓ Analyze deployment pipelines for Spring Boot apps to environments
✓ Check SonarQube integration via pipelines

### Bitbucket + Angular Analysis Checklist
✓ Analyze Bitbucket Pipelines for npm/Angular CLI
✓ Check environment-specific Angular builds (using variables)
✓ Review deployment to S3/CDN via pipelines
✓ Analyze artifact storage for Angular `dist` files

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
### 2.3 Branching Strategy & Collaboration Patterns Analysis

What to analyze:

Identify the branching model (Trunk-Based, Git Flow, GitHub Flow)

Check main branch name (main, master, development)

Analyze Pull Request (PR) lifecycle: time to merge, review comments

Check for stale branches (older than 3 months, unmerged)

Analysis Commands:

```Bash

# List all remote branches
git branch -r

# List branches by last commit date (to find stale branches)
git branch -r --sort=-committerdate | head -20

# Check main branch name (common names)
git branch -r | grep -E "(main|master|development|production)"

# Get 10 most recently merged branches (to check naming conventions)
git log --merges --pretty=format:"%s" -10 | grep "Merge pull request"
```


🔵 BRANCHING STRATEGY & COLLABORATION:

Branching Model:
- Primary model: [Trunk-Based / Git Flow / GitHub Flow / Unclear]
- Main branch: [name]
- Feature branch prefix: [e.g., feat/ / fix/ / feature-]
- Release branches used: [Yes/No]

Collaboration Patterns:
- Average PR lifespan: [X days/hours - if available]
- PR reviews required: [Yes/No - from platform analysis]
- CODEOWNERS file: [Present/Missing/Well-configured]
- PR Templates used: [Yes/No/Poorly]

Branch Hygiene:
- Total remote branches: X
- Stale branches (>3 months unmerged): X (LIST 5 OLDEST)
- Merged branches deleted: [Yes/No/Partially]

🚨 POTENTIAL ROOT CAUSES:
- [ ] No defined branching strategy (e.g., long-lived feature branches)
- [ ] Lack of branch cleanup process
- [ ] PRs merged without adequate review
- [ ] Bottlenecks in review process (long PR lifespans)

RECOMMENDATIONS:
1. Define and document a clear branching strategy.
2. Implement automated stale branch detection/cleanup.
3. Enforce PR templates and CODEOWNERS.

### 2.4 Code Review Practices

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

### 2.5 Team Collaboration Patterns

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

### 2.6 Release & Deployment Patterns

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
## Part 4: Synthesis & Final Report Structure
Objective: Synthesize all findings from into a single, actionable report. Use the markdown file name convention specified in "Output Requirements".

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

### **CI/CD**

### **Security**

### **Testing**

### Git & Collaboration

- **Git Hygiene**
- Commits w/o Ticket
- Oversized Commits
- Bus Factor
- Duplicate Commit Messages

## Recommendations by Priority
[Section 3.1 priority matrix]

## Implementation Roadmap
[Section 3.3 phased approach]

## Appendix
- Detailed metrics tables
- Examples of good/bad patterns found
- Tool recommendations
```

The example of the final output structure.

```
# Development Process Review Report

**Repository**: [repository-name]
**Team**: [team-name]
**Platform**: [GitHub / Bitbucket]
**Technology**: [Java / Angular]
**Analysis Date**: [YYYY-MM-DD]

## Executive Summary

* **Overall Process Health**: [Good / Fair / Needs Improvement]
* **Key Positive Findings**:
    1.  [e.g., High test coverage, fast builds, good commit hygiene]
    1.  [e.g., Excellent CI/CD automation]
* **Top 3 Critical Issues**:
    1.  [e.g., Critical security vulnerabilities found]
    1.  [e.g., No automated deployment process (manual deploys)]
    1.  [e.g., Git history anomaly: 80% commits from "root" user]

## Priority Recommendations

### CRITICAL
* [e.g., Patch Log4Shell vulnerability (CVE-XXXX-XXXX)]
* [e.g., Fix hardcoded secrets found in MyController.java]
* [e.g., Investigate "John Doe" 85 commits/day anomaly]

### HIGH PRIORITY
* [e.g., Enable automated security scanning (Dependabot/Snyk)]
* [e.g., Automate deployment to staging environment]
* [e.g., Implement commit message standards and pre-commit hooks]
* [e.g., Enforce branch protection rules (require 1 reviewer)]

### MEDIUM PRIORITY
* [e.g., Upgrade from Java 11 to 17 (EOL in 2024)]
* [e.g., Implement integration testing with TestContainers]
* [e.g., Add bundle size tracking to Angular CI pipeline]

## Detailed Findings: Process & CI/CD

### Testing Infrastructure (Priority: HIGH)
* [Paste findings from "1.1 Testing Process Assessment"]
* **Issues**: [List "CRITICAL TESTING ISSUES"]
* **Recommendations**: [List "TESTING PROCESS RECOMMENDATIONS"]

### Build & CI/CD Pipeline (Priority: HIGH)
* [Paste findings from "1.2 Build & CI/CD Health"]
* **Issues**: [List "CRITICAL BUILD/DEPLOYMENT ISSUES"]
* **Recommendations**: [List "BUILD PROCESS RECOMMENDATIONS"]

### Dependency Management & Security (Priority: MEDIUM)
* [Paste findings from "1.3 Dependency Health"]
* **Issues**: [List "CRITICAL SECURITY ISSUES"]
* **Recommendations**: [List "DEPENDENCY RECOMMENDATIONS"]

### Obvious Code Quality Issues (Priority: LOW)
* [Paste findings from "1.4 Obvious Code Issues"]
* **Note**: Comprehensive code review was out of scope.

## Detailed Findings: Git & Collaboration

### Commit History & Anomaly Detection (Priority: HIGH)
* **Basic Quality**:
* **Duplicate Commits**:
* **Message Quality**:
* **Frequency Anomalies**:
* **Author Anomalies**:

### Branching Strategy (Priority: MEDIUM)
```

## Notes for AI Analysis

- Maintain objectivity; report facts without blame
- Provide context: explain *why* each practice matters
- Include both quantitative metrics and qualitative observations
- Reference specific files/commits as evidence
- Compare against industry benchmarks when possible
- Focus on actionable items, not just problems
- Consider team size and project maturity in recommendations
- The report should not contains any emoj
- Documents MUST looks like prepared by person (not AI)