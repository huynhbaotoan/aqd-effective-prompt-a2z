# Code Generation Examples

This section provides practical examples of effective prompts for generating code with Amazon Q Developer. Each example demonstrates key prompt engineering techniques and best practices.

## Basic Code Generation

### Example 1: Simple Function

**Prompt:**
```
Create a JavaScript function that calculates the Fibonacci sequence up to n terms.
```

**Improved Prompt:**
```
Create a JavaScript function that calculates the Fibonacci sequence up to n terms.

Requirements:
- Function name should be 'generateFibonacci'
- It should take a single parameter 'n' (number of terms)
- It should return an array containing the Fibonacci sequence
- It should handle edge cases (n <= 0)
- It should be optimized for performance

Example usage:
generateFibonacci(7) should return [0, 1, 1, 2, 3, 5, 8]
```

**Why It's Better:**
- Specifies function name and signature
- Clearly defines the return value
- Mentions edge case handling
- Includes performance considerations
- Provides an example of expected output

### Example 2: Class Implementation

**Prompt:**
```
Create a Python class for a bank account.
```

**Improved Prompt:**
```
Create a Python class for a bank account with the following specifications:

Class name: BankAccount

Properties:
- account_number (string)
- account_holder (string)
- balance (float, default 0.0)
- account_type (string, either "checking" or "savings")

Methods:
- deposit(amount): Adds amount to balance, returns new balance
- withdraw(amount): Subtracts amount from balance if sufficient funds, returns new balance or raises InsufficientFundsError
- get_balance(): Returns current balance
- transfer(target_account, amount): Transfers amount to another account if sufficient funds

Requirements:
- Include proper validation for all inputs
- Implement proper error handling
- Use Python 3.8+ features
- Include docstrings following Google style guide
- Implement __str__ and __repr__ methods

Example usage:
```python
# Create accounts
account1 = BankAccount("123456", "John Doe", 1000.0, "checking")
account2 = BankAccount("789012", "Jane Smith", 500.0, "savings")

# Perform operations
account1.deposit(500.0)  # Balance: 1500.0
account1.transfer(account2, 300.0)  # account1: 1200.0, account2: 800.0
```
```

**Why It's Better:**
- Specifies class name, properties, and methods
- Defines method behaviors and return values
- Includes validation and error handling requirements
- Specifies documentation style
- Provides example usage

## Intermediate Code Generation

### Example 3: API Endpoint

**Prompt:**
```
Create an Express.js API endpoint for user registration.
```

**Improved Prompt:**
```
Create an Express.js API endpoint for user registration with the following specifications:

Endpoint: POST /api/users/register

Request body:
```json
{
  "username": "string (required, 3-20 alphanumeric characters)",
  "email": "string (required, valid email format)",
  "password": "string (required, min 8 chars, must contain letters, numbers, and special chars)",
  "firstName": "string (optional)",
  "lastName": "string (optional)"
}
```

Response (Success - 201 Created):
```json
{
  "id": "uuid",
  "username": "string",
  "email": "string",
  "firstName": "string (if provided)",
  "lastName": "string (if provided)",
  "createdAt": "ISO datetime string"
}
```

Response (Error - 400 Bad Request):
```json
{
  "error": "string (error message)",
  "details": {
    "field": "string (field with error)",
    "message": "string (specific error message)"
  }
}
```

Implementation requirements:
- Use Express.js with async/await syntax
- Validate request body using express-validator
- Hash passwords using bcrypt (10 salt rounds)
- Store user in MongoDB using Mongoose
- Check for existing users with the same username or email
- Return appropriate HTTP status codes and error messages
- Do not include password in the response
- Use proper error handling middleware

Security considerations:
- Implement rate limiting to prevent brute force attacks
- Validate and sanitize all inputs
- Use HTTPS for the API in production
- Set appropriate security headers

Example usage:
```javascript
// Example of how the endpoint should be used in the Express app
app.use('/api/users', userRoutes);

// In userRoutes.js
router.post('/register', validateRegistration, userController.register);
```

Please provide the complete implementation including the controller, validation middleware, and any necessary models.
```

**Why It's Better:**
- Specifies endpoint path and HTTP method
- Defines request and response formats in detail
- Includes validation requirements
- Specifies error handling approach
- Includes security considerations
- Provides example usage
- Requests complete implementation with all necessary components

### Example 4: Data Processing Function

**Prompt:**
```
Write a Python function to process CSV data.
```

