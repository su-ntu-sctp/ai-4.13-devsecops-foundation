# 4.13 Self Studies

**Estimated Preparation Time:** 70 minutes

---

> **📌 Note:** The videos in these self studies are selected to help you build familiarity with the tools and concepts before class. The approach, project structure, and commands used in the videos may differ from what we do in the lesson. Focus on understanding the **concepts and the why** — not on replicating the video step by step. The lesson content is what you should follow during class.

---

## Task 1 — What is DevSecOps? (25 minutes)

Watch the following video on DevSecOps:

- 📹 [What is DevSecOps? — https://www.youtube.com/watch?v=DTEaw2-Sa7I]

While watching, refer to **lesson.md Part 1** and pay attention to:
- How DevSecOps differs from traditional DevOps
- Why security is described as "everyone's responsibility"
- How integrating security earlier changes the development workflow
- What the key principles of DevSecOps are

**Guiding Questions:**
1. In your own words, what is the main difference between traditional DevOps and DevSecOps?
2. Why does treating security as a final step cause problems for development teams?
3. Which DevSecOps principle do you think is most important for a small development team to adopt first?

---

## Task 2 — Shift-Left Security (25 minutes)

Watch the following video on shift-left security:

- 📹 [Shift-Left Security — https://www.youtube.com/watch?v=nGR8SdKsxu0]

While watching, refer to **lesson.md Part 2** and pay attention to:
- What "shift-left" means in the context of software development
- Why catching security issues early is significantly cheaper than catching them late
- How shift-left security changes the responsibilities of developers
- What tools and practices support a shift-left approach

**Guiding Questions:**
1. Using the cost table in lesson.md, explain why fixing a security issue in production costs so much more than fixing it during development
2. What specific things can a developer do before committing code to support shift-left security?
3. How does shift-left security relate to the CI/CD pipeline you built in earlier lessons?

---

## Task 3 — Pipeline Risks and Secrets Management (20 minutes)

No video for this task. Refer to **lesson.md Parts 3 and 4** and answer the following:

1. Look at the three attack scenarios in Part 3 (Supply Chain Attack, Leaked Credentials, Vulnerable Dependency). For each one, write one sentence describing how it could have been prevented.
2. Review the "What NOT to do" section in Part 4. Have you seen any of these mistakes in your own projects or in tutorials online? Which one do you think is the most common mistake developers make?
3. Look at the three code snippets from Activity 2 in lesson.md. Identify the security mistake in each one and write down the correct approach.

**Guiding Questions:**
1. Why is it not enough to just delete a hardcoded secret from your code — why does the Git history still pose a risk?
2. What is the difference between using environment variables in local development vs in a CI/CD pipeline?
3. Why should production secrets be different from development secrets?

---

## Active Engagement Strategies

- Pause the first video when each DevSecOps principle is introduced and try to give a real-world example before the video does
- After watching Task 2, close the video and try to draw the shift-left diagram from memory — traditional approach on one side, shift-left on the other
- For Task 3, write your answers before class — come prepared to discuss the attack scenarios and security mistakes

---

## Additional Reading Material

- [OWASP DevSecOps Guideline](https://owasp.org/www-project-devsecops-guideline/)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [National Vulnerability Database](https://nvd.nist.gov/)
- [CVE Database](https://cve.mitre.org/)