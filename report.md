# Web Application Vulnerability Assessment Report

## Introduction
This report documents the findings of a manual Web Application Vulnerability Assessment conducted on a deliberately vulnerable web application (DVWA) in a controlled lab environment. The objective of this assessment was to identify, validate, and document common OWASP Top 10 vulnerabilities using ethical testing methodologies.

All testing activities were limited to proof-of-concept only, and no real-world systems were targeted.

---

## Scope
- *Target Application:* Damn Vulnerable Web Application (DVWA)  
- *Environment:* Local Virtual Lab  
- *Testing Type:* Manual Web Application VAPT  
- *Security Level:* Low  
- *Exploitation Level:* Proof-of-Concept Only  

---

## Tools Used
- Kali Linux  
- DVWA  
- Firefox Web Browser

---

## Methodology
The assessment followed a structured Vulnerability Assessment and Penetration Testing (VAPT) lifecycle:

1. Identification of user input points  
2. Manual vulnerability testing  
3. Proof-of-concept validation  
4. Impact analysis  
5. Remediation recommendations  
6. Professional documentation  

---

## Findings

### SQL Injection

*Description:*  
The application fails to properly validate user input before using it in SQL queries, allowing attackers to manipulate database logic.

*Proof of Concept:*  
The following payload was submitted in the User ID field:
' OR '1'='1
The application returned all database records instead of a specific user, confirming SQL Injection.

*Impact:*  
- Unauthorized data access  
- Authentication bypass  
- Possible database compromise  

*Remediation:*  
- Use prepared statements (parameterized queries)  
- Implement strict input validation  
- Apply least-privilege database access  

---

### Reflected Cross-Site Scripting (XSS)

*Description:*  
User input is reflected in the HTTP response without proper sanitization, allowing execution of malicious JavaScript code.

*Proof of Concept:*  
The following payload was submitted:
<script>alert('XSS')</script>
A JavaScript alert was executed in the browser.

*Impact:*
- Session hijacking
- Cookie theft
- Phishing attacks

*Remediation:*
- Apply output encoding
- Sanitize user input
- Implement Content Security Policy (CSP)

---

### OS Command Injection
Description:
The application executes operating system commands using unsanitized user input, enabling command injection.
Proof of Concept:
The following payload was used:
127.0.0.1 | whoami
The injected command was executed and returned system user information.

*Impact:*
- Arbitrary command execution
- Server compromise risk
- Data manipulation

*Remediation:*
- Avoid system command execution functions
- Validate and restrict input
- Use allowlists for acceptable values

---

### Unrestricted File Upload

Description:
The application allows users to upload files without validating file type or extension, enabling execution of server-side scripts.

*Proof of Concept:*
A harmless PHP file containing test code was uploaded and successfully executed on the server.

*Impact:*
- Remote code execution
- Malware hosting
- Full server compromise

*Remediation:*
- Restrict allowed file extensions
- Validate MIME types
- Store uploads outside web root
- Disable execution permissions

---

### Risk Analysis
Multiple high-risk vulnerabilities were identified, primarily caused by improper input validation and insecure application configuration. If exploited in a real-world environment, these vulnerabilities could lead to complete system compromise and data loss.

---

### Conclusion
The assessment demonstrated the presence of several critical OWASP Top 10 vulnerabilities in the target application. Proper secure coding practices, regular security testing, and system hardening are essential to reduce the overall attack surface. This project highlights the importance of proactive web application security testing.

---

### Disclaimer
This report is intended for educational purposes only. All testing was conducted in a controlled lab environment. Unauthorized testing of real systems is illegal and unethical.
