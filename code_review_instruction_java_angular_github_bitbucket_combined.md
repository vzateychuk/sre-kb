# Code & Git History Review Instructions for GitHub Copilot

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

## Technology-Specific Analysis: Java

### Java Code Quality Checks

**1. Java-Specific Architecture Patterns**

Analyze:
- **Spring Framework Usage** (if applicable):
  - Proper use of `@Service`, `@Repository`, `@Controller` stereotypes
  - Dependency injection patterns (constructor vs field injection)
  - Transaction management (`@Transactional` usage)
  - Configuration management (`@ConfigurationProperties` vs hardcoded values)
  
- **Jakarta EE / Java EE Patterns** (if applicable):
  - EJB usage patterns
  - CDI bean scopes
  - JPA entity design
  
- **Dependency Injection**:
  - Constructor injection preferred over field injection
  - Avoid circular dependencies
  - Interface-based design for testability

**Output:**
```
Java Architecture Assessment:
- DI Pattern: [Constructor-based: X% | Field-based: Y%]
- Spring stereotypes misuse: [list violations]
- Configuration externalization: X% hardcoded values
- Transaction boundaries: [issues found]
```

**2. Java Code Quality Metrics**

Check for:
- **Exception Handling**:
  - Empty catch blocks
  - Generic `Exception` catching instead of specific types
  - Proper exception logging
  - Custom exception hierarchy design
  
- **Resource Management**:
  - Use of try-with-resources for AutoCloseable
  - Proper connection/stream closing
  - Thread pool management
  
- **Java Best Practices**:
  - Immutability usage (`final` fields, immutable collections)
  - Proper `equals()`, `hashCode()`, `toString()` implementation
  - Enum usage for constants instead of static finals
  - Stream API usage vs traditional loops (for Java 8+)
  - Optional usage to avoid null checks
  
- **Concurrency Issues**:
  - Thread-safety of shared resources
  - Proper synchronization
  - Use of concurrent collections
  - Visibility issues (missing `volatile`)

**Output:**
```
Java Quality Report:
- Empty catch blocks: [count and locations]
- Resources not properly closed: [list]
- Missing @Override annotations: [count]
- Mutable static fields: [list - potential thread-safety issues]
- Non-thread-safe shared state: [critical issues]
- Stream API adoption rate: X%
```

**3. Java Testing Practices**

Evaluate:
- **Test Framework Usage**:
  - JUnit 5 (Jupiter) vs JUnit 4 usage
  - Mockito usage patterns
  - TestContainers for integration tests
  - AssertJ for fluent assertions
  
- **Test Quality**:
  - Test naming conventions (`should_XXX_when_YYY`)
  - Arrange-Act-Assert pattern compliance
  - Test data builders vs direct instantiation
  - Avoid test interdependencies
  
- **Spring Testing**:
  - `@SpringBootTest` vs `@WebMvcTest` / `@DataJpaTest` (use slicing)
  - MockBean vs Mockito mocks
  - Test configuration management

**Output:**
```
Java Testing Assessment:
- JUnit version: [4 or 5]
- Test slicing usage: X% (Spring Boot)
- Mockito usage: [patterns, anti-patterns]
- Integration test coverage: X%
- Test naming consistency: X%
- Tests using real DB vs in-memory: [ratio]
```

**4. Java Build & Dependencies**

Analyze:
- **Maven / Gradle Configuration**:
  - Maven: `pom.xml` - dependency management, plugin versions
  - Gradle: `build.gradle` - dependencies, task configuration
  - Multi-module project structure
  - Dependency version conflicts
  
- **Dependency Management**:
  - Outdated dependencies (check Maven Central / Gradle)
  - Vulnerable dependencies (CVEs)
  - Unused declared dependencies
  - Undeclared dependencies (used but not declared)
  - Dependency scopes correctness (compile vs provided vs test)
  
- **Build Plugins**:
  - Code coverage (JaCoCo)
  - Static analysis (SpotBugs, PMD, Checkstyle)
  - Dependency check plugins
  - Enforcer plugin rules (Maven)

**Output:**
```
Java Build Health:
Build Tool: [Maven X.X / Gradle X.X]

Dependencies:
- Total dependencies: X
- Outdated (minor): X
- Outdated (major): X
- Vulnerable: X (CVE details)
- Unused: X

Build Configuration:
- Code coverage plugin: [enabled/missing]
- Static analysis: [tools enabled]
- Dependency check: [enabled/missing]
- Build reproducibility: [deterministic/non-deterministic]
```

