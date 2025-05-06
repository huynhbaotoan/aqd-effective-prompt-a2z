# Security Considerations

## The Critical Importance of Security

When working with Amazon Q Developer to generate code, security must be a top priority. Insecure code can lead to vulnerabilities, data breaches, and other serious consequences. This section explores techniques for guiding Amazon Q Developer to produce secure code that follows best practices.

## Principles of Secure Prompt Engineering

### 1. Explicitly Request Security Best Practices

Make security requirements explicit in your prompts.

**Example:**
```
Create a Node.js API endpoint for user registration that follows these security best practices:
- Hash passwords using bcrypt with appropriate salt rounds
- Implement proper input validation and sanitization
- Use parameterized queries to prevent SQL injection
- Set secure HTTP headers (Content-Security-Policy, X-XSS-Protection, etc.)
- Implement rate limiting to prevent brute force attacks
```

### 2. Specify Security Standards and Compliance

Reference specific security standards or compliance requirements.

**Example:**
```
Create a function to store and retrieve sensitive customer data following these security requirements:
- GDPR compliance for personal data handling
- PCI DSS requirements for payment information
- Data encryption at rest using AES-256
- TLS 1.2+ for data in transit
- Proper key management with rotation policies
- Audit logging for all access and modifications
```

### 3. Request Security Testing

Ask for security testing or validation as part of the solution.

**Example:**
```
After implementing the authentication system, please provide:
1. Security test cases that verify protection against:
   - Brute force attacks
   - Session hijacking
   - CSRF vulnerabilities
   - Privilege escalation
2. A security review checklist for the implementation
3. Recommendations for additional security measures
```

### 4. Prioritize Security Over Convenience

Explicitly state that security should take precedence over convenience when there's a tradeoff.

**Example:**
```
Create a file upload feature with the following requirements:
- Security is the highest priority, even if it impacts user experience
- Implement strict file type validation using content inspection, not just extension
- Scan uploaded files for malware using a third-party service
- Store files outside the web root with randomized names
- Implement proper access controls for file retrieval
```

### 5. Request Secure Defaults

Ask for implementations with secure defaults that require explicit opt-out rather than opt-in.

**Example:**
```
Create a configuration system for our application with these security requirements:
- All security features should be enabled by default
- TLS should be required by default, with HTTP disabled
- CSRF protection should be automatically enabled
- Secure cookies should be the default
- Content Security Policy should be restrictive by default
- Users should have to explicitly disable security features (with warnings)
```

## Common Security Concerns by Domain

### 1. Web Application Security

**Authentication and Authorization:**
- Password storage and handling
- Multi-factor authentication
- Session management
- Access control
- Account lockout policies

**Input Validation:**
- Cross-site scripting (XSS) prevention
- SQL injection protection
- Command injection prevention
- Input sanitization
- Content validation

**API Security:**
- Authentication mechanisms
- Rate limiting
- Input validation
- CORS configuration
- Error handling

### 2. Data Security

**Data Protection:**
- Encryption at rest
- Encryption in transit
- Key management
- Data minimization
- Secure deletion

**Database Security:**
- Connection security
- Query parameterization
- Access controls
- Sensitive data handling
- Audit logging

**File Operations:**
- Path traversal prevention
- File type validation
- Secure file storage
- Access control for files
- Malware scanning

### 3. Infrastructure and Deployment

**Configuration Security:**
- Secrets management
- Environment separation
- Principle of least privilege
- Secure defaults
- Configuration validation

**Deployment Security:**
- CI/CD pipeline security
- Container security
- Infrastructure as Code security
- Dependency management
- Vulnerability scanning

## Techniques for Secure Prompt Engineering

### 1. Security-Focused Requirements

Frame your requirements with security as a primary concern.

**Example:**
```
Task: Create a user authentication system for a web application.

Security Requirements:
1. Password Storage:
   - Use Argon2id for password hashing
   - Configure appropriate memory, iterations, and parallelism factors
   - Generate unique salt for each password
   - Implement pepper using environment variables

2. Authentication Flow:
   - Implement account lockout after 5 failed attempts
   - Require password reset after 90 days
   - Enforce MFA for administrative accounts
   - Use secure, HttpOnly, SameSite=Strict cookies for session

3. Registration Security:
   - Implement email verification
   - Check passwords against breach databases
   - Enforce password complexity requirements
   - Rate limit registration attempts by IP

4. Session Management:
   - Generate cryptographically secure session IDs
   - Rotate session IDs after login
   - Implement absolute and idle timeouts
   - Allow users to view and terminate active sessions
```

### 2. Security Anti-Patterns to Avoid

Explicitly mention security anti-patterns that should be avoided.

**Example:**
```
Create a database access layer for our application, avoiding these security anti-patterns:

1. DO NOT:
   - Use string concatenation for SQL queries
   - Store credentials in code or config files
   - Use the same database user for all operations
   - Log sensitive data or full SQL queries with parameters
   - Leave default database credentials unchanged

2. INSTEAD:
   - Use parameterized queries or ORM with proper escaping
   - Retrieve credentials from a secure vault or environment variables
   - Implement database users with least privilege
   - Mask sensitive data in logs
   - Use unique, strong credentials
```

