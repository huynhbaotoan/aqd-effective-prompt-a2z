# Error Handling and Edge Cases

## The Importance of Anticipating Problems

When working with Amazon Q Developer, anticipating potential errors and edge cases in your prompts leads to more robust and reliable code. This section explores techniques for guiding Amazon Q Developer to produce code that gracefully handles unexpected situations and edge cases.

## Principles of Effective Error Handling

### 1. Explicit Error Identification

Explicitly identify potential error scenarios that should be handled.

**Example:**
```
Create a function to read and parse a JSON file. The function should handle these error cases:
- File not found
- Permission denied
- Invalid JSON format
- Empty file
- Memory limitations for very large files
```

### 2. Specify Error Handling Strategies

Clearly state how different types of errors should be handled.

**Example:**
```
Create an API endpoint for user registration with the following error handling:

1. For validation errors (invalid email, weak password):
   - Return 400 Bad Request
   - Include specific field errors in the response
   - Log the validation failure with warning level

2. For database errors:
   - Return 500 Internal Server Error
   - Don't expose database details in the response
   - Log the full error with error level
   - Include a correlation ID in both the log and response

3. For duplicate email:
   - Return 409 Conflict
   - Include a user-friendly message
   - Don't reveal if the email exists for security
```

### 3. Define Recovery Mechanisms

Specify how the code should recover from errors when possible.

**Example:**
```
Create a function to upload files to S3 with these recovery mechanisms:

1. Network failures:
   - Implement exponential backoff retry (max 3 attempts)
   - Wait 2^n seconds between retries (where n is the attempt number)

2. Temporary S3 service issues:
   - Queue failed uploads for later retry
   - Implement a dead letter queue after 5 failed attempts

3. File access errors:
   - Skip the problematic file
   - Continue with remaining files
   - Return a list of successfully uploaded and failed files
```

### 4. Request Graceful Degradation

Specify how functionality should degrade when ideal conditions aren't met.

**Example:**
```
Create a weather dashboard component with graceful degradation:

1. If the weather API is down:
   - Display cached data if available (with timestamp)
   - Show a user-friendly error message
   - Provide a manual refresh button

2. If geolocation is unavailable:
   - Fall back to IP-based location
   - If that fails, show a location selector

3. If the user is offline:
   - Use cached data from IndexedDB
   - Clearly indicate that data may be outdated
   - Queue updates for when connectivity is restored
```

### 5. Specify Logging and Monitoring

Request appropriate logging and monitoring for error scenarios.

**Example:**
```
Implement error handling for a payment processing service with these logging requirements:

1. For all errors:
   - Log timestamp, error type, and correlation ID
   - Include relevant transaction details (excluding sensitive data)
   - Add context about the operation being performed

2. For payment gateway errors:
   - Log the error code and message from the gateway
   - Include the request ID from the gateway
   - Don't log full card details (only last 4 digits)

3. For system errors:
   - Log stack traces
   - Include memory usage and system load
   - Trigger alerts for repeated errors
```

## Techniques for Comprehensive Edge Case Handling

### 1. Enumerate Edge Cases

Explicitly list edge cases that should be handled.

**Example:**
```
Create a function to calculate the average of an array of numbers. Handle these edge cases:

- Empty array (return 0 or throw a descriptive error)
- Array with non-numeric values (ignore or throw error)
- Very large arrays (handle memory efficiently)
- Arrays with extreme values (very large or small numbers)
- NaN or Infinity values in the array
- Null or undefined input
```

### 2. Provide Test Cases for Edge Conditions

Include test cases that specifically target edge conditions.

**Example:**
```
Create a date parsing function that handles various formats. It should pass these test cases:

- parseDate("2023-04-15") → new Date(2023, 3, 15)
- parseDate("04/15/2023") → new Date(2023, 3, 15)
- parseDate("April 15, 2023") → new Date(2023, 3, 15)
- parseDate("yesterday") → (date object for yesterday)
- parseDate("") → throw Error("Empty date string")
- parseDate("invalid date") → throw Error("Invalid date format")
- parseDate("2023-13-45") → throw Error("Invalid date: month out of range")
- parseDate(null) → throw Error("Date input is null or undefined")
```

### 3. Request Input Validation

Explicitly request comprehensive input validation.

**Example:**
```
Create a user registration function with the following input validation:

1. Email:
   - Must be a valid format (RFC 5322 compliant)
   - Maximum 255 characters
   - Check for disposable email domains
   - Normalize by trimming and converting to lowercase

2. Password:
   - Minimum 8 characters
   - At least one uppercase letter, one lowercase letter, one number
   - No more than 3 consecutive identical characters
   - Not in the list of common passwords
   - Not containing parts of the email or username

3. Username:
   - 3-30 characters
   - Only alphanumeric characters, hyphens, and underscores
   - No spaces or special characters
   - Not starting or ending with hyphen or underscore
   - Not containing consecutive hyphens or underscores
```

### 4. Consider Resource Constraints

Ask for code that handles resource limitations.

**Example:**
```
Create a function to process large CSV files with these resource constraints:

1. Memory usage:
   - Process the file in streams rather than loading entirely in memory
   - Limit buffer sizes to 64MB
   - Release resources promptly after use

2. CPU usage:
   - Process in batches to avoid blocking the event loop
   - Allow specifying batch size and processing delay
   - Implement cancellation mechanism for long-running operations

3. Disk space:
   - Check available disk space before writing output files
   - Clean up temporary files even if processing fails
   - Implement compression for output if specified
```