**5. Java-Specific Code Smells**

Flag:
- God classes (>500 lines, >20 methods)
- Utility classes not final with private constructor
- Mutable Date usage (should use `java.time.*`)
- Raw types usage (generics without type parameters)
- String concatenation in loops (should use `StringBuilder`)
- Premature optimization (complex code without profiling)
- Servlet anti-patterns (if using servlets directly)

**Output:**
```
Java Anti-Patterns Detected:
- Legacy Date API usage: [count locations]
- Raw types: [list]
- String concatenation in loops: [list]
- Non-final utility classes: [list]
- Servlet instance variables: [thread-safety issues]
```

**6. Java Frameworks & Libraries Best Practices**

**Spring Boot Specific:**
```
Spring Boot Assessment:
- Spring Boot version: X.X.X [outdated/current]
- Auto-configuration usage: [appropriate/excessive]
- Profile management: [environments configured]
- Actuator endpoints: [enabled and secured]
- Logging configuration: [proper externalization]
- Application properties vs YAML: [consistency]
- Custom starters: [if applicable, quality check]
```

**Hibernate/JPA Specific:**
```
JPA/Hibernate Review:
- N+1 query problems: [detected locations]
- Lazy loading issues: [LazyInitializationException risks]
- Cartesian product in queries: [detected]
- Missing indexes on foreign keys: [list]
- Entity graph usage for performance
- Query optimization (JPQL vs Criteria vs Native)
```

---

## Technology-Specific Analysis: Angular

### Angular Code Quality Checks

**1. Angular Architecture Patterns**

Analyze:
- **Module Organization**:
  - Feature modules structure
  - Shared vs Core modules separation
  - Lazy loading implementation
  - Module imports (avoid importing everything in AppModule)
  
- **Component Design**:
  - Smart vs Dumb components pattern
  - Component size (<400 lines recommended)
  - Single Responsibility Principle per component
  - Proper use of `@Input()` and `@Output()`
  
- **State Management**:
  - Use of services for shared state
  - RxJS patterns (proper subscription management)
  - NgRx/Akita/other state management library usage (if applicable)
  
- **Routing**:
  - Route guards implementation
  - Route lazy loading
  - Resolver usage for data fetching

**Output:**
```
Angular Architecture Assessment:
- Feature modules count: X
- Lazy loaded modules: X%
- Average component size: X lines
- Smart/Dumb ratio: [assessment]
- State management: [service-based / NgRx / other]
- Components with >400 lines: [list]
```

**2. Angular Best Practices**

Check for:
- **RxJS Subscription Management**:
  - Unsubscribed observables (memory leaks)
  - Use of `async` pipe vs manual subscribe
  - `takeUntil` / `take` / `first` operators usage
  - Subject vs BehaviorSubject usage appropriateness
  
- **Change Detection Optimization**:
  - `OnPush` change detection strategy usage
  - Immutable data patterns
  - `trackBy` functions in `*ngFor`
  - Avoiding function calls in templates
  
- **Template Best Practices**:
  - Template complexity (avoid business logic in templates)
  - Proper use of structural directives
  - Safe navigation operator usage
  - Template reference variables usage

**Output:**
```
Angular Code Quality:
- Memory leak risks (unsubscribed): [count and locations]
- OnPush usage: X% of components
- TrackBy in ngFor: X% usage
- Template complexity issues: [list]
- Async pipe adoption: X% vs manual subscribe
```

**3. TypeScript Quality (Angular Context)**

Evaluate:
- **Type Safety**:
  - `any` type usage (should be minimal)
  - Proper interface definitions
  - Strict mode enabled in `tsconfig.json`
  - Type guards usage
  
- **Modern TypeScript Features**:
  - Optional chaining (`?.`)
  - Nullish coalescing (`??`)
  - Readonly properties
  - Discriminated unions
  
- **Angular-Specific Types**:
  - Proper typing of observables
  - Template type checking (`strictTemplates`)
  - Form control typing (Angular 14+)

**Output:**
```
TypeScript Quality Report:
- 'any' type usage: X occurrences (target: <5%)
- Strict mode: [enabled/disabled]
- strictTemplates: [enabled/disabled]
- Type coverage: X%
- Missing return types: [count]
```

