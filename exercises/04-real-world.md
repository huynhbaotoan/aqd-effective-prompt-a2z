# Real-world Scenarios

This section provides practical exercises based on real-world scenarios that software developers commonly face. These exercises will help you apply prompt engineering techniques to solve actual problems you might encounter in your development work.

## Scenario 1: Legacy Code Migration

**Context:** Your team has inherited a legacy application written in an older technology stack. You need to migrate it to a modern framework while preserving functionality.

**Exercise:** Use Amazon Q Developer to help with the migration process.

**Steps:**

1. **Analysis Phase**
   
   Write a prompt that asks Amazon Q Developer to analyze a piece of legacy code and identify:
   - Key functionality and business logic
   - Dependencies and external integrations
   - Potential challenges in migration
   - Recommended modern equivalents for outdated patterns

   Example legacy code snippet (jQuery to React migration):
   ```javascript
   $(document).ready(function() {
     $('#userForm').submit(function(e) {
       e.preventDefault();
       
       var userData = {
         name: $('#name').val(),
         email: $('#email').val(),
         role: $('#role').val()
       };
       
       if (!validateEmail(userData.email)) {
         $('#emailError').text('Please enter a valid email').show();
         return;
       }
       
       $.ajax({
         url: '/api/users',
         type: 'POST',
         data: userData,
         success: function(response) {
           $('#successMessage').text('User created successfully!').show();
           $('#userForm').hide();
         },
         error: function(xhr) {
           $('#errorMessage').text('Error: ' + xhr.responseText).show();
         }
       });
     });
     
     function validateEmail(email) {
       var re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
       return re.test(email);
     }
   });
   ```

2. **Migration Planning**
   
   Based on the analysis, write a prompt requesting a step-by-step migration plan that:
   - Outlines a phased approach to migration
   - Identifies which components to migrate first
   - Suggests strategies for testing equivalence between old and new implementations
   - Addresses potential risks and mitigation strategies

3. **Implementation**
   
   Write a prompt requesting the implementation of a specific component in the modern framework, ensuring that:
   - All original functionality is preserved
   - Modern best practices are applied
   - The code is well-documented
   - Tests are included to verify equivalence with the legacy implementation

**Reflection:**
- How effectively did Amazon Q Developer understand the legacy code?
- Did the migration plan address all key concerns?
- How well did the modernized implementation preserve the original functionality?
- What aspects of the migration process were most challenging for Amazon Q Developer?

## Scenario 2: Debugging a Production Issue

**Context:** Your application is experiencing intermittent errors in production that are difficult to reproduce in development environments.

**Exercise:** Use Amazon Q Developer to help diagnose and fix the issue based on logs and error reports.

**Steps:**

1. **Problem Description**
   
   Write a prompt that clearly describes the issue, including:
   - Error messages and stack traces
   - Environment details
   - Frequency and pattern of occurrences
   - Recent code changes that might be related

   Example:
   ```
   Our Node.js API (Express 4.17.1, running on Node 14.17.0) is experiencing intermittent 500 errors in production with the following error message:

   Error: Cannot read property 'id' of undefined
       at /app/services/orderService.js:142:45
       at processTicksAndRejections (internal/process/task_queues.js:95:5)
       at async /app/controllers/orderController.js:87:23

   The issue occurs approximately 3-5 times per hour, usually during peak traffic periods. It only affects the order checkout endpoint (POST /api/orders) and started occurring after we deployed a change to the order processing pipeline yesterday.

   Relevant code from orderService.js:
   ```javascript
   async function processOrder(orderData) {
     const user = await userService.getUserById(orderData.userId);
     const paymentMethod = user.paymentMethods.find(pm => pm.id === orderData.paymentMethodId);
     
     // Line 142 where the error occurs:
     const paymentDetails = await paymentService.processPayment(paymentMethod.id, orderData.amount);
     
     // Rest of the function...
   }
   ```

   We've checked and confirmed that orderData.userId and orderData.paymentMethodId are always present in the request, but the error suggests that either user or user.paymentMethods might be undefined in some cases.
   ```

2. **Root Cause Analysis**
   
   Write a prompt asking Amazon Q Developer to:
   - Analyze the error and code snippet
   - Identify potential root causes
   - Suggest debugging approaches
   - Recommend logging enhancements to gather more information

