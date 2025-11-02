# Code & Git History Review Instructions for GitHub Copilot

## Objective
Analyze the codebase and Git commit history to evaluate development processes (testing, build, deployment) and team collaboration patterns. Focus on process improvements rather than detailed code review, flagging only critical and obvious code quality issues.

## Output Requirements
**IMPORTANT**: All findings must be documented in a markdown file for the project knowledge base.

**File naming convention**: `team-name_repository-name_review_YYYY-MM-DD.md`

**Knowledge base structure**:
```
Knowledge Base/
├── Project Name/
│   ├── Team Alpha/
│   │   ├── repository-1_review_2025-11-02.md
│   │   ├── repository-2_review_2025-11-02.md
│   └── Team Beta/
│       ├── repository-3_review_2025-11-02.md
```

The analysis should be **business-logic agnostic** - focus on observable process patterns, not domain-specific implementation details.

---

## Platform-Specific Analysis

### GitHub-Specific Analysis

**Repository Insights:**
- Analyze GitHub Actions workflows in `.github/workflows/`
- Review CI/CD pipeline configuration (build, test, deploy stages)
- Check branch protection rules via API or settings
- Analyze GitHub Issues linking in commits (e.g., "fixes #123", "closes #456")
- Review use of GitHub Projects for task tracking
- Check Dependabot configuration and alerts
- Analyze PR templates (`.github/PULL_REQUEST_TEMPLATE.md`)
- Review code owners file (`.github/CODEOWNERS`)

**GitHub Actions Quality:**
```
CI/CD Health Check:
- Pipeline success rate: X%
- Average build time: X minutes
- Test failures frequency
- Deployment frequency to production
- Failed workflow patterns
- Security scanning enabled: Yes/No (Dependabot, CodeQL)
```

**GitHub Features Utilization:**
```
Platform Usage:
- Issues linked to commits: X%
- Draft PRs usage (good for WIP)
- PR reviews required before merge: Yes/No
- Status checks required: [list]
- Auto-merge enabled appropriately
- GitHub Discussions usage
```

### Bitbucket-Specific Analysis

**Repository Configuration:**
- Analyze Bitbucket Pipelines (`bitbucket-pipelines.yml`)
- Review branch permissions and merge checks
- Check Jira integration (commits with PROJ-123 format)
- Analyze pull request default reviewers configuration
- Review merge strategies (merge commit, squash, fast-forward)
- Check required approvals count
- Analyze build status reporting

**Bitbucket Pipelines Quality:**
```
Pipeline Analysis:
- Pipeline configuration quality
- Build success rate: X%
- Pipeline steps efficiency
- Parallel execution usage
- Caching strategy effectiveness
- Deployment pipelines to different environments
```

**Bitbucket Features Usage:**
```
Collaboration Features:
- Jira issue linking: X% of commits
- Required reviewers compliance
- Build status checks enabled
- Merge checks configuration
- Branch restrictions effectiveness
```

---

## Part 1: Process-Focused Analysis (PRIMARY FOCUS)

### 1.1 Testing Infrastructure & Practices ⭐ HIGH PRIORITY

**What to analyze:**
- Test automation setup and execution
- Test coverage trends (not absolute numbers, but direction)
- Testing tools and frameworks configuration
- Test execution in CI/CD pipeline
- Test data management approach

**For Java projects:**
```
Testing Process Assessment:

CI Test Execution:
- Tests run on every commit: [Yes/No]
- Test execution time: X minutes
- Flaky tests detected: [count if >5%]
- Test categories: [unit/integration/e2e present?]

Test Infrastructure:
- JUnit version: [4/5]
- Integration test approach: [TestContainers/H2/Real DB/None]
- Mocking framework: [Mockito/other/none]
- Test coverage tool: [JaCoCo/Cobertura/None]
- Coverage trend: [improving/stable/declining]

Issues:
- Tests not running in CI: [critical if true]
- Very slow test suite (>10 min): [list if applicable]
- No integration tests: [flag if service has DB/external APIs]
- Tests commented out: [count if >5]
```