**4. Angular Testing Practices**

Analyze:
- **Testing Strategy**:
  - Unit test coverage
  - Component testing (TestBed vs shallow)
  - Service testing with HTTP mocking
  - Integration tests with Spectator library
  - E2E tests (Cypress/Playwright/Protractor)
  
- **Test Quality**:
  - Proper use of `async`, `fakeAsync`, `tick`
  - TestBed configuration optimization
  - Mocking strategies (spies, stubs)
  - DOM testing patterns
  
- **Coverage Metrics**:
  - Component coverage
  - Service coverage
  - Pipe and directive coverage

**Output:**
```
Angular Testing Assessment:
- Unit test coverage: X%
- Components with tests: X%
- Services with tests: X%
- E2E test framework: [Cypress/Playwright/none]
- Test execution time: X seconds
- Flaky tests: [identified if pattern exists]
```

**5. Angular Build & Configuration**

Check:
- **Angular CLI Configuration** (`angular.json`):
  - Production optimization settings
  - Source maps configuration
  - Budget limits for bundle sizes
  - AOT compilation enabled
  - Build optimizer enabled
  
- **Dependencies**:
  - Angular version consistency across packages
  - Peer dependency warnings
  - Outdated Angular packages
  - Security vulnerabilities (npm audit)
  
- **Bundle Optimization**:
  - Bundle size analysis
  - Lazy loading effectiveness
  - Common chunk optimization
  - Tree shaking effectiveness

**Output:**
```
Angular Build Health:
Angular Version: X.X.X [LTS/Current/Outdated]

Bundle Analysis:
- Main bundle size: X KB
- Lazy chunks: X (average size: Y KB)
- Budget violations: [list]
- Tree-shaking effectiveness: [assessment]

Dependencies:
- Outdated Angular packages: [list]
- npm audit issues: X vulnerabilities
- Peer dependency warnings: X
```

**6. Angular Performance Patterns**

Evaluate:
- **Performance Optimizations**:
  - Virtual scrolling for large lists
  - Proper image loading (lazy loading)
  - Debouncing of user inputs
  - Caching strategies (HTTP interceptors)
  
- **Performance Anti-Patterns**:
  - Frequent change detection cycles
  - Large bundle sizes (>500KB initial)
  - Synchronous operations in constructors
  - Missing production build optimizations

**Output:**
```
Performance Assessment:
- Initial bundle size: X KB [good/acceptable/needs improvement]
- Virtual scrolling usage: [where applicable]
- HTTP caching strategy: [implemented/missing]
- Image optimization: [implemented/missing]
- Performance bottlenecks: [list detected issues]
```

**7. Angular-Specific Code Smells**

Flag:
- Components communicating via shared services (should use @Input/@Output)
- Logic in constructors (should be in `ngOnInit`)
- Direct DOM manipulation (should use Renderer2)
- Mixing business logic with view logic
- Not using Angular's reactive forms for complex forms
- Subscribing in templates (use async pipe instead)
- Missing error handling in HTTP calls

**Output:**
```
Angular Anti-Patterns:
- DOM manipulation: [list instances not using Renderer2]
- Constructor logic: [list components]
- Missing error handlers: [HTTP calls without error handling]
- Reactive Forms usage: X% (for forms >3 fields)
- Component coupling issues: [list]
```

**8. Angular Style Guide Compliance**

Check against official Angular Style Guide:
- File naming conventions (`kebab-case`)
- Component selector naming (`app-` prefix)
- Service naming (suffix with `Service`)
- Directory structure (feature-based)
- Import ordering and grouping
- Code organization (lifecycle hooks order)

**Output:**
```
Style Guide Compliance:
- Naming conventions: X% compliant
- File structure: [compliant/needs improvement]
- Import organization: X% files need cleanup
- Lifecycle hooks order: X% correct
```

---

## Combined Platform & Technology Matrix

### GitHub + Java Analysis Checklist
```
✓ Analyze GitHub Actions for Maven/Gradle builds
✓ Check Dependabot for Java dependency updates
✓ Review Java-specific GitHub workflows (tests, SonarQube, coverage)
✓ Analyze issue linking with Java exception traces
✓ Check GitHub Packages usage for artifact publishing
```

### GitHub + Angular Analysis Checklist
```
✓ Analyze GitHub Actions for Angular builds (ng build, ng test)
✓ Check npm audit integration in workflows
✓ Review Lighthouse CI integration for performance
✓ Analyze bundle size tracking in PRs
✓ Check GitHub Pages deployment for Angular apps
```

