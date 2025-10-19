# Project Scope and Expectations - Director Email

**Проект:** SRE-Knowledge-Base

## Project Overview
**Working Group Focus**: Improving the development organization
**Geographic Focus**: APAC teams (due to recipients being APAC-based)
**Target**: All dev teams under Sumit's organization
**Duration**: Approximately 1 month (started around September 30th)

## Key Participants
- **Team Leads**: @Lavrenov, Alexander [TECH NE] and @Zateychuk, Vladimir [TECH NE]
- **Project Lead**: Rich (with complete access and 100% cooperation expected)
- **Support Team**: 2-3 Paul's dev guys (Alex and Vladimir)
- **Current Team**: Sushil's team (already being worked with)

## Project Goals
1. **Primary Goal**: "A completely brilliant dev org"
2. **Secondary Goals**:
   - Lessons learned about what worked, what didn't
   - Greater degree of automation (maybe)
   - 100% compliance with Justin's checklist

## Key Tools and Resources
- **Justin's Checklist**: "Road to Prod - Mind Map for Development Teams (002).xlsx"
- **Automation Scripts**: Starting point at `https://github.com/CitiSandbox/rp47127.git`
- **Friday Call**: Demo test automation (night time for APAC recipients)

## Team Structure Requirements

### What is a "Team"?
- Classic two pizza team of folks in engineering roles delivering software products
- **Reference**: "Empowered" book or google "product teams vs feature teams"
- **NOT**: Individual contributors nor assorted pools of people

### Team Composition
- **Primary**: Engineering roles delivering software products
- **Secondary**: BA/PM/Support people (small fraction of team)
- **Issue**: Engineers doing BA and Support work needs to be fixed
- **Exception**: On-call support doesn't count unless it's constant

### Team Lead Role
- **Definition**: Team lead is a pointer to the team (programming terms)
- **Responsibility**: Represent and control work done by the team
- **Accountability**: Last line of accountability
- **Importance**: Most important link in the org chain

## Work Definition
**Engineering Work Includes**:
- Product features
- Bug fixes
- CAMP work tickets
- EE adoptions
- Team ownership of CI/CD pipelines
- Source control repos ownership

## Accountability Framework
- **CODA**: Culture of direct accountability
- **Work Management**: Must be managed at team level
- **Completion Accountability**: Team is ultimately accountable
- **WMC**: Define and maintain teams in WMC (no formal HR support)

## Rich's Initial Observations (First 15 Days)

### 1. Unfamiliarity with Developer Manifesto
**Issues**:
- Lack of connecting dots with Developer manifesto and "Baking Better Code" emails
- Lack of prioritization of modern tech migrations
- Focus needed on: Github migrations, Gradle migrations, Renovate onboarding

**Examples**:
- Github, Gradle, Renovate migrations not prioritized due to busyness
- Migration work exists but not prioritized
- Modern solutions adoption leads to less manual, more automated workflows

### 2. Monolithic Architecture Issues
**Problems**:
- Monolithic software architecture leads to complex dependencies
- Manual and cumbersome release processes
- Anti-pattern: Trying to shoehorn Macro/Monolithic development into Microservice practices

**Recommendations**:
- Break up components into features
- Organize teams based on features
- Reduce coupling amongst feature squads/teams
- Increase release frequency

**Specific Issues**:
- Monthly manual release process
- One RoD per CSI but software spans CSIs
- Shared technology stacks (e.g., Databases) leading to tight coupling
- DevOps team manages release dependencies manually
- Code releases during weekend outage windows
- Monthly release schedule optimized to reduce DevOps weekend working hours
- Dependency POM repo created to tightly couple repos for Spring Boot dependencies

## Geographic Distribution Considerations
- Modern development teams are geographically diverse
- Small highly effective teams tend to be geolocated in one office/region
- Optimally collocated with product/ops or business users
- Example: Equities tech team collocated together and with business
- **Renaissance Developers**: Business knowledgeable technologists (Mike Naggar reference)
- **Example**: Team lead in NAM, team in APAC

## Success Metrics
- 100% compliance with Justin's checklist
- Healthy engineering product teams
- No need for EE chasing
- Increased productivity
- Happier engineers
- Natural excellence at Developer and Testing Manifesto compliance
- Correct architectures creation
- Leadership in EE space

## Timeline and Progress
- **Started**: Around September 30th
- **Current Status**: Approximately halfway through
- **Progress**: Only been discussing with Sushil (one of Sumit's teams)
- **Target**: Complete Sumit's org in one month
- **Next Steps**: Get started with rest of team leads