### 5. Request Security Considerations

Explicitly ask for security-focused error handling.

**Example:**
```
Create an authentication system with these security-focused error handling requirements:

1. Login failures:
   - Don't reveal whether the username or password was incorrect
   - Implement progressive delays after multiple failed attempts
   - Log authentication failures with client IP and user agent
   - Alert on multiple failures from the same IP

2. Session handling:
   - Invalidate sessions on suspicious activity
   - Implement secure session timeout and renewal
   - Handle concurrent logins according to policy (allow or prevent)

3. Error responses:
   - Never expose stack traces or system details
   - Use generic error messages in production
   - Include correlation IDs for internal troubleshooting
   - Log detailed errors server-side only
```

## Common Edge Cases by Domain

### 1. Web Applications

**User Input:**
- Empty inputs
- Extremely long inputs
- Special characters and Unicode
- Script injection attempts
- Malformed data

**Authentication:**
- Expired credentials
- Invalid tokens
- Session timeout
- Multiple concurrent logins
- Account lockouts

**Network:**
- Slow connections
- Intermittent connectivity
- Request timeouts
- CORS issues
- Content blocking

### 2. Data Processing

**File Operations:**
- Empty files
- Extremely large files
- Corrupted files
- Unexpected formats
- Insufficient permissions

**Data Quality:**
- Missing values
- Duplicate records
- Inconsistent formats
- Out-of-range values
- Unexpected data types

**Performance:**
- Large datasets
- Complex queries
- Resource limitations
- Concurrent operations
- Long-running processes

### 3. APIs and Integrations

**External Services:**
- Service unavailable
- Rate limiting
- Changed API responses
- Versioning conflicts
- Authentication failures

**Data Exchange:**
- Serialization errors
- Incompatible formats
- Validation failures
- Partial responses
- Timeout during transmission

## Example: Comprehensive Error Handling for a File Upload Service

Here's a complete example of requesting code with thorough error handling:

```
Task: Create a service for uploading files to AWS S3 with comprehensive error handling.

## Functional Requirements
- Accept file uploads from users
- Validate file types and sizes
- Store metadata in a database
- Upload files to S3
- Generate and return a shareable URL

## Error Handling Requirements

### Input Validation
- File size: Reject files larger than 50MB with a clear error message
- File type: Allow only images, PDFs, and office documents
- Metadata: Validate required fields (title, description)
- User permissions: Verify user has upload permissions

### Storage Errors
- S3 connection failures: Retry up to 3 times with exponential backoff
- S3 quota exceeded: Provide clear error message about storage limits
- Database errors: Roll back S3 upload if metadata cannot be stored
- Concurrent modifications: Handle race conditions with optimistic locking

### Security Considerations
- Malicious files: Scan for viruses before uploading
- Permissions: Verify user is authorized for the requested storage location
- Privacy: Ensure files are stored with appropriate access controls
- Logging: Log access attempts without exposing sensitive information

### Resource Management
- Memory usage: Stream files rather than loading entirely in memory
- Cleanup: Remove temporary files even if processing fails
- Quotas: Check user quotas before accepting uploads
- Rate limiting: Prevent abuse with appropriate rate limits

### User Experience
- Progress tracking: Provide upload progress for large files
- Resumable uploads: Support resuming interrupted uploads
- Friendly errors: Convert technical errors to user-friendly messages
- Fallbacks: Offer alternative upload methods if primary method fails

## Expected Error Responses

For validation errors:
```json
{
  "status": "error",
  "code": "VALIDATION_ERROR",
  "message": "The provided file does not meet requirements",
  "details": {
    "field": "file",
    "error": "File size exceeds the 50MB limit",
    "limit": "50MB",
    "actual": "75MB"
  }
}
```

For service errors:
```json
{
  "status": "error",
  "code": "SERVICE_ERROR",
  "message": "Unable to process upload at this time",
  "correlationId": "err-12345-abcde",
  "retry": true
}
```

## Logging Requirements
- Log all errors with correlation IDs
- Include relevant context (user ID, file metadata)
- Log different levels based on severity
- Don't log file contents or sensitive user data

Please implement this service with the specified error handling requirements.
```

## Strategies for Testing Error Handling

When requesting code from Amazon Q Developer, consider asking for test cases that verify error handling:

**Example:**
```
After implementing the user authentication function, please create unit tests that verify these error handling scenarios:

1. Test invalid credentials:
   - Non-existent username
   - Incorrect password for valid username
   - Locked account
   - Expired account

2. Test input validation:
   - Empty username/password
   - Malformed email as username
   - Extremely long inputs
   - SQL injection attempts

3. Test authentication failures:
   - Database connection errors
   - Timeout during authentication
   - Too many concurrent authentication attempts

4. Test session handling:
   - Expired session token
   - Invalid session format
   - Session from different IP address
```

## Key Takeaways

- Comprehensive error handling leads to more robust and reliable code
- Explicitly identify potential error scenarios in your prompts
- Specify how different types of errors should be handled
- Define recovery mechanisms and graceful degradation strategies
- Request appropriate logging and monitoring
- Consider resource constraints and security implications
- Provide test cases that verify error handling behavior

## Next Steps

In the next section, we'll explore Security Considerations in prompt engineering.

---

[Next: Security Considerations](./03-security.md) | [Previous: Clarity and Precision](./01-clarity.md) | [Back to Main](../README.md)
