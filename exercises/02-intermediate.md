# Intermediate Exercises

This section provides more advanced exercises to help you practice intermediate prompt engineering techniques with Amazon Q Developer. These exercises build on the fundamentals and introduce more complex scenarios.

## Exercise 1: Chain of Thought Prompting

**Objective:** Practice guiding Amazon Q Developer through a step-by-step reasoning process.

**Instructions:**
1. Choose a complex programming problem (e.g., implementing a specific algorithm, designing a system component).
2. Write a prompt that guides Amazon Q Developer through a step-by-step approach:
   - Break down the problem into logical steps
   - Ask for reasoning at each step
   - Request consideration of alternatives
   - Ask for evaluation of the final solution

**Example Problem:** Implementing a caching system for expensive API calls

**Example Prompt:**
```
I need to implement a caching system for expensive API calls in a Node.js application. Please help me design and implement this system by following these steps:

1. First, analyze the requirements for an effective API caching system:
   - What key features should it have?
   - What are the important considerations for cache invalidation?
   - What edge cases should be handled?

2. Next, evaluate different caching strategies:
   - In-memory caching (e.g., using Map or a library)
   - Redis-based distributed caching
   - File-based caching
   Compare these approaches and recommend the most suitable one for a medium-sized application.

3. Design the core caching interface:
   - What methods should it expose?
   - How should cache keys be generated?
   - How should timeouts and expiration be handled?

4. Implement the chosen caching solution:
   - Provide the complete implementation
   - Include error handling
   - Add logging for cache hits/misses

5. Finally, demonstrate how to use this caching system with a practical example:
   - Show how to cache results from a third-party API
   - Include proper error handling and fallback strategies

For each step, explain your reasoning and any trade-offs being made.
```

**Reflection Questions:**
- How did the step-by-step approach affect the quality and depth of the response?
- Did Amazon Q Developer provide reasoning for its decisions?
- How did explicitly requesting alternatives and evaluations improve the solution?
- What steps would you add or modify to get an even better response?

## Exercise 2: Few-Shot Learning

**Objective:** Practice using examples to guide Amazon Q Developer's responses.

**Instructions:**
1. Choose a task that benefits from consistent formatting or style (e.g., generating API documentation, writing test cases).
2. Write a prompt that includes 2-3 examples of the desired output format.
3. Request Amazon Q Developer to follow the same pattern for a new case.
4. Evaluate how well it followed the pattern in your examples.

**Example Task:** Generating consistent test cases for API endpoints