**Improved Prompt:**
```
Create a Python function to process CSV data with the following specifications:

Function name: process_sales_data

Purpose: The function should process a CSV file containing sales data, perform calculations, and output summary statistics.

Input CSV format:
- Headers: date,product_id,product_name,category,quantity,unit_price,customer_id
- Date format: YYYY-MM-DD
- Example row: 2023-04-15,PRD-123,Laptop X1,Electronics,2,1200.00,CUST-456

Function parameters:
- input_file_path (str): Path to the input CSV file
- output_file_path (str): Path to save the output CSV file
- start_date (str, optional): Filter data starting from this date (YYYY-MM-DD)
- end_date (str, optional): Filter data until this date (YYYY-MM-DD)
- categories (list, optional): List of categories to include

Function should:
1. Read the CSV file using the csv module or pandas
2. Filter data based on date range and categories if provided
3. Calculate total sales per product (quantity * unit_price)
4. Group data by category and calculate:
   - Total revenue per category
   - Average order value per category
   - Top selling product per category
   - Number of unique customers per category
5. Output a summary CSV with headers: category,total_revenue,avg_order_value,top_product,unique_customers
6. Return a dictionary with overall statistics:
   - total_revenue: sum of all sales
   - total_orders: count of unique order combinations
   - top_category: category with highest revenue
   - date_range: actual date range in the processed data

Error handling:
- Handle file not found errors
- Handle malformed CSV data
- Validate date formats
- Provide meaningful error messages

Performance considerations:
- Efficiently process large files (potentially millions of rows)
- Minimize memory usage
- Use appropriate data structures for aggregations

Example usage:
```python
stats = process_sales_data(
    input_file_path="sales_2023_q1.csv",
    output_file_path="sales_summary_2023_q1.csv",
    start_date="2023-01-01",
    end_date="2023-03-31",
    categories=["Electronics", "Furniture"]
)
print(f"Total Revenue: ${stats['total_revenue']:,.2f}")
print(f"Top Category: {stats['top_category']}")
```

Please provide a complete implementation with appropriate comments and error handling.
```

**Why It's Better:**
- Specifies function name and purpose
- Defines input and output formats in detail
- Provides clear processing steps
- Includes error handling requirements
- Addresses performance considerations
- Provides example usage
- Requests complete implementation with comments

## Advanced Code Generation

### Example 5: Design Pattern Implementation

**Prompt:**
```
Implement a factory pattern in Java.
```

**Improved Prompt:**
```
Implement a Factory Method design pattern in Java for a payment processing system with the following specifications:

Context:
We're building a payment processing system that needs to support multiple payment methods (Credit Card, PayPal, Bank Transfer, Cryptocurrency). Each payment method has different processing logic, validation rules, and transaction fees.

Requirements:

1. Create an abstract Product interface/class:
   - Interface name: PaymentProcessor
   - Methods:
     - validatePayment(PaymentDetails details): boolean
     - processPayment(PaymentDetails details): PaymentResult
     - calculateFees(double amount): double

2. Create Concrete Products:
   - CreditCardProcessor
   - PayPalProcessor
   - BankTransferProcessor
   - CryptocurrencyProcessor
   - Each should implement the PaymentProcessor interface with appropriate logic

3. Create an abstract Creator class:
   - Class name: PaymentProcessorFactory
   - Abstract method: createPaymentProcessor(PaymentMethod method): PaymentProcessor
   - Helper method: processPayment(PaymentMethod method, PaymentDetails details): PaymentResult

4. Create a Concrete Creator:
   - DefaultPaymentProcessorFactory that implements PaymentProcessorFactory
   - Should create the appropriate processor based on the payment method

5. Create necessary supporting classes:
   - PaymentMethod enum (CREDIT_CARD, PAYPAL, BANK_TRANSFER, CRYPTOCURRENCY)
   - PaymentDetails class with appropriate fields for different payment methods
   - PaymentResult class to represent the outcome of a payment

Implementation details:
- Use Java 11+ features
- Follow SOLID principles
- Include proper exception handling
- Add appropriate validation in each processor
- Include unit tests for the factory and at least one processor
- Use meaningful comments and documentation

Example usage:
```java
PaymentProcessorFactory factory = new DefaultPaymentProcessorFactory();
PaymentDetails details = new PaymentDetails("john@example.com", 100.00, "USD");
details.setCreditCardNumber("4111111111111111");
details.setExpiryDate("12/25");
details.setCvv("123");

PaymentResult result = factory.processPayment(PaymentMethod.CREDIT_CARD, details);
if (result.isSuccessful()) {
    System.out.println("Payment processed successfully. Transaction ID: " + result.getTransactionId());
} else {
    System.out.println("Payment failed: " + result.getErrorMessage());
}
```

Please provide a complete implementation of all required classes and interfaces.
```

**Why It's Better:**
- Provides specific context for the design pattern
- Defines all components of the pattern
- Specifies class names, methods, and relationships
- Includes implementation details and requirements
- Follows SOLID principles
- Requests unit tests
- Provides example usage
- Asks for complete implementation

### Example 6: Full-Stack Feature

**Prompt:**
```
Create a user dashboard feature.
```

