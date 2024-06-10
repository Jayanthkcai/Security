Static Application Security Testing (SAST) and Dynamic Application Security Testing (DAST) are two fundamental approaches to application security testing. 

**SAST** is a white-box testing methodology where the application's source code, bytecode, or binary is examined to find security vulnerabilities without executing the program. SAST tools analyze the codebase for coding errors, insecure coding practices, and potential vulnerabilities early in the development lifecycle.

**Example Workflow:**
- Code Analysis: A developer commits code to the repository.
- SAST Tool Execution: The SAST tool scans the codebase for vulnerabilities.
- Report Generation: The tool generates a report detailing the identified issues.
- Issue Resolution: Developers review the report, fix the vulnerabilities, and recommit the code.
- Re-Scanning: The code is re-scanned to ensure the issues are resolved.

**Popular SAST Tools:**
- SonarQube: An open-source platform that continuously inspects code quality and security.
- Fortify Static Code Analyzer (SCA): A commercial tool that scans code for security vulnerabilities.
- Checkmarx: A comprehensive SAST tool that integrates with CI/CD pipelines and various development environments.
- Veracode Static Analysis: A cloud-based SAST solution that provides detailed vulnerability reports and remediation guidance.
- Codacy: An automated code review tool that includes static analysis for security vulnerabilities.
- Snyk: Snyk is a powerful tool that helps identify and fix security vulnerabilities in open-source dependencies used in your project. It provides both SAST and DAST capabilities but primarily focuses on dependency scanning and management.

</br>

**DAST** is a black-box testing methodology where the application is tested in its running state. DAST tools simulate attacks against the application to identify vulnerabilities that could be exploited in a real-world scenario. Unlike SAST, DAST does not require access to the source code.

**Example Workflow:**
- Application Deployment: The application is deployed in a test or staging environment.
- DAST Tool Execution: The DAST tool scans the application by sending various inputs and observing the responses.
- Vulnerability Detection: The tool identifies vulnerabilities based on the application's behavior.
- Report Generation: The tool generates a report detailing the identified vulnerabilities.
Issue Resolution: Developers review the report, fix the vulnerabilities, and redeploy the application.
- Re-Scanning: The application is re-scanned to ensure the issues are resolved.

**Popular DAST Tools:**
- OWASP ZAP (Zed Attack Proxy): An open-source DAST tool that identifies security vulnerabilities in web applications.
- Burp Suite: A comprehensive platform for web application security testing, including a robust DAST tool.
- Acunetix: A commercial DAST tool that scans web applications and APIs for vulnerabilities.
- Netsparker: An automated DAST solution that detects vulnerabilities in web applications and web services.
- AppSpider: A DAST tool that simulates real-world attacks to identify vulnerabilities in web applications and APIs.

**Comparison**

<table><thead><tr><th>Aspect</th><th>SAST</th><th>DAST</th></tr></thead><tbody><tr><td><strong>Code Access</strong></td><td>Requires access to source code, bytecode, or binaries</td><td>No access to source code needed; tests the running application</td></tr><tr><td><strong>Testing Phase</strong></td><td>Early in the development lifecycle</td><td>Post-deployment (test/staging environment)</td></tr><tr><td><strong>Detection</strong></td><td>Finds vulnerabilities in the code itself</td><td>Finds vulnerabilities by simulating attacks on the application</td></tr><tr><td><strong>Types of Issues Found</strong></td><td>Coding errors, insecure coding practices, logic flaws</td><td>Configuration issues, runtime vulnerabilities, business logic flaws</td></tr><tr><td><strong>Example Tools</strong></td><td>SonarQube, Fortify SCA, Checkmarx, Veracode, Codacy</td><td>OWASP ZAP, Burp Suite, Acunetix, Netsparker, AppSpider</td></tr></tbody></table>

**Static Application Security Testing (SAST) Detected Vulnerabilities**:
- SQL Injection (SQLi):
    - User input directly concatenated into SQL queries without proper sanitization or parameterization.
        - Example: SELECT * FROM Products WHERE ProductID = '<userInput>'
    - Resolution:
        - Implement parameterized queries or use ORM frameworks with built-in parameterization to prevent SQL injection attacks.        
            
            ```markdown
            string query = "SELECT * FROM Products WHERE ProductID = @productId";
            SqlCommand cmd = new SqlCommand(query, connection);
            cmd.Parameters.AddWithValue("@productId", userInput);
            ```

- Cross-Site Scripting (XSS):
    - User input directly echoed into HTML responses without proper encoding.
        - Example: 

           ```markdown

          1.   var productName = '<%= userInput %>';

          2.   <script>alert('<userInput>');</script>
           ```

    - Resolution:
        - Encode user input properly before rendering it in HTML to prevent XSS attacks.
            
            ```markdown
            1. // Assume userInput is the variable containing user input

                // Step 1: Encode User Input
                var encodedUserInput = encodeHTML(userInput);

                // Step 2: Display Encoded User Input in HTML
                document.getElementById("output").innerHTML = encodedUserInput;

                // Function to HTML-encode user input
                function encodeHTML(input) {
                    return input.replace(/&/g, "&amp;")
                                .replace(/</g, "&lt;")
                                .replace(/>/g, "&gt;")
                                .replace(/"/g, "&quot;")
                                .replace(/'/g, "&#39;");
                }

            2. var productName = '<%= HttpUtility.HtmlEncode(userInput) %>';
            ```

**Dynamic Application Security Testing (DAST) Detected Vulnerabilities**:
- Broken Authentication:
    - Weak password policies, lack of multi-factor authentication, susceptibility to brute force attacks.
        - Examples:
            - Weak passwords like 'password123' allowed.
            - Absence of multi-factor authentication for sensitive operations.
            - No rate limiting on login attempts.
    - Resolution:
        - Enforce strong password policies, implement multi-factor authentication, and rate-limit login attempts to mitigate brute force attacks.
        - Regularly review and update authentication mechanisms to address emerging threats and vulnerabilities.

- Sensitive Data Exposure:
    - Exposed sensitive information through unencrypted communication channels or inadequate access controls.
        - Examples:
            - User credentials transmitted over HTTP.
            - Access to sensitive endpoints without proper authentication.
            - Session tokens stored in client-side storage without encryption.
    - Resolution: 
        - Encrypt sensitive data in transit using HTTPS/TLS, enforce access controls to restrict access to sensitive endpoints or resources, and ensure compliance with data protection regulations (e.g., GDPR, PCI DSS).