**For Angular projects:**
```
Testing Process Assessment:

CI Test Execution:
- Unit tests in CI: [Yes/No]
- E2E tests in CI: [Yes/No]
- Test execution time: X minutes
- Test framework: [Karma+Jasmine/Jest/other]

Test Infrastructure:
- E2E framework: [Cypress/Playwright/Protractor/None]
- Component testing approach: [TestBed/shallow/none]
- Coverage tool: [Istanbul/other/none]
- Visual regression tests: [Yes/No]

Issues:
- E2E tests missing for critical flows: [flag if no E2E]
- Tests skipped in CI: [critical]
- No coverage reporting: [flag]
- Outdated testing framework (Protractor): [migration needed]
```

**Output Priority:**
```
CRITICAL TESTING ISSUES:
- [List only serious problems: no tests, tests not running, major gaps]

TESTING PROCESS RECOMMENDATIONS:
1. [Specific, actionable improvements]
2. [Focus on quick wins]
3. [Long-term improvements]
```

---

### 1.2 Build & CI/CD Pipeline Analysis ⭐ HIGH PRIORITY

**What to analyze:**
- Build configuration quality
- CI/CD pipeline structure
- Build success rate and stability
- Deployment automation level
- Environment management

**GitHub + Java:**
```
Build & CI/CD Health:

Pipeline Configuration:
- GitHub Actions workflows: [count and purpose]
- Build tool: [Maven X.X / Gradle X.X]
- Build success rate (last 30 days): X%
- Average build time: X minutes
- Parallel execution: [Yes/No]

Build Quality Checks:
- Automated tests: [Yes/No]
- Code quality gates: [SonarQube/Checkstyle/None]
- Security scanning: [Dependabot/Snyk/OWASP/None]
- Artifact publishing: [configured/missing]

Deployment:
- Deployment automation: [Full/Partial/Manual]
- Environments: [dev/staging/prod configured]
- Deployment frequency: [X times per week]
- Rollback capability: [automated/manual/unclear]

Issues:
- Build failures >20%: [investigate instability]
- No deployment automation: [critical]
- Missing security scanning: [high priority]
- Build time >15 min: [optimization needed]
```

**GitHub + Angular:**
```
Build & CI/CD Health:

Pipeline Configuration:
- GitHub Actions workflows: [count and purpose]
- Node version: [X.X]
- Build success rate: X%
- Average build time: X minutes
- Caching strategy: [npm cache configured/missing]

Build Optimization:
- Production build configured: [Yes/No]
- AOT compilation: [enabled/disabled]
- Build optimizer: [enabled/disabled]
- Bundle size tracking: [Yes/No]

Deployment:
- Deployment target: [S3/Azure/Netlify/Vercel/Other]
- Deployment automation: [Full/Partial/Manual]
- Environment configs: [dev/staging/prod]
- Preview deployments for PRs: [Yes/No]

Issues:
- Production build not optimized: [critical]
- No bundle size monitoring: [recommend]
- Manual deployment process: [automation needed]
- Missing environment configurations: [flag]
```

**Bitbucket + Java:**
```
Build & CI/CD Health:

Bitbucket Pipelines:
- Pipeline file present: [Yes/No]
- Build success rate: X%
- Pipeline steps: [list: build/test/deploy]
- Caching configured: [dependencies/build artifacts]

Integration:
- Jira integration: [commit linking X%]
- Artifactory/Nexus: [artifact publishing configured]
- Deployment pipelines: [per environment]

Issues:
- Pipeline missing: [critical]
- No caching: [build time impact]
- Manual deployment: [automation opportunity]
```

**Bitbucket + Angular:**
```
Build & CI/CD Health:

Bitbucket Pipelines:
- Pipeline configuration: [present/missing]
- Build success rate: X%
- npm/yarn caching: [configured/missing]
- Build steps: [list]

Deployment:
- CDN deployment: [automated/manual]
- Environment variables: [managed via pipelines/unclear]
- Deployment frequency: X per week

Issues:
- Missing pipeline: [critical]
- No automated deployment: [high priority]
- Build not optimized: [flag]
```