**Improved Prompt:**
```
Create a full-stack implementation for a user dashboard feature with the following specifications:

## Feature Overview
The dashboard will display a summary of a user's activity, including recent orders, account information, and personalized recommendations.

## Frontend Requirements (React)

Components:
1. Dashboard container component
   - Responsive layout (mobile, tablet, desktop)
   - Navigation tabs for different sections

2. UserProfile component
   - Display name, email, profile picture
   - Edit profile functionality
   - Account settings section

3. RecentOrders component
   - Table/list of recent orders
   - Sorting and filtering options
   - Pagination (5 items per page)
   - Order details expansion/modal

4. Analytics component
   - Display spending patterns using charts
   - Monthly purchase summary
   - Category breakdown with Chart.js

5. Recommendations component
   - Product cards for recommended items
   - "Add to cart" functionality

Technical specifications:
- Use React 18 with functional components and hooks
- State management with Redux Toolkit
- Styling with Tailwind CSS
- Form handling with Formik and Yup validation
- Responsive design with mobile-first approach
- Implement proper loading states and error handling
- Use React Router for tab navigation

## Backend Requirements (Node.js/Express)

API Endpoints:
1. GET /api/dashboard/summary
   - Return user profile, activity summary, and stats

2. GET /api/dashboard/orders
   - Query parameters: page, limit, sort, filter
   - Return paginated order history

3. GET /api/dashboard/analytics
   - Query parameters: timeframe (week, month, year)
   - Return spending analytics data

4. GET /api/dashboard/recommendations
   - Return personalized product recommendations

5. PUT /api/dashboard/profile
   - Update user profile information

Technical specifications:
- RESTful API design
- Express.js with middleware pattern
- MongoDB with Mongoose for data storage
- JWT authentication
- Input validation with express-validator
- Error handling middleware
- Rate limiting for API endpoints

## Data Models

1. User model:
   - Basic fields: id, name, email, password (hashed)
   - Profile fields: address, phone, preferences
   - Account fields: createdAt, lastLogin, status

2. Order model:
   - Basic fields: id, userId, status, totalAmount
   - Items: array of products with quantity and price
   - Timestamps: createdAt, updatedAt
   - Shipping and billing information

3. Product model (for recommendations):
   - Basic fields: id, name, description, price
   - Category, tags, image URLs
   - Inventory information

## Security Considerations
- Implement proper authentication and authorization
- Secure API endpoints with JWT verification
- Validate and sanitize all inputs
- Implement CSRF protection
- Set secure HTTP headers

## Performance Considerations
- Implement caching for dashboard data
- Optimize database queries
- Lazy load components when appropriate
- Implement virtual scrolling for long lists
- Use pagination for large datasets

Please provide the implementation for both frontend and backend components, focusing on code quality, best practices, and maintainability.
```

**Why It's Better:**
- Provides comprehensive feature overview
- Breaks down requirements into frontend and backend
- Specifies components, endpoints, and data models
- Includes technical specifications for each part
- Addresses security and performance considerations
- Requests complete implementation with best practices

## Specialized Code Generation

### Example 7: Algorithm Implementation

**Prompt:**
```
Implement a graph traversal algorithm.
```

**Improved Prompt:**
```
Implement Dijkstra's shortest path algorithm in Python with the following specifications:

Function signature:
```python
def dijkstra_shortest_path(graph, start_node, end_node):
    """
    Find the shortest path between start_node and end_node in a weighted graph.
    
    Args:
        graph: A dictionary representing a weighted graph where:
               - Keys are node names
               - Values are dictionaries mapping connected nodes to edge weights
               Example: {'A': {'B': 5, 'C': 3}, 'B': {'A': 5, 'D': 2}, ...}
        start_node: The starting node name
        end_node: The target node name
        
    Returns:
        A tuple containing:
        - The shortest distance from start_node to end_node (float or int)
        - The path as a list of nodes from start_node to end_node
        - If no path exists, return (float('inf'), [])
    """
```

Requirements:
1. Implement the classic Dijkstra's algorithm using a priority queue
2. Use the heapq module for the priority queue implementation
3. Handle edge cases:
   - Nodes not in graph
   - Unreachable end_node
   - Negative edge weights (optional: detect and raise an error)
   - Self-loops and parallel edges
4. Optimize for performance with large graphs
5. Include clear comments explaining the algorithm steps
6. Add time and space complexity analysis

Example test cases:
```python
# Test case 1: Simple graph
graph1 = {
    'A': {'B': 5, 'C': 3},
    'B': {'A': 5, 'D': 2},
    'C': {'A': 3, 'D': 6, 'E': 8},
    'D': {'B': 2, 'C': 6, 'E': 4},
    'E': {'C': 8, 'D': 4}
}
assert dijkstra_shortest_path(graph1, 'A', 'E') == (11, ['A', 'C', 'D', 'E'])