3. **Solution Implementation**
   
   Based on the analysis, write a prompt requesting:
   - A fix for the identified issue
   - Additional error handling to prevent similar issues
   - Improved logging to help diagnose similar problems in the future
   - A testing strategy to verify the fix

**Reflection:**
- How accurately did Amazon Q Developer identify potential root causes?
- How comprehensive was the suggested fix?
- Did the solution address both the immediate issue and potential future issues?
- What additional information would have helped Amazon Q Developer provide a better solution?

## Scenario 3: Performance Optimization

**Context:** A critical component of your application is experiencing performance issues that impact user experience.

**Exercise:** Use Amazon Q Developer to identify performance bottlenecks and implement optimizations.

**Steps:**

1. **Performance Profile**
   
   Write a prompt that provides:
   - Performance metrics and benchmarks
   - Profiling data if available
   - Code of the component with performance issues
   - System constraints and requirements

   Example:
   ```
   Our product search function is experiencing performance issues. On our catalog of 100,000 products, searches are taking 3-5 seconds to complete, when our target is under 500ms. Here's the current implementation:

   ```javascript
   async function searchProducts(query, filters = {}) {
     const allProducts = await productRepository.getAllProducts();
     
     // Filter products based on search query
     let results = allProducts.filter(product => {
       const matchesQuery = product.name.toLowerCase().includes(query.toLowerCase()) || 
                           product.description.toLowerCase().includes(query.toLowerCase());
       
       if (!matchesQuery) return false;
       
       // Apply additional filters
       for (const [key, value] of Object.entries(filters)) {
         if (Array.isArray(value)) {
           if (!value.includes(product[key])) return false;
         } else {
           if (product[key] !== value) return false;
         }
       }
       
       return true;
     });
     
     // Sort results by relevance (basic implementation)
     results.sort((a, b) => {
       const aNameMatch = a.name.toLowerCase().includes(query.toLowerCase());
       const bNameMatch = b.name.toLowerCase().includes(query.toLowerCase());
       
       if (aNameMatch && !bNameMatch) return -1;
       if (!aNameMatch && bNameMatch) return 1;
       
       return 0;
     });
     
     return results;
   }
   ```

   Our product data structure looks like this:
   ```javascript
   {
     id: "prod-123",
     name: "Ergonomic Office Chair",
     description: "Comfortable chair with lumbar support",
     price: 299.99,
     category: "furniture",
     tags: ["office", "chair", "ergonomic"],
     attributes: {
       color: "black",
       material: "mesh",
       adjustable: true
     },
     inventory: 45,
     created_at: "2023-01-15T00:00:00Z",
     updated_at: "2023-04-22T00:00:00Z"
   }
   ```

   We're using MongoDB as our database, and the products collection has indexes on id, name, and category fields.
   ```

2. **Bottleneck Identification**
   
   Write a prompt asking Amazon Q Developer to:
   - Identify performance bottlenecks in the code
   - Explain why these bottlenecks occur
   - Quantify the impact of each bottleneck
   - Suggest areas for optimization

3. **Optimization Implementation**
   
   Based on the analysis, write a prompt requesting:
   - An optimized version of the component
   - Explanation of each optimization
   - Expected performance improvements
   - Trade-offs made in the optimization process

4. **Verification Strategy**
   
   Write a prompt asking for:
   - A testing strategy to verify performance improvements
   - Benchmarking approaches
   - Monitoring recommendations to track performance in production

**Reflection:**
- How effectively did Amazon Q Developer identify the performance bottlenecks?
- How significant were the suggested optimizations?
- Did the optimized solution maintain the same functionality?
- What additional context would have helped Amazon Q Developer provide better optimizations?

## Scenario 4: API Design and Documentation

**Context:** You're developing a new API that will be used by multiple teams and external partners.

**Exercise:** Use Amazon Q Developer to help design, implement, and document the API.

**Steps:**

1. **Requirements Gathering**
   
   Write a prompt that outlines:
   - The purpose and scope of the API
   - Key functionality that must be supported
   - User types and their needs
   - Technical constraints and preferences

   Example:
   ```
   We're creating a new API for our e-commerce platform that will allow:
   1. Internal teams to manage product inventory
   2. Marketing team to update product promotions
   3. External partners to retrieve product information
   4. Customer-facing applications to display products and handle purchases

   Key requirements:
   - RESTful design following OpenAPI 3.0 standards
   - Authentication using OAuth 2.0
   - Rate limiting for external partners
   - Comprehensive error handling
   - Versioning strategy for future changes
   - Support for filtering, pagination, and sorting
   - Batch operations for efficiency

   Technical constraints:
   - Must be implemented in Node.js with Express
   - Must use PostgreSQL as the database
   - Must be deployable to our Kubernetes cluster
   - Must integrate with our existing logging and monitoring systems
   ```