**Output Priority:**
```
CRITICAL BUILD/DEPLOYMENT ISSUES:
- [List blockers: no CI, manual deployment, high failure rate]

BUILD PROCESS RECOMMENDATIONS:
1. [Immediate improvements]
2. [Automation opportunities]
3. [Performance optimizations]
```

---

### 1.3 Dependency Management & Security ⭐ MEDIUM PRIORITY

**What to analyze:**
- Dependency update frequency
- Security vulnerability management
- Automated dependency updates setup

**Java Projects:**
```
Dependency Health:

Security:
- Known vulnerabilities: [count from Dependabot/Snyk]
- Critical CVEs: [list if any]
- Last security update: [date]

Maintenance:
- Outdated dependencies (major versions): [count]
- Spring Boot version: [X.X.X - current/outdated/EOL]
- Java version: [8/11/17/21 - supported/EOL]
- Automated updates: [Dependabot/Renovate/None]

Issues:
- Critical security vulnerabilities: [list]
- EOL framework versions: [critical]
- No automated scanning: [recommend setup]
```

**Angular Projects:**
```
Dependency Health:

Security:
- npm audit vulnerabilities: [count by severity]
- Critical vulnerabilities: [list]
- Last security update: [date]

Maintenance:
- Angular version: [X.X - current/LTS/outdated]
- Outdated major dependencies: [count]
- Automated updates: [Dependabot/Renovate/None]

Issues:
- Critical npm vulnerabilities: [list]
- Very outdated Angular (<3 major versions): [migration needed]
- No automated scanning: [setup needed]
```

**Output Priority:**
```
CRITICAL SECURITY ISSUES:
- [Only list high/critical CVEs and EOL software]

DEPENDENCY RECOMMENDATIONS:
1. [Security fixes]
2. [Update automation setup]
3. [Major version upgrades if needed]
```

---

### 1.4 Code Quality - Only Obvious Issues 🔍 LOW PRIORITY

**IMPORTANT**: Do NOT perform deep code review. Flag only glaring issues that are immediately visible.

**What to flag (Java):**
- Empty catch blocks (code search: `catch.*\{\s*\}`)
- System.out.println in production code (should use logger)
- Hardcoded credentials/secrets (search for "password", "apiKey", etc.)
- SQL concatenation (SQL injection risk)
- Commented out code blocks (>20 lines)
- Very large files (>1000 lines)

```
Obvious Code Issues (Java):

Critical:
- Hardcoded secrets: [count and hint at locations - DO NOT expose values]
- SQL injection risks: [count if string concatenation in SQL]
- Empty catch blocks: [count if >10]

Maintainability:
- Very large classes (>1000 lines): [count]
- System.out.println usage: [count]
- Large blocks of commented code: [flag if widespread]

Note: Detailed code review not performed - focus is on processes.
```

**What to flag (Angular):**
- console.log statements in code (should be removed for production)
- Hardcoded API URLs (should use environment files)
- Very large components (>500 lines)
- Unsubscribed observables (search for `.subscribe(` without unsubscribe)
- Disabled ESLint rules (search for eslint-disable)

```
Obvious Code Issues (Angular):

Critical:
- Hardcoded API URLs: [count]
- Hardcoded credentials: [flag if found]
- Memory leak patterns: [count .subscribe without takeUntil/async pipe]

Maintainability:
- console.log statements: [count]
- Very large components (>500 lines): [count]
- Widespread eslint-disable: [flag if >20 instances]

Note: Detailed code review not performed - focus is on processes.
```

**Output:**
```
GLARING CODE ISSUES:
- [Only list obvious problems that jump out]
- [Maximum 5 items - this is not the focus]

Note: Comprehensive code review requires domain knowledge and is outside scope of this analysis.
```

---

## Part 2: Commit History & Git Analysis (HIGH FOCUS)

### 2.1 Basic Commit Quality Assessment

Analyze the last 500 commits for:

- **Commit Message Quality**: 
  - Flag messages <10 characters or generic ("fix", "update", "changes")
  - Check for conventional commit format (feat:, fix:, docs:, etc.)
  - Verify presence of issue/ticket references
  