# Test case 2: Unreachable node
graph2 = {
    'A': {'B': 5},
    'B': {'A': 5},
    'C': {'D': 3},
    'D': {'C': 3}
}
assert dijkstra_shortest_path(graph2, 'A', 'C') == (float('inf'), [])

# Test case 3: Start and end are the same
graph3 = {
    'A': {'B': 5},
    'B': {'A': 5}
}
assert dijkstra_shortest_path(graph3, 'A', 'A') == (0, ['A'])
```

Additional considerations:
- Focus on readability and maintainability
- Include docstrings and type hints
- Avoid using external libraries beyond the standard library
- Consider edge cases like disconnected graphs

Please provide a complete implementation with explanatory comments and the time/space complexity analysis.
```

**Why It's Better:**
- Specifies the exact algorithm to implement
- Provides detailed function signature with docstring
- Includes specific requirements and constraints
- Provides test cases to validate the implementation
- Requests complexity analysis
- Addresses edge cases
- Focuses on readability and maintainability

### Example 8: Testing Framework

**Prompt:**
```
Write tests for a user authentication system.
```

**Improved Prompt:**
```
Create a comprehensive test suite for a Node.js user authentication system using Jest and Supertest with the following specifications:

## System Under Test
The authentication system provides these endpoints:
- POST /api/auth/register - User registration
- POST /api/auth/login - User login
- GET /api/auth/me - Get current user info
- POST /api/auth/logout - User logout
- POST /api/auth/refresh-token - Refresh access token
- POST /api/auth/forgot-password - Password reset request
- POST /api/auth/reset-password - Reset password with token

## Test Requirements

1. Unit Tests:
   - Test the User model validation
   - Test password hashing functions
   - Test token generation and verification
   - Test authentication middleware

2. Integration Tests:
   - Test the registration process
   - Test the login process
   - Test token refresh flow
   - Test password reset flow
   - Test authentication middleware with routes

3. API Tests:
   - Test all endpoints with valid inputs
   - Test all endpoints with invalid inputs
   - Test authentication and authorization flows
   - Test rate limiting

## Test Cases to Include

For each endpoint, include tests for:
- Successful operation
- Invalid input validation
- Missing required fields
- Unauthorized access
- Server errors (using mocks)

Specific test scenarios:
- Register with valid data → should create user and return tokens
- Register with existing email → should return 409 Conflict
- Login with valid credentials → should return tokens
- Login with invalid credentials → should return 401 Unauthorized
- Access protected route with valid token → should succeed
- Access protected route with invalid token → should return 401
- Access protected route with expired token → should return 401
- Refresh token flow → should provide new access token
- Password reset flow → should allow changing password

## Technical Requirements
- Use Jest as the test framework
- Use Supertest for API testing
- Implement test database setup and teardown
- Use mocks for external services
- Organize tests in a logical structure
- Include setup and teardown hooks
- Use descriptive test names following the pattern "should [expected behavior] when [condition]"
- Implement proper assertion messages

## Mock Requirements
- Create mock implementations for:
  - Email service
  - Token generation service
  - External authentication providers

## Example Test Structure
```javascript
describe('Authentication API', () => {
  describe('POST /api/auth/register', () => {
    it('should create a new user when valid data is provided', async () => {
      // Test implementation
    });
    
    it('should return 409 when email already exists', async () => {
      // Test implementation
    });
    
    // More test cases...
  });
  
  // More endpoint tests...
});
```

Please provide the complete test suite implementation, including necessary setup, teardown, and mock implementations.
```

**Why It's Better:**
- Specifies the system under test in detail
- Breaks down test requirements by type
- Provides specific test cases to implement
- Includes technical requirements and mock requirements
- Provides example test structure
- Requests complete implementation with setup and teardown

## Key Takeaways

1. **Be Specific**: Clearly define function names, parameters, return values, and behavior.

2. **Provide Context**: Explain the purpose and context of the code to be generated.

3. **Include Requirements**: Specify technical requirements, constraints, and expectations.

4. **Address Edge Cases**: Mention how edge cases and errors should be handled.

5. **Give Examples**: Provide examples of inputs and expected outputs.

6. **Consider Performance**: Include performance considerations and optimization requirements.

7. **Request Complete Solutions**: Ask for complete implementations with all necessary components.

8. **Specify Testing**: Request tests or test cases to validate the implementation.

9. **Use Structured Formats**: Organize complex prompts with clear sections and formatting.

10. **Balance Detail and Clarity**: Provide enough detail without overwhelming the prompt.

## Next Steps

In the next section, we'll explore examples of prompts for code explanation tasks.

---

[Next: Code Explanation Examples](./02-code-explanation.md) | [Previous: Performance Optimization](../best-practices/04-performance.md) | [Back to Main](../README.md)
