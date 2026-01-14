Perform a security-focused code scan with compliance controls embedded early in the review process.

## Security Scan Framework

Analyze the codebase for security vulnerabilities across these categories:

### OWASP Top 10 Checks
1. **Injection** - SQL, NoSQL, OS command, LDAP injection points
2. **Broken Authentication** - Weak session management, credential handling
3. **Sensitive Data Exposure** - Hardcoded secrets, unencrypted data, logs
4. **XML External Entities (XXE)** - Unsafe XML parsing
5. **Broken Access Control** - Missing authorization, IDOR vulnerabilities
6. **Security Misconfiguration** - Debug modes, default credentials, verbose errors
7. **XSS** - Reflected, stored, DOM-based cross-site scripting
8. **Insecure Deserialization** - Untrusted data deserialization
9. **Using Components with Known Vulnerabilities** - Outdated dependencies
10. **Insufficient Logging & Monitoring** - Missing audit trails

### Additional Checks
- **Secrets Detection**: API keys, passwords, tokens in code
- **Dependency Audit**: Check for vulnerable packages
- **Input Validation**: Boundary checks, type validation
- **Cryptography**: Weak algorithms, improper key management
- **Race Conditions**: TOCTOU, concurrent access issues

## Output Format

```
## Security Scan Report

### Risk Level: [Critical/High/Medium/Low]

### Findings by Severity

#### Critical (Immediate Action Required)
- [CVE/Issue Type]: [File:Line] - [Description]
  Remediation: [Fix suggestion]

#### High
- ...

#### Medium
- ...

#### Low/Informational
- ...

### Dependency Vulnerabilities
| Package | Current | Vulnerable | Fix Version |
|---------|---------|------------|-------------|

### Compliance Notes
- [Relevant compliance considerations for regulated industries]

### Recommended Actions
1. [Priority action items]
```

Ask the user which file, directory, or the entire project to scan if not specified.