- **Commit Size**:
  - Count commits with >20 files changed (too large)
  - Count commits with >500 lines changed
  - Identify commits mixing multiple concerns (e.g., feature + refactoring)

**Output Format:**
```
Basic Commit Quality Report (last 500 commits):
- Poor commit messages: X% (examples: [list 5 worst])
- Oversized commits: X% (threshold: >20 files)
- Commits without ticket references: X%
- Average commit size: X files, Y lines
```

---

### 2.2 Commit History Anomaly Detection ⚠️ **CRITICAL SECTION**

**IMPORTANT**: These patterns may indicate issues with development process, automated code generation tools, workflow problems, or potential misuse of version control.

---

#### 2.2.1 Duplicate & Repetitive Commits Analysis

**What to detect:**

1. **Identical Commit Messages (Multiple Times)**
   - Multiple commits (>5) with exactly same message
   - Pattern example: "Update code" appearing 47 times
   - "Fix bug", "Changes", "Update" repeated excessively
   
2. **Similar Commit Patterns**
   - Sequential commits with barely different messages
   - Example: "fix typo", "fix typo 2", "fix typo again"
   - May indicate: lack of atomic commits, rushed work, or automated tools

3. **Cherry-pick Detection**
   - Same commit hash or message appearing in multiple branches
   - Legitimate use: hotfixes to multiple versions
   - Anomaly: excessive cherry-picking indicates branching strategy issues

4. **Revert-Revert Chains**
   - Patterns like: commit → revert → revert revert → revert revert revert
   - Indicates: unstable code, unclear decisions, or panic fixes

**Analysis Commands:**
```bash
# Detect duplicate commit messages (most important check)
git log --pretty=format:"%s" -500 | sort | uniq -c | sort -rn | head -20

# Flag any message appearing >5 times
git log --pretty=format:"%s" -500 | sort | uniq -c | awk '$1 > 5' | sort -rn

# Detect revert chains
git log --oneline -500 | grep -i revert | wc -l

# Find sequential similar commits
git log --pretty=format:"%s" -500 | sort | uniq -c | sort -rn | awk '$1 > 3'
```

**Output:**
```
🔴 DUPLICATE COMMITS ANALYSIS:

Identical Message Repetition:
- "Update" - 47 occurrences (CRITICAL ANOMALY)
- "Fix" - 23 occurrences (CRITICAL ANOMALY)
- "Changes" - 15 occurrences (WARNING)
- "WIP" - 12 occurrences (WARNING - should be in feature branches)
- "feat: add feature" - 8 occurrences (INVESTIGATE)

Statistics:
- Total commits analyzed: 500
- Unique commit messages: X
- Duplicate rate: X% (healthy: >80% unique)
- Most duplicated: "{message}" (X times)

Revert Patterns:
- Total reverts: X (healthy: <5% of commits)
- Revert chains detected: X instances
- Most reverted file/module: [name]

🚨 POTENTIAL ROOT CAUSES:
- [ ] Automated code generation tool without proper commit messages
- [ ] Copy-paste development without proper Git discipline  
- [ ] Lack of commit message standards or review
- [ ] Developer using same message habitually
- [ ] Build system or CI committing automatically
- [ ] Junior developers not trained on Git best practices

RECOMMENDATION: Investigate top 3 most duplicated messages immediately.
```

---

#### 2.2.2 Commit Message Quality Issues

**What to detect:**

1. **Typos and Language Errors**
   - Common typos: "fiex", "upate", "teh", "hte", "comit", "bugifx"
   - Grammar mistakes indicating rushed commits
   - Inconsistent language (mix of English/Russian/other)
   - ALL CAPS messages (e.g., "FIX BUG NOW")

2. **Incomplete or Truncated Messages**
   - Single word commits: "Update", "Fix", "Changes", "Test"
   - Extremely short messages (<5 characters): "wip", "asd", "123"
   - Messages cut off mid-sentence (copy-paste errors)
   - Only emoji or special characters

3. **Unprofessional Messages**
   - Profanity or unprofessional language
   - Frustration expressions: "WTF", "this is stupid", "I hate this"
   - Passive-aggressive messages
   - Personal notes: "remind myself", "TODO for tomorrow"

