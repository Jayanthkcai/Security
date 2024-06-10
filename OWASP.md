OWASP, the Open Web Application Security Project.

The OWASP Top 10 is a list of the most common and dangerous security problems found in web applications. 

1. Broken Access Control: Users can access parts of the app they shouldn't.
    - Example: A user with a regular account can access the admin panel by changing the URL from /user/profile to /admin/dashboard.

    - Mitigation:
        - Implement role-based access control.
        - Use a single access control mechanism across the application.
        - Regularly test access control mechanisms.

2. Cryptographic Failures: Sensitive data isn’t properly protected.
    - Example: Storing passwords in plaintext or using outdated algorithms like MD5 for hashing.

    - Mitigation:
        - Use strong encryption standards like AES for data at rest.
        - Use HTTPS to protect data in transit.
        - Store passwords using strong, adaptive hashing algorithms like bcrypt.

3. Injection: Malicious data can trick the app into running harmful commands.
    - Example: SQL Injection where user input is directly concatenated into a SQL query:
        SELECT * FROM Users WHERE Username = 'admin' AND Password = 'password';

    - Mitigation:
        - Use parameterized queries or prepared statements.
        - Validate and sanitize all user inputs.
        - Employ ORM tools to abstract direct SQL queries.
        
4. Insecure Design: The app is built without considering security from the start.
    - Example: An application that does not use multi-factor authentication (MFA) by design.

    - Mitigation:
        - Integrate security into the design phase.
        - Conduct threat modeling and security reviews.
        - Implement secure design patterns and principles.

5. Security Misconfiguration: Poorly set up security settings.
    - Example: Default admin credentials not changed or unnecessary features enabled (like detailed error messages).

    - Mitigation:
        - Establish secure configuration settings and deploy them to all environments.
        - Regularly update and patch systems.
        - Remove or disable unused features and components.

6. Vulnerable and Outdated Components: Using software components with known security issues.
    - Example: Using an outdated version of a library that has known security flaws.

    - Mitigation:
        - Regularly update dependencies and third-party libraries.
        - Use tools to check for known vulnerabilities in dependencies.
        - Apply patches and updates as soon as they are available.

7. Identification and Authentication Failures: Problems with verifying user identity.
    - Example: Implementing weak password policies or failing to use account lockout mechanisms.

    - Mitigation:
        - Implement strong password policies and use multi-factor authentication (MFA).
        - Ensure proper session management (e.g., session timeout, secure cookies).
        - Use standard authentication frameworks and libraries.

8. Software and Data Integrity Failures: Risks from code and data changes by unauthorized sources.
    - Example: Insecure CI/CD pipeline that allows unauthorized code changes.

    - Mitigation:
        - Implement code signing and integrity checks.
        - Secure CI/CD pipelines and use security tools to scan builds.
        - Employ runtime protection mechanisms.

9. Security Logging and Monitoring Failures: Lack of proper tracking and detection of security issues.
    - Example: Failure to log login attempts, or not monitoring application logs for suspicious activity.

    - Mitigation:
        - Implement comprehensive logging and monitoring.
        - Ensure logs are stored securely and reviewed regularly.
        - Use automated tools to detect and alert on potential security incidents.

10. Server-Side Request Forgery (SSRF): The app fetches resources from unintended locations due to user input manipulation.
    - Example: An attacker can make the server request internal resources by supplying a crafted URL:
        http://internal-server/admin

    - Mitigation:
        - Validate and sanitize all URLs.
        - Use a whitelist of allowed domains for making requests.
        - Implement proper network segmentation and firewall rules.