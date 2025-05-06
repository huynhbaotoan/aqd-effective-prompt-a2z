# Debugging Examples

This section provides practical examples of effective prompts for debugging code with Amazon Q Developer. Each example demonstrates key prompt engineering techniques and best practices for identifying and fixing issues in code.

## Basic Debugging

### Example 1: Syntax Error Debugging

**Prompt:**
```
Fix this code:

function calculateTotal(items) {
  let total = 0;
  for (let i = 0; i < items.length; i++ {
    total += items[i].price * items[i].quantity;
  }
  return total
}
```

**Improved Prompt:**
```
Fix the syntax errors in this JavaScript function that calculates the total price of items:

```javascript
function calculateTotal(items) {
  let total = 0;
  for (let i = 0; i < items.length; i++ {
    total += items[i].price * items[i].quantity;
  }
  return total
}
```

Please:
1. Identify each syntax error in the code
2. Explain why each is an error
3. Provide the corrected version of the function
4. Explain how JavaScript's parser would report these errors
5. Suggest best practices to avoid these types of errors in the future (e.g., linting tools, IDE features)

Example usage of the function:
```javascript
const shoppingCart = [
  { name: 'Shirt', price: 20, quantity: 2 },
  { name: 'Pants', price: 30, quantity: 1 },
  { name: 'Shoes', price: 50, quantity: 1 }
];

const total = calculateTotal(shoppingCart); // Should return 120
```
```

**Why It's Better:**
- Specifies that the issue is syntax errors
- Requests identification and explanation of each error
- Asks for the corrected version
- Requests explanation of how errors would be reported
- Asks for best practices to avoid similar errors
- Provides example usage to clarify the function's purpose

### Example 2: Logic Error Debugging

**Prompt:**
```
Debug this function:

function findAverage(numbers) {
  let sum = 0;
  for (let i = 1; i < numbers.length; i++) {
    sum += numbers[i];
  }
  return sum / numbers.length;
}
```

**Improved Prompt:**
```
Debug this JavaScript function that calculates the average of an array of numbers but produces incorrect results:

```javascript
function findAverage(numbers) {
  let sum = 0;
  for (let i = 1; i < numbers.length; i++) {
    sum += numbers[i];
  }
  return sum / numbers.length;
}
```

Test cases that reveal the issue:
```javascript
console.log(findAverage([10, 20, 30, 40])); // Expected: 25, Actual: ?
console.log(findAverage([5])); // Expected: 5, Actual: ?
console.log(findAverage([])); // Expected: NaN or 0, Actual: ?
```

Please:
1. Identify the logical error(s) in the function
2. Explain why the function produces incorrect results
3. Provide a fixed version of the function
4. Explain your debugging process and reasoning
5. Suggest how unit tests could have caught this issue
6. Provide test cases that verify the fixed function works correctly

I'm a beginner JavaScript developer learning about debugging, so please explain your thought process in detail.
```

**Why It's Better:**
- Specifies that the issue is logical errors
- Provides test cases that reveal the issue
- Asks for identification and explanation of the errors
- Requests a fixed version
- Asks for explanation of the debugging process
- Requests test cases for verification
- Provides context about the reader's experience level

## Intermediate Debugging

### Example 3: Asynchronous Code Debugging

**Prompt:**
```
Fix this async code:

async function fetchUserData() {
  const response = await fetch('/api/users');
  const data = response.json();
  return data;
}
```

**Improved Prompt:**
```
Debug this JavaScript async function that fetches user data but may not be handling promises correctly:

```javascript
async function fetchUserData() {
  const response = await fetch('/api/users');
  const data = response.json();
  return data;
}
```

Expected behavior:
The function should fetch user data from the API and return the parsed JSON data.

Observed issue:
When using this function, the returned data is not the actual user data but a Promise object.

Example usage:
```javascript
async function displayUsers() {
  const users = await fetchUserData();
  console.log(users); // Logs a Promise object instead of the actual data
}
```

Please:
1. Identify the issue with the async/await usage in the function
2. Explain why the function returns a Promise instead of the resolved data
3. Provide a corrected version of the function
4. Explain the correct pattern for handling promises with async/await
5. Suggest additional error handling improvements
6. Show how to properly use the fixed function

Additional context:
- The fetch API returns a Promise that resolves to a Response object
- The Response.json() method returns a Promise that resolves to the parsed JSON
- This code is running in a modern browser environment
```

**Why It's Better:**
- Specifies that the issue is with asynchronous code
- Describes the expected behavior and observed issue
- Provides example usage showing the problem
- Asks for identification and explanation of the issue
- Requests a corrected version
- Asks for explanation of the correct pattern
- Provides additional context about the fetch API

### Example 4: Performance Debugging

**Prompt:**
```
Fix the performance issue:

function findDuplicates(array) {
  const duplicates = [];
  for (let i = 0; i < array.length; i++) {
    for (let j = i + 1; j < array.length; j++) {
      if (array[i] === array[j] && !duplicates.includes(array[i])) {
        duplicates.push(array[i]);
      }
    }
  }
  return duplicates;
}
```

**Improved Prompt:**
```
Optimize this JavaScript function that finds duplicates in an array but has performance issues with large inputs:

```javascript
function findDuplicates(array) {
  const duplicates = [];
  for (let i = 0; i < array.length; i++) {
    for (let j = i + 1; j < array.length; j++) {
      if (array[i] === array[j] && !duplicates.includes(array[i])) {
        duplicates.push(array[i]);
      }
    }
  }
  return duplicates;
}
```

Performance issues observed:
- With an array of 10,000 elements, the function takes several seconds to complete
- CPU usage spikes to 100% during execution
- For larger arrays, the browser may become unresponsive

Analysis of the current implementation:
- The nested loops create O(n²) time complexity
- The includes() method adds additional iterations
- For each duplicate found, another O(n) operation is performed

Please:
1. Identify all performance bottlenecks in the code
2. Explain why each bottleneck impacts performance
3. Provide an optimized version with better time complexity
4. Analyze the time and space complexity of your optimized solution
5. Compare the performance characteristics of the original and optimized versions
6. Suggest how to benchmark both implementations
7. Explain any trade-offs made in your optimization

Test case:
```javascript
// Generate test array with some duplicates
const testArray = Array.from({ length: 10000 }, () => Math.floor(Math.random() * 1000));
console.time('findDuplicates');
const result = findDuplicates(testArray);
console.timeEnd('findDuplicates');
console.log(`Found ${result.length} duplicates`);
```
```

**Why It's Better:**
- Specifies that the issue is with performance
- Describes the observed performance issues
- Provides analysis of the current implementation
- Asks for identification of performance bottlenecks
- Requests an optimized version
- Asks for complexity analysis and comparison
- Provides a test case for benchmarking

## Advanced Debugging

### Example 5: Memory Leak Debugging

**Prompt:**
```
Fix the memory leak:

function createButtons() {
  const buttons = [];
  for (let i = 0; i < 10; i++) {
    const button = document.createElement('button');
    button.innerText = `Button ${i}`;
    button.addEventListener('click', function() {
      console.log(`Button ${i} clicked`);
    });
    document.body.appendChild(button);
    buttons.push(button);
  }
}
```

**Improved Prompt:**
```
Identify and fix the memory leak in this JavaScript function that creates buttons with event listeners:

```javascript
function createButtons() {
  const buttons = [];
  for (let i = 0; i < 10; i++) {
    const button = document.createElement('button');
    button.innerText = `Button ${i}`;
    button.addEventListener('click', function() {
      console.log(`Button ${i} clicked`);
    });
    document.body.appendChild(button);
    buttons.push(button);
  }
}
```

Context:
This function is part of a single-page application. When a user navigates to a different view, the buttons are removed from the DOM, but we've observed increasing memory usage over time as users navigate back and forth between views.

Symptoms of the memory leak:
- Increasing memory usage in the browser's task manager
- Performance degradation over time
- No memory is reclaimed when buttons are removed from the DOM

Please:
1. Identify the specific cause of the memory leak
2. Explain how closures and event listeners can create memory leaks
3. Provide a fixed version of the function that prevents the leak
4. Include proper cleanup code for when the buttons are removed
5. Explain best practices for preventing memory leaks in JavaScript
6. Suggest tools and techniques for detecting memory leaks in web applications
7. Explain how garbage collection works in JavaScript and why it fails in this case

Additional requirements:
- The fixed code should maintain the same functionality
- The solution should follow modern JavaScript best practices
- Include comments explaining the memory management considerations
```

**Why It's Better:**
- Specifies that the issue is a memory leak
- Provides context about the application
- Describes the symptoms of the memory leak
- Asks for identification of the specific cause
- Requests explanation of closures and event listeners in relation to memory leaks
- Asks for a fixed version with proper cleanup
- Requests explanation of best practices and tools for memory leak detection
- Specifies additional requirements for the solution

### Example 6: Race Condition Debugging

**Prompt:**
```
Fix this race condition:

let counter = 0;

async function incrementCounter() {
  const currentValue = counter;
  await new Promise(resolve => setTimeout(resolve, Math.random() * 10));
  counter = currentValue + 1;
}

async function runConcurrent() {
  const promises = [];
  for (let i = 0; i < 100; i++) {
    promises.push(incrementCounter());
  }
  await Promise.all(promises);
  console.log(counter);
}
```

**Improved Prompt:**
```
Debug and fix the race condition in this JavaScript code that attempts to increment a counter concurrently:

```javascript
let counter = 0;

async function incrementCounter() {
  const currentValue = counter;
  await new Promise(resolve => setTimeout(resolve, Math.random() * 10));
  counter = currentValue + 1;
}

async function runConcurrent() {
  const promises = [];
  for (let i = 0; i < 100; i++) {
    promises.push(incrementCounter());
  }
  await Promise.all(promises);
  console.log(counter);
}
```

Expected behavior:
When `runConcurrent()` is called, the counter should be incremented 100 times, resulting in a final value of 100.

Actual behavior:
The final value is unpredictable and usually much less than 100 due to a race condition.

Please:
1. Explain what a race condition is and why it occurs in this code
2. Provide a detailed step-by-step explanation of how the race condition manifests
3. Implement at least three different solutions to fix the race condition:
   - Using a mutex/lock mechanism
   - Using atomic operations
   - Using a queue to serialize operations
4. Compare the pros and cons of each solution
5. Recommend the best approach for this specific scenario
6. Explain how to test that the race condition is fixed
7. Discuss how similar race conditions can be prevented in larger applications

Context:
This code is part of a system that needs to handle concurrent operations reliably. The actual implementation will involve database operations instead of simple counter increments, but the same concurrency principles apply.
```

**Why It's Better:**
- Specifies that the issue is a race condition
- Describes the expected and actual behavior
- Asks for explanation of race conditions
- Requests multiple solutions using different approaches
- Asks for comparison of the solutions
- Requests recommendation for the best approach
- Asks for testing strategies
- Provides context about the larger system

## Specialized Debugging

### Example 7: Security Vulnerability Debugging

**Prompt:**
```
Fix the security issues:

app.get('/user/:id', (req, res) => {
  const query = `SELECT * FROM users WHERE id = ${req.params.id}`;
  db.query(query, (err, result) => {
    if (err) throw err;
    res.json(result[0]);
  });
});
```

**Improved Prompt:**
```
Identify and fix the security vulnerabilities in this Node.js/Express API endpoint:

```javascript
app.get('/user/:id', (req, res) => {
  const query = `SELECT * FROM users WHERE id = ${req.params.id}`;
  db.query(query, (err, result) => {
    if (err) throw err;
    res.json(result[0]);
  });
});
```

Security context:
This endpoint is part of a REST API for a web application that allows users to view user profiles. The endpoint is accessible to authenticated users.

Please:
1. Identify all security vulnerabilities in this code (there are multiple issues)
2. Explain each vulnerability and its potential impact:
   - How it could be exploited
   - What damage could result
   - OWASP category for each vulnerability
3. Provide a fully secured version of the endpoint
4. Explain each security measure implemented in your solution
5. Suggest additional security headers or middleware that should be used
6. Recommend proper error handling practices from a security perspective
7. Explain how to test for these vulnerabilities

Specific vulnerabilities to address:
- SQL injection
- Error handling exposing sensitive information
- Missing input validation
- Potential information disclosure
- Missing rate limiting
- Improper authentication/authorization checks

Assume the application uses:
- Express.js framework
- MySQL database with the 'mysql2' package
- JWT for authentication
```

**Why It's Better:**
- Specifies that the issue is security vulnerabilities
- Provides context about the API endpoint
- Asks for identification and explanation of each vulnerability
- Requests a fully secured version
- Asks for explanation of security measures
- Lists specific vulnerabilities to address
- Provides information about the application stack

### Example 8: Cross-Browser Compatibility Debugging

**Prompt:**
```
Fix this code to work in all browsers:

const container = document.querySelector('.container');
container.addEventListener('click', (e) => {
  if (e.target.matches('.item')) {
    const items = [...container.querySelectorAll('.item')];
    const index = items.indexOf(e.target);
    console.log(`Clicked item ${index}`);
  }
});
```

**Improved Prompt:**
```
Debug and fix the cross-browser compatibility issues in this JavaScript DOM manipulation code:

```javascript
const container = document.querySelector('.container');
container.addEventListener('click', (e) => {
  if (e.target.matches('.item')) {
    const items = [...container.querySelectorAll('.item')];
    const index = items.indexOf(e.target);
    console.log(`Clicked item ${index}`);
  }
});
```

Browser compatibility issues:
- The code works in Chrome and Firefox but fails in Internet Explorer 11
- Safari on iOS 12 reports "TypeError: undefined is not a function"
- Some older Android browsers don't execute the event handler correctly

HTML context:
```html
<div class="container">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
</div>
```

Please:
1. Identify each browser compatibility issue in the code
2. Explain which browsers are affected by each issue and why
3. Provide a fixed version that works across all major browsers including:
   - Chrome, Firefox, Safari (latest versions)
   - Edge (latest)
   - Internet Explorer 11
   - iOS Safari (version 11+)
   - Android browsers (version 5+)
4. Explain each fix and why it resolves the compatibility issue
5. Suggest how to test cross-browser compatibility
6. Recommend tools or libraries that could help prevent similar issues
7. Provide a progressive enhancement approach that gracefully degrades in older browsers

Additional requirements:
- The solution should maintain the same functionality
- Avoid using large polyfill libraries if possible
- Include comments explaining browser-specific considerations
```

**Why It's Better:**
- Specifies that the issue is cross-browser compatibility
- Lists specific browser compatibility issues
- Provides HTML context
- Asks for identification and explanation of each issue
- Requests a fixed version for specific browser versions
- Asks for explanation of each fix
- Requests testing strategies and tool recommendations
- Specifies additional requirements for the solution

## Debugging with Context

### Example 9: Framework-Specific Debugging

**Prompt:**
```
Fix this React component:

function UserProfile({ userId }) {
  const [user, setUser] = useState({});
  
  useEffect(() => {
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => setUser(data));
  });
  
  return (
    <div>
      <h1>{user.name}</h1>
      <p>Email: {user.email}</p>
    </div>
  );
}
```

**Improved Prompt:**
```
Debug and fix the issues in this React functional component that causes excessive re-rendering:

```jsx
function UserProfile({ userId }) {
  const [user, setUser] = useState({});
  
  useEffect(() => {
    fetch(`/api/users/${userId}`)
      .then(res => res.json())
      .then(data => setUser(data));
  });
  
  return (
    <div>
      <h1>{user.name}</h1>
      <p>Email: {user.email}</p>
    </div>
  );
}
```

Observed issues:
- The component makes API requests in an infinite loop
- The browser's network tab shows repeated calls to the API
- The component re-renders continuously
- Console shows React warning about state updates during rendering

Component usage:
```jsx
<UserProfile userId="123" />
```

Please:
1. Identify all issues in the component
2. Explain why each issue causes problems in React
3. Provide a fixed version of the component
4. Explain React's rendering lifecycle and how it relates to the issues
5. Add proper error handling for the API request
6. Add loading state management
7. Implement best practices for data fetching in React
8. Suggest performance optimizations

Additional requirements:
- Handle cases where userId changes
- Handle API errors gracefully
- Show a loading indicator while fetching data
- Implement proper cleanup if the component unmounts during a fetch
- Follow React best practices and hooks rules

React version: 17.0.2
```

**Why It's Better:**
- Specifies that the issue is with a React component
- Describes the observed issues
- Provides component usage example
- Asks for identification and explanation of each issue
- Requests a fixed version
- Asks for explanation of React's rendering lifecycle
- Specifies additional requirements for error handling and loading states
- Provides React version information

### Example 10: Database Query Debugging

**Prompt:**
```
Fix this SQL query:

SELECT * FROM orders 
JOIN customers ON orders.customer_id = customer.id
WHERE order_date > '2023-01-01' AND status = 'shipped'
ORDER BY order_date;
```

**Improved Prompt:**
```
Debug and fix the issues in this SQL query that's producing an error when executed against a PostgreSQL database:

```sql
SELECT * FROM orders 
JOIN customers ON orders.customer_id = customer.id
WHERE order_date > '2023-01-01' AND status = 'shipped'
ORDER BY order_date;
```

Error message received:
```
ERROR: column customer.id does not exist
LINE 2: JOIN customers ON orders.customer_id = customer.id
                                               ^
HINT: Perhaps you meant to reference the column "customers.id".
```

Database schema:
```sql
CREATE TABLE customers (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  customer_id INTEGER REFERENCES customers(id),
  order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  status VARCHAR(20) NOT NULL,
  total_amount DECIMAL(10, 2) NOT NULL
);
```

Query purpose:
Retrieve all shipped orders placed after January 1, 2023, along with the customer information, sorted by order date.

Please:
1. Identify all syntax and logical errors in the query
2. Explain why each error occurs
3. Provide a corrected version of the query
4. Explain any SQL best practices that should be applied
5. Optimize the query for performance
6. Suggest indexes that would improve query performance
7. Provide an alternative query that only selects necessary columns instead of using SELECT *

Additional considerations:
- The database may contain millions of orders and thousands of customers
- The query will be used in a report that runs daily
- Consider adding appropriate table aliases for readability
```

**Why It's Better:**
- Specifies that the issue is with an SQL query
- Provides the error message
- Includes the database schema
- Explains the purpose of the query
- Asks for identification and explanation of each error
- Requests a corrected version
- Asks for optimization suggestions
- Provides additional context about the database size and query usage

## Key Takeaways

1. **Be Specific About the Issue**: Clearly identify the type of bug or issue (syntax error, logic error, performance issue, etc.).

2. **Provide Context**: Include relevant information about the environment, expected behavior, and observed issues.

3. **Include Error Messages**: If available, provide exact error messages or symptoms.

4. **Show Test Cases**: Provide examples that demonstrate the issue.

5. **Request Explanation**: Ask for an explanation of why the issue occurs, not just a fix.

6. **Ask for Multiple Solutions**: Request different approaches to fixing the issue when appropriate.

7. **Specify Requirements**: Clearly state any requirements or constraints for the solution.

8. **Request Best Practices**: Ask for recommendations to prevent similar issues in the future.

9. **Provide Relevant Context**: Include information about frameworks, libraries, or systems being used.

10. **Format Code Properly**: Use proper code formatting for readability.

## Next Steps

In the next section, we'll explore examples of prompts for documentation tasks.

---

[Next: Documentation Examples](./04-documentation.md) | [Previous: Code Explanation Examples](./02-code-explanation.md) | [Back to Main](../README.md)