4. **Auto-generated Without Context**
   - "WIP", "checkpoint", "save", "backup" used frequently
   - Merge commits without resolution context
   - "Merge branch 'master'" without additional info (hundreds of times)
   - IDE auto-generated messages unchanged

**Analysis Commands:**
```bash
# Detect very short messages
git log --pretty=format:"%s" -500 | awk 'length($0) < 10' | wc -l

# Find common typos
git log --pretty=format:"%s" -500 | grep -iE "(fiex|upate|comit|bugifx|teh|hte)" | wc -l

# Detect WIP/save patterns
git log --pretty=format:"%s" -500 | grep -iE "^(wip|checkpoint|save|temp|backup|test)$" | wc -l

# Find ALL CAPS commits
git log --pretty=format:"%s" -500 | grep -E "^[A-Z ]+$" | head -20

# Detect single-word commits
git log --pretty=format:"%s" -500 | awk 'NF==1' | sort | uniq -c | sort -rn
```

**Output:**
```
🟡 COMMIT MESSAGE QUALITY ISSUES:

Inadequate Messages:
- Single-word commits: X (examples: "Update", "Fix", "Changes", "Done")
- Very short (<10 chars): X commits (X% of total)
- Empty or whitespace-only: X commits
- Only numbers/symbols: X commits

WIP/Temporary Commits in Main Branch:
- "WIP" commits: X (should be squashed before merge)
- "checkpoint" / "save": X
- "temp" / "backup": X
→ ISSUE: Temporary commits should not be in main branch

Language Quality:
- Typos detected: X instances
  - "fiex" instead of "fix": Y times
  - "upate" instead of "update": Z times
  - "comit" instead of "commit": N times
- Mixed language commits: X (if English is standard)
- ALL CAPS messages: X (unprofessional)

Auto-generated Without Edit:
- Default merge messages: X (e.g., "Merge branch 'master'")
- IDE-generated unchanged: X
- Build system commits: X

Unprofessional Content:
- Profanity detected: X instances [DO NOT LIST EXPLICITLY]
- Frustration expressions: X instances
- Personal notes in commits: X

🚨 POTENTIAL ROOT CAUSES:
- [ ] No commit message template configured
- [ ] No pre-commit hooks for message validation
- [ ] Team not trained on commit message standards
- [ ] Developers committing directly without review
- [ ] CI/CD system committing with poor messages
- [ ] Time pressure leading to rushed commits

RECOMMENDATIONS:
1. IMMEDIATE: Implement commit message template (.gitmessage)
2. IMMEDIATE: Add pre-commit hook for message validation (min 20 chars, no typos)
3. SHORT-TERM: Team training on conventional commits
4. SHORT-TERM: Require ticket references in commits (e.g., PROJ-123)
```

---

#### 2.2.3 Commit Frequency Anomalies

**What to detect:**

1. **Unusually High Commit Volume**
   - >50 commits per day from single developer
   - >100 commits per week consistently
   - May indicate: automated commits, misconfigured tool, very granular commits

2. **Burst Commit Patterns**
   - 20+ commits within same hour
   - 50+ commits on same day
   - Sudden spike after long silence
   - May indicate: mass rebasing, automated tool, batch commit after offline work

3. **Timestamp Anomalies**
   - Commits consistently at 3-5 AM (unusual hours)
   - All commits at exact same time (HH:MM:00)
   - Future timestamps (clock misconfiguration)
   - Very old timestamps suddenly appearing
   - Commits every few minutes 24/7 (bot behavior)

4. **Commit Gaps & Irregular Patterns**
   - No commits for >2 weeks, then 100 commits in 1 day
   - "Weekend warrior" pattern (only commits on weekends)
   - Commits only during business hours vs random times
   - Long gaps followed by massive bursts