### 3. Security-Focused Code Reviews

Request a security-focused review of the generated code.

**Example:**
```
After generating the file upload functionality, please perform a security review covering:

1. Input Validation:
   - Are file types properly validated?
   - Is there a file size limit?
   - Is the file content inspected beyond just the extension?

2. Storage Security:
   - Are files stored outside the web root?
   - Are filenames randomized to prevent guessing?
   - Is proper access control implemented?

3. Processing Security:
   - Is the file processed securely?
   - Are there protections against zip bombs or decompression attacks?
   - Is metadata stripped from uploaded files?

4. Error Handling:
   - Do error messages leak sensitive information?
   - Are failed uploads logged properly?
   - Are temporary files cleaned up after errors?
```

### 4. Threat Modeling

Include threat modeling in your prompt to focus on specific security concerns.

**Example:**
```
Create an API for a financial transaction system. Consider these threat vectors:

1. Attacker trying to manipulate transaction amounts:
   - Implement server-side validation of all transaction details
   - Use digital signatures to verify transaction integrity
   - Compare transaction details against original authorization

2. Attacker attempting to replay transactions:
   - Implement unique transaction IDs
   - Use nonce values for each request
   - Check for and prevent duplicate transactions

3. Attacker trying to access others' transaction history:
   - Implement proper authentication and authorization
   - Use indirect reference IDs instead of sequential identifiers
   - Validate user has permission for each transaction view

4. Insider threat with partial system access:
   - Implement separation of duties
   - Require multiple approvals for sensitive operations
   - Maintain comprehensive audit logs
```

### 5. Security Testing Requirements

Request specific security tests as part of the implementation.

**Example:**
```
Implement a JWT authentication system with the following security tests:

1. Token Security Tests:
   - Test for proper signature validation
   - Verify token expiration is enforced
   - Confirm audience and issuer validation
   - Test handling of manipulated tokens

2. Key Management Tests:
   - Verify keys are properly protected
   - Test key rotation procedures
   - Confirm old tokens are invalidated after rotation
   - Test for proper algorithm enforcement

3. Implementation Tests:
   - Test for timing attacks in token validation
   - Verify proper error messages (not too revealing)
   - Test handling of malformed tokens
   - Confirm proper logging of authentication events
```

## Example: Comprehensive Security Requirements for a Web API

Here's a complete example of requesting code with thorough security considerations:

```
Task: Create a RESTful API for a healthcare application that manages patient records.

## Security Requirements

### Authentication and Authorization
- Implement OAuth 2.0 with OpenID Connect for authentication
- Use JWT with appropriate expiration (15 minutes)
- Implement role-based access control (Patient, Doctor, Admin)
- Require MFA for administrative and healthcare provider roles
- Implement IP-based access restrictions for administrative endpoints

### Data Protection
- Encrypt all PHI (Protected Health Information) at rest using AES-256
- Implement field-level encryption for sensitive data elements
- Ensure all data in transit uses TLS 1.2+
- Implement data masking for non-essential PII in responses
- Maintain audit logs for all data access (who, when, what)

### API Security
- Implement rate limiting (100 requests per minute per user)
- Use API keys for service-to-service communication
- Set secure HTTP headers:
  - Content-Security-Policy
  - Strict-Transport-Security
  - X-Content-Type-Options: nosniff
  - X-Frame-Options: DENY
- Validate and sanitize all input parameters
- Implement proper CORS configuration

### Compliance Requirements
- Ensure HIPAA compliance for all PHI handling
- Implement data retention policies
- Provide data export functionality for GDPR compliance
- Include consent management for data processing
- Maintain comprehensive access logs for compliance reporting

### Secure Development Practices
- Use parameterized queries for all database operations
- Implement proper error handling that doesn't leak sensitive information
- Use secure dependencies and keep them updated
- Follow the principle of least privilege for all operations
- Implement proper secrets management (no hardcoded secrets)

## Security Testing Requirements
- Include unit tests for access control mechanisms
- Provide integration tests for authentication flows
- Include tests for input validation and sanitization
- Demonstrate tests for rate limiting functionality
- Include security headers validation tests

## Security Documentation
- Document the authentication and authorization model
- Provide API security guidelines for consumers
- Include security configuration documentation
- Document data encryption approach
- Provide incident response procedures for security events

Please implement this API with the specified security requirements, focusing on protecting patient data according to healthcare industry standards.
```

## Key Takeaways

- Security must be explicitly requested and prioritized in prompts
- Specify security standards and compliance requirements
- Request security testing and validation
- Prioritize security over convenience when necessary
- Ask for implementations with secure defaults
- Consider domain-specific security concerns
- Use threat modeling to focus on specific security risks
- Request security-focused code reviews

## Next Steps

In the next section, we'll explore Performance Optimization in prompt engineering.

---

[Next: Performance Optimization](./04-performance.md) | [Previous: Error Handling and Edge Cases](./02-error-handling.md) | [Back to Main](../README.md)