2. **API Design**
   
   Write a prompt requesting:
   - Endpoint definitions with paths, methods, and parameters
   - Request and response formats
   - Status codes and error handling
   - Authentication and authorization approach
   - Pagination, filtering, and sorting mechanisms

3. **Implementation**
   
   Based on the design, write a prompt requesting implementation of a specific endpoint, including:
   - Controller logic
   - Input validation
   - Business logic
   - Database interactions
   - Error handling
   - Tests

4. **Documentation**
   
   Write a prompt requesting comprehensive API documentation, including:
   - OpenAPI/Swagger specification
   - Usage examples
   - Authentication instructions
   - Rate limiting details
   - Common error scenarios and handling
   - Best practices for API consumers

**Reflection:**
- How well did the API design address all the requirements?
- Was the implementation secure, efficient, and maintainable?
- How comprehensive and clear was the documentation?
- What aspects of API design did Amazon Q Developer handle particularly well or poorly?

## Scenario 5: Refactoring Complex Legacy Code

**Context:** You're working with a complex, monolithic application that needs to be refactored to improve maintainability and enable new features.

**Exercise:** Use Amazon Q Developer to help plan and execute a strategic refactoring.

**Steps:**

1. **Code Analysis**
   
   Write a prompt that provides:
   - A complex code module with multiple responsibilities
   - Context about its role in the larger application
   - Specific issues that make it hard to maintain
   - Constraints that must be respected during refactoring

   Example:
   ```
   This UserManager class has grown over years of development and now handles too many responsibilities. It's become a source of bugs and makes adding new features difficult:

   ```java
   public class UserManager {
       private Database db;
       private EmailService emailService;
       private Logger logger;
       private Cache cache;
       
       public UserManager(Database db, EmailService emailService, Logger logger, Cache cache) {
           this.db = db;
           this.emailService = emailService;
           this.logger = logger;
           this.cache = cache;
       }
       
       public User createUser(String username, String email, String password) {
           logger.log("Creating user: " + username);
           
           // Validate input
           if (username == null || username.length() < 3) {
               throw new ValidationException("Username must be at least 3 characters");
           }
           if (!email.matches("^[A-Za-z0-9+_.-]+@(.+)$")) {
               throw new ValidationException("Invalid email format");
           }
           if (password == null || password.length() < 8) {
               throw new ValidationException("Password must be at least 8 characters");
           }
           
           // Check if user exists
           if (db.query("SELECT * FROM users WHERE username = ?", username).size() > 0) {
               throw new DuplicateUserException("Username already exists");
           }
           if (db.query("SELECT * FROM users WHERE email = ?", email).size() > 0) {
               throw new DuplicateUserException("Email already exists");
           }
           
           // Hash password
           String salt = generateSalt();
           String hashedPassword = hashPassword(password, salt);
           
           // Create user
           User user = new User();
           user.setUsername(username);
           user.setEmail(email);
           user.setPasswordHash(hashedPassword);
           user.setSalt(salt);
           user.setCreatedAt(new Date());
           user.setStatus("active");
           
           // Save to database
           db.execute("INSERT INTO users (username, email, password_hash, salt, created_at, status) VALUES (?, ?, ?, ?, ?, ?)",
                   user.getUsername(), user.getEmail(), user.getPasswordHash(), user.getSalt(), user.getCreatedAt(), user.getStatus());
           
           // Send welcome email
           String emailBody = "Welcome to our service, " + username + "!";
           emailService.sendEmail(email, "Welcome!", emailBody);
           
           // Update cache
           cache.put("user_" + username, user);
           
           logger.log("User created successfully: " + username);
           return user;
       }
       
       public User authenticateUser(String usernameOrEmail, String password) {
           logger.log("Authenticating user: " + usernameOrEmail);
           
           // Find user
           List<Map<String, Object>> results;
           if (usernameOrEmail.contains("@")) {
               results = db.query("SELECT * FROM users WHERE email = ?", usernameOrEmail);
           } else {
               results = db.query("SELECT * FROM users WHERE username = ?", usernameOrEmail);
           }
           
           if (results.size() == 0) {
               logger.log("Authentication failed: user not found");
               throw new AuthenticationException("Invalid credentials");
           }
           
           // Check password
           Map<String, Object> userData = results.get(0);
           String storedHash = (String) userData.get("password_hash");
           String salt = (String) userData.get("salt");
           String hashedPassword = hashPassword(password, salt);
           
           if (!storedHash.equals(hashedPassword)) {
               logger.log("Authentication failed: incorrect password");
               
               // Update failed login attempts
               int failedAttempts = getFailedLoginAttempts(usernameOrEmail) + 1;
               setFailedLoginAttempts(usernameOrEmail, failedAttempts);
               
               if (failedAttempts >= 5) {
                   lockUserAccount(usernameOrEmail);
                   emailService.sendEmail((String) userData.get("email"), 
                           "Account Locked", 
                           "Your account has been locked due to multiple failed login attempts.");
               }
               
               throw new AuthenticationException("Invalid credentials");
           }
           
           // Check if account is locked
           if ("locked".equals(userData.get("status"))) {
               logger.log("Authentication failed: account locked");
               throw new AccountLockedException("Account is locked");
           }
           
           // Reset failed attempts
           setFailedLoginAttempts(usernameOrEmail, 0);
           
           // Update last login
           db.execute("UPDATE users SET last_login = ? WHERE id = ?", 
                   new Date(), userData.get("id"));
           
           // Convert to User object
           User user = new User();
           user.setId((Long) userData.get("id"));
           user.setUsername((String) userData.get("username"));
           user.setEmail((String) userData.get("email"));
           user.setStatus((String) userData.get("status"));
           
           // Update cache
           cache.put("user_" + user.getUsername(), user);
           
           logger.log("Authentication successful: " + usernameOrEmail);
           return user;
       }
       
       // Many more methods for user management...
       public void resetPassword(String email) { /* ... */ }
       public void updateUserProfile(Long userId, Map<String, Object> profileData) { /* ... */ }
       public void deleteUser(Long userId) { /* ... */ }
       public List<User> searchUsers(String query) { /* ... */ }
       public void lockUserAccount(String usernameOrEmail) { /* ... */ }
       public void unlockUserAccount(String usernameOrEmail) { /* ... */ }
       public int getFailedLoginAttempts(String usernameOrEmail) { /* ... */ }
       public void setFailedLoginAttempts(String usernameOrEmail, int attempts) { /* ... */ }
       
       private String generateSalt() { /* ... */ }
       private String hashPassword(String password, String salt) { /* ... */ }
   }
   ```

   Refactoring constraints:
   - Must maintain backward compatibility with existing API consumers
   - Cannot change the database schema
   - Must maintain current security practices
   - Must be done incrementally to allow for continuous deployment
   ```