**Analysis Commands:**
```bash
# Commits per day per author
git log --pretty=format:"%an %ad" --date=short -500 | \
  awk '{print $1,$2}' | sort | uniq -c | sort -rn | head -20

# Find burst patterns (>20 commits same hour)
git log --pretty=format:"%an %ad" --date=format:"%Y-%m-%d %H" -500 | \
  awk '{print $1,$2,$3}' | sort | uniq -c | awk '$1 > 20' | sort -rn

# Commits by hour of day
git log --pretty=format:"%ad" --date=format:"%H" -500 | \
  sort | uniq -c | sort -k2

# Detect unusual hours (2-5 AM)
git log --pretty=format:"%an %ad" --date=format:"%H" -500 | \
  awk '$2 >= 2 && $2 <= 5' | wc -l

# Find gaps (days without commits)
git log --pretty=format:"%ad" --date=short | uniq | \
  awk '{if (prev) {diff = (NR-1) - prev_nr; if (diff > 1) print prev " to " $1 " (" diff-1 " days gap)"} prev=$1; prev_nr=NR}'

# Commits per author per day average
git log --pretty=format:"%an %ad" --date=short | \
  awk '{commits[$1" "$2]++} END {for (key in commits) print key, commits[key]}' | \
  awk '{sum+=$3; count++} END {print sum/count " commits/day average"}'
```

**Output:**
```
🔴 COMMIT FREQUENCY ANOMALIES:

High Volume Patterns:
- Developer "John Doe": 85 commits/day average (CRITICAL ANOMALY if >50)
- Developer "Jane Smith": 156 commits on 2025-10-15 (INVESTIGATE)
- Highest single-day count: 203 commits on 2025-09-20

Burst Patterns Detected:
DATE/TIME                    | COMMITS | AUTHOR      | STATUS
2025-10-15 14:00            | 47      | John Doe    | 🚨 ANOMALY
2025-09-20 09:00            | 38      | Build Bot   | ⚠️ Automated
2025-08-10 16:00            | 25      | Jane Smith  | ⚠️ Check

Timestamp Anomalies:
- Commits at 3-5 AM: X commits (Y% of total)
- Exact minute (:00) timestamps: X commits (possible automation)
- Future timestamps: X commits (CRITICAL - check local clocks)
- Weekend commits: X% (compare to weekday: Y%)
- Commits every 5 minutes pattern: Detected for user [name]

Commit Gaps:
- Longest gap: 45 days (2025-07-01 to 2025-08-15)
- Gaps >2 weeks: X instances
- Pattern: [regular/irregular/burst-based/concerning]
- Average time between commits: X hours

Irregular Patterns:
- "Weekend warrior": User [name] - 80% commits on Sat/Sun
- "Night owl": User [name] - 70% commits between 10 PM - 3 AM  
- "Burst committer": User [name] - 5 commits total, all in 1 hour

Frequency Distribution:
- 0-5 commits/day: X developers (healthy)
- 6-20 commits/day: X developers (normal)
- 21-50 commits/day: X developers (monitor)
- >50 commits/day: X developers (INVESTIGATE)

🚨 POTENTIAL ROOT CAUSES:
- [ ] Automated tool (IDE, build system) committing on every save
- [ ] Developer not using atomic commit principle (too granular)
- [ ] Mass code generation or refactoring tools
- [ ] Rebasing/history rewriting creating burst appearance
- [ ] Offline work being committed in batch
- [ ] Bot or CI system committing as developer
- [ ] Copy-paste from another repository
- [ ] Clock/timezone misconfiguration

RECOMMENDATIONS:
1. IMMEDIATE: Interview developers with >50 commits/day pattern
2. IMMEDIATE: Check for automated tools committing unintentionally
3. SHORT-TERM: Establish commit frequency guidelines (3-8 commits/day ideal)
4. SHORT-TERM: Review IDE configurations across team
5. LONG-TERM: Implement commit hooks to prevent burst patterns
```

---

#### 2.2.4 Author Identity Anomalies

**What to detect:**

1. **Duplicate/Inconsistent Author Identities**
   - Same person with multiple names: "John Doe", "john.doe", "J. Doe", "jdoe", "John D."
   - Same person with multiple emails: personal + work + old company
   - Case inconsistencies: "john doe" vs "John Doe"
   - Nickname vs real name confusion

2. **Generic or Suspicious Usernames**
   - System accounts: "root", "admin", "user", "developer", "unknown"
   - Placeholder names: "User 1", "New User", "Your Name"
   - Missing email addresses: "user@localhost", "user@example.com"
   - Non-company email domains for company projects