**Example Prompt:**
```
I need to write test cases for several API endpoints in my Express.js application using Jest and Supertest. Please follow the exact pattern shown in these examples to create tests for a new endpoint.

Example 1: GET /api/users endpoint test
```javascript
describe('GET /api/users', () => {
  it('should return 200 and an array of users when valid token is provided', async () => {
    // Arrange
    const validToken = generateValidToken();
    
    // Act
    const response = await request(app)
      .get('/api/users')
      .set('Authorization', `Bearer ${validToken}`);
    
    // Assert
    expect(response.status).toBe(200);
    expect(Array.isArray(response.body)).toBe(true);
    expect(response.body[0]).toHaveProperty('id');
    expect(response.body[0]).toHaveProperty('name');
  });

  it('should return 401 when no token is provided', async () => {
    // Act
    const response = await request(app).get('/api/users');
    
    // Assert
    expect(response.status).toBe(401);
    expect(response.body).toHaveProperty('error');
  });

  it('should return 403 when token has insufficient permissions', async () => {
    // Arrange
    const limitedToken = generateLimitedToken();
    
    // Act
    const response = await request(app)
      .get('/api/users')
      .set('Authorization', `Bearer ${limitedToken}`);
    
    // Assert
    expect(response.status).toBe(403);
    expect(response.body).toHaveProperty('error');
  });
}
```

Example 2: POST /api/login endpoint test
```javascript
describe('POST /api/login', () => {
  it('should return 200 and auth token when valid credentials are provided', async () => {
    // Arrange
    const credentials = {
      email: 'test@example.com',
      password: 'validPassword123'
    };
    
    // Act
    const response = await request(app)
      .post('/api/login')
      .send(credentials);
    
    // Assert
    expect(response.status).toBe(200);
    expect(response.body).toHaveProperty('token');
    expect(response.body).toHaveProperty('user');
  });

  it('should return 400 when email is missing', async () => {
    // Arrange
    const credentials = {
      password: 'validPassword123'
    };
    
    // Act
    const response = await request(app)
      .post('/api/login')
      .send(credentials);
    
    // Assert
    expect(response.status).toBe(400);
    expect(response.body).toHaveProperty('error');
  });

  it('should return 401 when credentials are invalid', async () => {
    // Arrange
    const credentials = {
      email: 'test@example.com',
      password: 'wrongPassword'
    };
    
    // Act
    const response = await request(app)
      .post('/api/login')
      .send(credentials);
    
    // Assert
    expect(response.status).toBe(401);
    expect(response.body).toHaveProperty('error');
  });
}
```

Now, please create test cases following the exact same pattern for this new endpoint:

POST /api/orders - Creates a new order
- Requires authentication token
- Request body should include: items (array of product IDs with quantities), shippingAddress (object), paymentMethodId (string)
- Returns 201 and the created order on success
- Returns 400 if request body is invalid
- Returns 401 if not authenticated
- Returns 409 if any product is out of stock
```

**Reflection Questions:**
- How closely did Amazon Q Developer follow the pattern in your examples?
- What aspects of the examples were most effective in guiding the response?
- What would you change about your examples to get an even more consistent result?

## Exercise 3: Iterative Refinement

**Objective:** Practice refining solutions through multiple iterations.

**Instructions:**
1. Choose a complex programming task (e.g., building a specific component or feature).
2. Start with a basic prompt requesting an initial solution.
3. Evaluate the response and identify specific aspects to improve.
4. Write follow-up prompts that focus on refining those aspects.
5. Continue the iterative process for at least 3 rounds.

**Example Task:** Building a data visualization component

**Initial Prompt:**
```
Create a React component that displays a bar chart for visualizing monthly sales data.
```

**First Refinement:**
```
Thanks for the initial bar chart component. I'd like to refine it with these improvements:

1. Add responsive design so the chart looks good on both mobile and desktop
2. Include proper TypeScript type definitions for all props and functions
3. Add the ability to customize colors for the bars
4. Implement smooth animations when data changes

Please update the component with these enhancements.
```

**Second Refinement:**
```
The responsive design and TypeScript definitions look good, but I'd like to further enhance this component:

1. Add accessibility features:
   - Proper ARIA attributes
   - Keyboard navigation
   - Screen reader support for the chart data

2. Improve the performance:
   - Memoize expensive calculations
   - Optimize rendering for large datasets
   - Add virtualization for charts with many bars

3. Add comprehensive error handling:
   - Graceful handling of missing or malformed data
   - Fallback display when rendering fails
   - Helpful error messages for developers

Please update the component with these enhancements and explain the changes you've made.
```

**Third Refinement:**
```
The component is coming along nicely. For the final refinement, please:

1. Add comprehensive documentation:
   - JSDoc comments for all props, methods, and types
   - Usage examples for common scenarios
   - Performance considerations and best practices

2. Add testing:
   - Unit tests for core functionality
   - Tests for edge cases and error handling
   - Accessibility tests

3. Implement additional features:
   - Tooltip on hover with detailed information
   - Option to display data labels on bars
   - Support for horizontal bar orientation

Please provide the final version of the component with these enhancements.
```

**Reflection Questions:**
- How did the solution evolve through the iterations?
- Which refinements had the biggest impact on the quality of the solution?
- What was more effective: asking for many changes at once or focusing on specific aspects in each iteration?
- How would you approach the iterative process differently next time?

## Exercise 4: Task Decomposition

**Objective:** Practice breaking down complex problems into manageable parts.

**Instructions:**
1. Choose a complex system or application to build (e.g., a project management tool, an e-commerce platform).
2. Write a prompt that breaks down the development into logical components or phases.
3. For one specific component, request a detailed implementation.
4. Evaluate how well the decomposition helped in getting a quality implementation.

**Example Task:** Building a task management application

**Example Prompt:**
```
I want to build a task management application with React and Node.js. Let's break this down into logical components:

1. User Authentication System:
   - User registration and login
   - Password reset functionality
   - JWT-based authentication
   - Role-based access control

2. Task Management Core:
   - Task creation, editing, and deletion
   - Task categorization and tagging
   - Task assignment to users
   - Due date and priority management

3. Project Organization:
   - Project creation and management
   - User roles within projects
   - Task grouping within projects
   - Project progress tracking

4. Notification System:
   - Due date reminders
   - Assignment notifications
   - Comment and mention alerts
   - Email and in-app notifications

5. User Interface Components:
   - Dashboard with task overview
   - Kanban board view
   - Calendar view
   - List view with filtering and sorting

6. API and Data Management:
   - RESTful API design
   - Database schema
   - Data validation
   - Error handling

Now, I'd like to focus on implementing component #2: Task Management Core. Please provide:

1. A detailed design for the Task Management Core, including:
   - Data models for tasks, categories, and tags
   - Required API endpoints
   - Key functions and their purposes

2. Frontend implementation:
   - React components for task CRUD operations
   - State management approach
   - Form validation

3. Backend implementation:
   - Express routes for the task API
   - Controller functions
   - Database interactions
   - Validation and error handling

Please provide complete, production-ready code for this component with appropriate comments and error handling.
```

**Reflection Questions:**
- How did breaking down the system help in getting a focused implementation?
- Was the level of detail in the decomposition appropriate?
- What aspects of the decomposition were most helpful for Amazon Q Developer?
- How would you improve the decomposition for future prompts?

## Exercise 5: Comparative Analysis

**Objective:** Practice requesting and evaluating multiple approaches to a problem.

**Instructions:**
1. Choose a technical problem with multiple potential solutions (e.g., state management in a frontend application, database schema design).
2. Write a prompt requesting multiple approaches to solving the problem.
3. Ask for a comparative analysis of the approaches based on specific criteria.
4. Request a recommendation based on your specific requirements.

**Example Task:** Choosing a state management approach for a React application

**Example Prompt:**
```
I'm building a medium-sized React application for managing employee schedules and need to choose an appropriate state management approach. The application will have:

- About 20-30 different screens/views
- Real-time updates for schedule changes
- Form-heavy interfaces for schedule creation
- User permissions affecting what data can be viewed/edited
- Need to share state between distant components
- Requirement to persist some state in local storage

Please provide a comparative analysis of these state management approaches:
1. React Context + useReducer
2. Redux (with Redux Toolkit)
3. MobX
4. Recoil
5. Zustand

For each approach, please analyze:
- Learning curve and developer experience
- Performance characteristics with medium-sized state
- Handling of asynchronous operations
- DevTools and debugging capabilities
- Testing approaches
- TypeScript integration
- Code maintainability for a team of 5 developers with varying React experience

After the comparison, please recommend the most suitable approach for my specific requirements and explain your reasoning. Include a simple example of how a typical state update flow would look with your recommended approach.
```

**Reflection Questions:**
- How thorough was the comparative analysis?
- Did Amazon Q Developer consider all the criteria you specified?
- Was the recommendation well-justified based on your requirements?
- What additional information could you have provided to get a more tailored recommendation?

## Exercise 6: Security-Focused Requirements

**Objective:** Practice incorporating security requirements into your prompts.

**Instructions:**
1. Choose a common web development task (e.g., user authentication, file uploads, form handling).
2. Write a prompt that emphasizes security requirements and best practices.
3. Evaluate the response for security considerations and implementation.
4. Identify any security aspects that were missed and refine your prompt.

**Example Task:** Implementing file uploads

**Example Prompt:**
```
I need to implement a secure file upload feature for a Node.js/Express application with the following security requirements:

1. File Validation:
   - Restrict uploads to specific file types (images, PDFs, and office documents only)
   - Validate file content type (not just extension)
   - Implement file size limits (max 10MB)
   - Scan uploaded files for malware (suggest appropriate libraries)

2. Storage Security:
   - Store files outside the web root
   - Use randomized filenames to prevent guessing
   - Maintain a database of file metadata separate from the files
   - Implement proper file permissions

3. Access Control:
   - Require authentication for file uploads
   - Implement authorization checks for file access
   - Create signed URLs for temporary access
   - Track file access and modifications

4. Frontend Security:
   - Implement client-side validation (as a usability feature, not security control)
   - Show progress and validation feedback
   - Handle errors securely without exposing system details

5. Additional Security Measures:
   - Rate limiting to prevent abuse
   - Implement proper error handling and logging
   - CSRF protection for upload forms
   - Consider content disposition headers for downloads

Please provide a complete implementation including:
- Backend code for handling uploads securely
- Database schema for file metadata
- Frontend component for file uploads with progress indication
- Configuration for secure file storage
- Error handling for security-related failures

For each security measure, explain why it's important and how it mitigates specific risks.
```

**Reflection Questions:**
- How well did Amazon Q Developer address the security requirements?
- Were there any security best practices that were missed?
- Did the response include explanations of why each security measure is important?
- How would you improve your prompt to get more security-focused results?

## Exercise 7: Performance Optimization

**Objective:** Practice requesting performance-optimized solutions.

**Instructions:**
1. Choose a performance-sensitive task (e.g., data processing, rendering large lists, complex calculations).
2. Write a prompt that emphasizes performance requirements and constraints.
3. Evaluate the response for performance considerations and optimizations.
4. Request benchmarking or complexity analysis to validate the performance.

**Example Task:** Optimizing a function that processes large datasets

**Example Prompt:**
```
I need to optimize a JavaScript function that processes large datasets with the following performance requirements:

Current function (needs optimization):
```javascript
function processTransactions(transactions) {
  let results = [];
  
  for (let i = 0; i < transactions.length; i++) {
    const transaction = transactions[i];
    
    // Filter by transaction type
    if (transaction.type === 'purchase' || transaction.type === 'refund') {
      // Calculate total with tax
      const total = transaction.amount * (1 + transaction.taxRate);
      
      // Group by customer
      let customer = results.find(r => r.customerId === transaction.customerId);
      if (!customer) {
        customer = {
          customerId: transaction.customerId,
          transactions: [],
          totalSpent: 0
        };
        results.push(customer);
      }
      
      // Add transaction and update total
      customer.transactions.push({
        id: transaction.id,
        amount: total,
        date: transaction.date,
        type: transaction.type
      });
      
      if (transaction.type === 'purchase') {
        customer.totalSpent += total;
      } else if (transaction.type === 'refund') {
        customer.totalSpent -= total;
      }
    }
  }
  
  // Sort customers by total spent
  results.sort((a, b) => b.totalSpent - a.totalSpent);
  
  return results;
}
```

Performance context:
- This function needs to process datasets with up to 1 million transactions
- It's called frequently in a web application
- Current implementation causes noticeable UI freezing
- Memory usage is also a concern

Optimization requirements:
1. Improve time complexity
2. Reduce memory usage
3. Avoid UI blocking (consider chunking or async processing)
4. Maintain the exact same output format and behavior

Please provide:
1. An optimized version of the function with detailed comments explaining each optimization
2. Time and space complexity analysis of both the original and optimized versions
3. Explanation of the performance bottlenecks in the original code
4. Suggestions for measuring and benchmarking the performance improvement
5. Any trade-offs made in your optimization approach

The solution should prioritize real-world performance over minor code simplifications.
```

**Reflection Questions:**
- How well did Amazon Q Developer identify and address the performance bottlenecks?
- Did the response include meaningful complexity analysis?
- Were the optimizations practical and maintainable?
- What additional performance requirements could you specify to get even better results?

## Next Steps

After completing these intermediate exercises, you should have a stronger grasp of advanced prompt engineering techniques. In the next section, we'll explore advanced exercises that challenge you to apply these skills in more complex scenarios.

---

[Next: Advanced Exercises](./03-advanced.md) | [Previous: Beginner Exercises](./01-beginner.md) | [Back to Main](../README.md)