2. **Refactoring Strategy**
   
   Write a prompt requesting:
   - Analysis of the code's responsibilities and concerns
   - Identification of design patterns that could improve the structure
   - A step-by-step refactoring plan
   - Risk assessment and mitigation strategies

3. **Implementation**
   
   Based on the strategy, write a prompt requesting implementation of a specific refactoring step, such as:
   - Extracting a specific responsibility into a new class
   - Implementing a design pattern
   - Improving error handling or validation
   - Adding tests to verify behavior preservation

4. **Verification**
   
   Write a prompt requesting:
   - Test cases to verify the refactored code maintains the same behavior
   - Code review checklist for the refactoring
   - Performance comparison between original and refactored code

**Reflection:**
- How effectively did Amazon Q Developer identify the code's issues and responsibilities?
- How practical and incremental was the refactoring strategy?
- Did the refactored code maintain the same functionality while improving structure?
- What aspects of the refactoring process were most challenging for Amazon Q Developer?

## Scenario 6: Security Review and Hardening

**Context:** You need to perform a security review of an application before deployment to production.

**Exercise:** Use Amazon Q Developer to identify security vulnerabilities and implement fixes.

**Steps:**

1. **Security Analysis**
   
   Write a prompt that provides:
   - Code snippets from different parts of the application
   - Context about the application's purpose and users
   - Current security measures in place
   - Specific security concerns or compliance requirements

   Example:
   ```
   We're preparing to deploy a Node.js Express application that processes payment information. Please review these key components for security vulnerabilities:

   1. Authentication middleware:
   ```javascript
   function authenticate(req, res, next) {
     const token = req.headers.authorization?.split(' ')[1];
     
     if (!token) {
       return res.status(401).json({ error: 'Authentication required' });
     }
     
     try {
       const decoded = jwt.verify(token, process.env.JWT_SECRET);
       req.user = decoded;
       next();
     } catch (err) {
       return res.status(401).json({ error: 'Invalid token' });
     }
   }
   ```

   2. Payment processing endpoint:
   ```javascript
   app.post('/api/payments', authenticate, (req, res) => {
     const { cardNumber, expiryDate, cvv, amount } = req.body;
     
     // Process payment
     const paymentResult = processPayment(cardNumber, expiryDate, cvv, amount);
     
     // Log transaction
     console.log(`Payment processed: ${amount} for user ${req.user.id}`);
     
     // Store payment record
     const query = `
       INSERT INTO payments (user_id, amount, status, created_at)
       VALUES ('${req.user.id}', ${amount}, '${paymentResult.status}', NOW())
     `;
     
     db.query(query, (err, result) => {
       if (err) {
         console.error('Database error:', err);
         return res.status(500).json({ error: 'Payment failed' });
       }
       
       res.json({ success: true, transactionId: paymentResult.transactionId });
     });
   });
   ```

   3. User input handling:
   ```javascript
   app.get('/api/products', (req, res) => {
     const category = req.query.category;
     const searchTerm = req.query.search;
     
     let query = 'SELECT * FROM products WHERE 1=1';
     
     if (category) {
       query += ` AND category = '${category}'`;
     }
     
     if (searchTerm) {
       query += ` AND (name LIKE '%${searchTerm}%' OR description LIKE '%${searchTerm}%')`;
     }
     
     db.query(query, (err, results) => {
       if (err) {
         return res.status(500).json({ error: 'Database error' });
       }
       
       res.json(results);
     });
   });
   ```

   4. Error handling:
   ```javascript
   app.use((err, req, res, next) => {
     console.error('Application error:', err);
     res.status(500).json({ 
       error: 'An unexpected error occurred', 
       details: err.toString() 
     });
   });
   ```

   Security requirements:
   - Must comply with PCI DSS for payment processing
   - Must protect against OWASP Top 10 vulnerabilities
   - Must implement proper authentication and authorization
   - Must securely handle sensitive data
   ```