3. **Single Massive Contributor (Bus Factor)**
   - One person: >80% of all commits
   - Two people: >90% of commits
   - Indicates: knowledge silo, lack of code ownership distribution, single point of failure

4. **Missing or Wrong Attribution**
   - CI/CD system committing as generic user
   - Pair programming without co-author attribution
   - Code review commits attributed to wrong person

**Analysis Commands:**
```bash
# List all unique author identities
git log --pretty=format:"%an <%ae>" -500 | sort | uniq

# Find similar names (case-insensitive grouping)
git log --pretty=format:"%an" -500 | \
  awk '{print tolower($0)}' | sort | uniq -c | sort -rn

# Detect generic usernames
git log --pretty=format:"%an <%ae>" -500 | \
  grep -iE "(root|admin|user|developer|unknown|test)@"

# Calculate Bus Factor (commits per author)
git log --pretty=format:"%an" -500 | sort | uniq -c | sort -rn | \
  awk '{sum+=$1; print $0; counts[NR]=$1} END {
    for (i=1; i<=NR; i++) {
      cumsum += counts[i];
      if (cumsum/sum >= 0.5 && bus_factor == 0) bus_factor = i;
      if (cumsum/sum >= 0.8) {eighty = i; break}
    }
    print "Bus Factor (50% knowledge):", bus_factor;
    print "80% of work by:", eighty, "people"
  }'

# Find email domain distribution
git log --pretty=format:"%ae" -500 | \
  sed 's/.*@//' | sort | uniq -c | sort -rn
```

**Output:**
```
🟡 AUTHOR IDENTITY ANOMALIES:

Identity Inconsistencies Detected:
USER: John Doe (Same Person, Different Git Configs)
- "John Doe <john.doe@company.com>" - 150 commits
- "john.doe <john.doe@company.com>" - 80 commits
- "J.Doe <john@company.com>" - 45 commits
- "jdoe <john.doe@oldcompany.com>" - 20 commits
→ TOTAL: 295 commits from same person with 4 different identities

USER: Jane Smith
- "Jane Smith <jane@personal.com>" - 60 commits (personal email - issue?)
- "Jane Smith <jane.smith@company.com>" - 120 commits
→ ISSUE: Using personal email for company code

Generic/Suspicious Usernames:
- "root <root@localhost>" - 25 commits (CONFIGURE PROPER IDENTITY)
- "admin <admin@example.com>" - 15 commits
- "developer <dev@localhost>" - 8 commits
- "Your Name <your.email@example.com>" - 3 commits (UNCONFIGURED GIT)
- Missing/invalid emails: 12 commits

Email Domain Analysis:
- @company.com: 450 commits (expected)
- @gmail.com: 45 commits (personal - investigate)
- @oldcompany.com: 20 commits (former employer - update)
- @localhost: 18 commits (misconfigured - fix)

Bus Factor Analysis (CRITICAL):
- Developer A: 385 commits (77% of total) 🚨 CRITICAL RISK
- Developer B: 65 commits (13%)
- Developer C: 30 commits (6%)
- Developer D: 20 commits (4%)
→ Bus Factor = 1 (ONE PERSON HAS MAJORITY OF KNOWLEDGE)
→ If Developer A leaves, project is at severe risk

Contribution Distribution:
- Top 1 developer: 77% of commits (RISK if >60%)
- Top 2 developers: 90% of commits (RISK if >80%)
- Top 3 developers: 96% of commits
- Active contributors: 4 people (RISK if <5 for team project)

Inactive or Minimal Contributors:
- 3 developers with <5 commits each (onboarding issues?)
- 2 developers with no commits in 90 days (left team?)

🚨 POTENTIAL ROOT CAUSES:
- [ ] Multiple machines with different Git configurations
- [ ] Developers not configuring Git properly on new machines
- [ ] CI/CD system committing with generic identity
- [ ] Pair programming without proper co-author attribution
- [ ] Former employees' Git configs still in use
- [ ] Knowledge concentration - only 1-2