### Bitbucket + Java Analysis Checklist
```
✓ Analyze Bitbucket Pipelines for Maven/Gradle
✓ Check Jira issue integration with Java commits
✓ Review Artifactory/Nexus integration
✓ Analyze deployment pipelines for Spring Boot apps
✓ Check SonarQube integration via pipelines
```

### Bitbucket + Angular Analysis Checklist
```
✓ Analyze Bitbucket Pipelines for npm/Angular CLI
✓ Check environment-specific Angular builds
✓ Review deployment to S3/CDN via pipelines
✓ Analyze test execution in pipelines
✓ Check artifact storage for Angular dist files
```

---

## Synthesis & Recommendations

### Technology-Specific Priority Matrix

**Java Projects - Critical Issues:**
```
CRITICAL:
- Security vulnerabilities in dependencies (log4shell, etc.)
- Thread-safety issues in shared state
- SQL injection vulnerabilities
- Memory leaks (unclosed resources)
- Spring security misconfigurations

HIGH:
- N+1 query problems
- Missing @Transactional boundaries
- Outdated Spring Boot version
- Low test coverage for services
- Missing exception logging

MEDIUM:
- Field injection usage
- Legacy Date API usage
- Raw types in collections
- Missing JaCoCo coverage checks

LOW:
- Checkstyle violations
- Missing JavaDoc on public APIs
- Code formatting inconsistencies
```

**Angular Projects - Critical Issues:**
```
CRITICAL:
- Security vulnerabilities (XSS, Angular version)
- Memory leaks (unsubscribed observables)
- Production build not optimized (AOT disabled)
- Missing error handling in HTTP calls
- Authentication token exposure

HIGH:
- Large bundle sizes (>1MB)
- Missing lazy loading for routes
- Any type usage >10%
- Low test coverage <50%
- Missing OnPush where applicable

MEDIUM:
- Template complexity
- Missing trackBy in ngFor
- Deprecated API usage
- Console.log statements in production

LOW:
- Style guide violations
- Import organization
- Component size (cosmetic)
```

### Platform-Specific Recommendations

**For GitHub:**
```
Quick Wins:
1. Enable Dependabot security updates
2. Add required status checks for branch protection
3. Implement PR templates with checklist
4. Enable CodeQL scanning
5. Set up CODEOWNERS file

Process Improvements:
1. Implement GitHub Actions for automated testing
2. Add bundle size / coverage reporting as PR comments
3. Configure automatic dependency updates
4. Set up deployment workflows
```

**For Bitbucket:**
```
Quick Wins:
1. Configure branch permissions
2. Enable required approvals (minimum 1)
3. Set up Bitbucket Pipelines
4. Configure Jira issue linking
5. Enable merge checks

Process Improvements:
1. Implement pipeline caching for faster builds
2. Add parallel test execution
3. Configure deployment pipelines
4. Set up default reviewers by path
```

---

## Final Report Structure

```markdown
# Development Process Review Report
**Repository**: [name]
**Platform**: [GitHub / Bitbucket]
**Technology**: [Java / Angular]
**Analysis Date**: [date]

## Executive Summary
- Overall Code Quality Score: X/10
- Technology-Specific Score: X/10
- Platform Usage Score: X/10
- Critical Issues: [count]
- Top 3 Recommendations

## Technology-Specific Findings

### [Java/Angular] Code Quality
[Detailed findings from technology-specific sections]

### [Java/Angular] Best Practices Compliance
[Compliance assessment]

### [Java/Angular] Testing & Quality
[Testing metrics and findings]

## Platform-Specific Findings

### [GitHub/Bitbucket] Workflow Analysis
[CI/CD and automation assessment]

### [GitHub/Bitbucket] Collaboration Patterns
[PR/review process analysis]

## Priority Recommendations

### Critical (Week 1)
[Technology and platform specific critical items]

### High Priority (Month 1)
[Important improvements]

### Medium Priority (Quarter 1)
[Planned improvements]

## Implementation Roadmap

### Phase 1: Security & Stability
[Immediate fixes]

### Phase 2: Process & Automation
[Workflow improvements]

### Phase 3: Quality & Performance
[Long-term improvements]

## Metrics Dashboard
[Key metrics to track progress]
```