2. **Vulnerability Identification**
   
   Write a prompt asking Amazon Q Developer to:
   - Identify all security vulnerabilities in the provided code
   - Explain the potential impact of each vulnerability
   - Categorize vulnerabilities by severity
   - Reference relevant security standards or best practices

3. **Security Hardening**
   
   Based on the identified vulnerabilities, write a prompt requesting:
   - Fixed versions of the vulnerable code
   - Additional security measures to implement
   - Explanation of how each fix addresses the vulnerability
   - Best practices for ongoing security maintenance

4. **Security Testing**
   
   Write a prompt requesting:
   - Test cases to verify the security fixes
   - Approaches for security testing (e.g., penetration testing, static analysis)
   - Monitoring recommendations for security-related events

**Reflection:**
- How comprehensive was Amazon Q Developer's security analysis?
- Did it identify all major security vulnerabilities?
- How effective were the proposed security fixes?
- What security considerations did Amazon Q Developer miss or handle particularly well?

## Key Takeaways

These real-world scenarios demonstrate how to apply prompt engineering techniques to solve common software development challenges. By practicing with these exercises, you'll develop the skills to:

1. **Provide Appropriate Context**: Frame your prompts with relevant background information and constraints.

2. **Break Down Complex Problems**: Divide large tasks into manageable components that can be addressed sequentially.

3. **Iterate and Refine**: Use follow-up prompts to build upon initial responses and address specific aspects of the solution.

4. **Specify Requirements Clearly**: Communicate your needs and expectations explicitly to get more relevant and useful responses.

5. **Evaluate and Improve**: Reflect on the effectiveness of your prompts and continuously refine your prompt engineering techniques.

As you work through these scenarios, remember that effective prompt engineering is both an art and a science. The more you practice, the better you'll become at crafting prompts that elicit high-quality, relevant responses from Amazon Q Developer.

---

[Previous: Advanced Exercises](./03-advanced.md) | [Back to Main](../README.md)
