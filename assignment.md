# Assignment (Optional)

## Brief

Practice DevSecOps principles by implementing secure secrets management and understanding dependency vulnerabilities.

1. **Secrets Management with Environment Variables**
   - Use your existing Spring Boot project (e.g., devops-demo)
   - Create a simple service class that needs an API key (you can simulate this):
```java
     @Service
     public class EmailService {
         private final String apiKey;
         
         public EmailService() {
             // Read API key from environment variable
             this.apiKey = System.getenv("EMAIL_API_KEY");
         }
         
         public String getApiKey() {
             return apiKey != null ? "API Key is set" : "API Key is missing";
         }
     }
```
   - Create a controller endpoint to test it:
```java
     @GetMapping("/check-config")
     public String checkConfig() {
         return emailService.getApiKey();
     }
```
   - Set the environment variable locally and test:
     - **Mac/Linux:** `export EMAIL_API_KEY=test_key_12345`
     - **Windows:** `set EMAIL_API_KEY=test_key_12345`
   - Run your application and access `/check-config` endpoint
   - Verify it shows "API Key is set"
   - Write a brief explanation (3-4 sentences) describing:
     - Why hardcoding secrets is dangerous
     - How environment variables improve security
     - Where you would set environment variables in CircleCI (hint: Project Settings)

2. **Understanding Dependency Vulnerabilities**
   - Open your project's `pom.xml` file
   - List all dependencies you see (at least 3-5)
   - Visit the National Vulnerability Database: https://nvd.nist.gov/
   - Search for ONE of your dependencies (e.g., "Spring Boot" or "PostgreSQL JDBC")
   - Find at least one CVE related to that dependency
   - Write a report (4-5 sentences) that includes:
     - Which dependency you researched
     - One CVE number you found (e.g., CVE-2021-12345)
     - The severity level (Critical, High, Medium, Low)
     - A brief description of what the vulnerability does
     - Why keeping dependencies updated is important
   - (Bonus) Check if your current version is affected by the CVE you found

## Submission (Optional)

- Submit the URL of the GitHub Repository that contains your work.
## References
- Java: https://docs.oracle.com/javase/
- Spring Boot: https://docs.spring.io/spring-boot/docs/current/reference/html/
- PostgreSQL: https://www.postgresql.org/docs/
- OWASP: https://cheatsheetseries.owasp.org/