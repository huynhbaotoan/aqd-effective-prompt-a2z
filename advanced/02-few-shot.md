# Few-Shot Learning

## What is Few-Shot Learning?

Few-Shot Learning is a prompt engineering technique where you provide Amazon Q Developer with examples of the task you want it to perform. By showing the AI a few examples of inputs and their corresponding outputs, you help it understand the pattern you want it to follow.

This technique is particularly effective for:
- Establishing specific coding styles or patterns
- Teaching custom formatting preferences
- Demonstrating domain-specific conventions
- Guiding the AI to follow particular implementation approaches

## The Science Behind Few-Shot Learning

Few-Shot Learning works because:

1. **Pattern Recognition**: AI models excel at recognizing and continuing patterns
2. **Implicit Instruction**: Examples communicate requirements that might be difficult to express in words
3. **Reduced Ambiguity**: Concrete examples clarify expectations better than abstract descriptions
4. **Context Enrichment**: Examples provide rich context about the task domain

## Basic Few-Shot Structure

A typical Few-Shot prompt follows this pattern:

```
Task: [Description of what you want Amazon Q Developer to do]

Here are some examples:

Input:
[Example input 1]

Output:
[Example output 1]

Input:
[Example input 2]

Output:
[Example output 2]

Now, please do the same for:

Input:
[Your actual input]
```

## Techniques for Effective Few-Shot Learning

### 1. Example Selection

Choose examples that are representative and diverse.

**Example:**
```
Task: Generate unit tests for JavaScript functions.

Here are some examples:

Input:
```javascript
function add(a, b) {
  return a + b;
}
```

Output:
```javascript
describe('add', () => {
  test('adds two positive numbers correctly', () => {
    expect(add(2, 3)).toBe(5);
  });
  
  test('adds a positive and negative number correctly', () => {
    expect(add(5, -3)).toBe(2);
  });
  
  test('adds two negative numbers correctly', () => {
    expect(add(-2, -3)).toBe(-5);
  });
});
```

Input:
```javascript
function isEven(num) {
  return num % 2 === 0;
}
```

Output:
```javascript
describe('isEven', () => {
  test('returns true for even numbers', () => {
    expect(isEven(2)).toBe(true);
    expect(isEven(100)).toBe(true);
  });
  
  test('returns false for odd numbers', () => {
    expect(isEven(1)).toBe(false);
    expect(isEven(99)).toBe(false);
  });
  
  test('handles zero correctly', () => {
    expect(isEven(0)).toBe(true);
  });
});
```

Now, please generate unit tests for:

Input:
```javascript
function capitalize(str) {
  if (!str) return '';
  return str.charAt(0).toUpperCase() + str.slice(1).toLowerCase();
}
```
```

### 2. Progressive Complexity

Arrange examples from simple to complex.

**Example:**
```
Task: Write SQL queries to extract data from a customer database.

Here are some examples:

Input:
Get all customer names.

Output:
```sql
SELECT first_name, last_name FROM customers;
```

Input:
Get all customers from New York.

Output:
```sql
SELECT * FROM customers
WHERE state = 'NY';
```

Input:
Get the total order value for each customer in 2023.

Output:
```sql
SELECT c.customer_id, c.first_name, c.last_name, SUM(o.total_amount) as total_spent
FROM customers c
JOIN orders o ON c.customer_id = o.customer_id
WHERE EXTRACT(YEAR FROM o.order_date) = 2023
GROUP BY c.customer_id, c.first_name, c.last_name
ORDER BY total_spent DESC;
```

Now, please write a SQL query for:

Input:
Find customers who have placed more than 5 orders and spent over $1000 in total, showing their contact information and total spend.
```

### 3. Annotated Examples

Add explanations to your examples to highlight important patterns.

**Example:**
```
Task: Write React components following our project's conventions.

Here are some examples:

Input:
Create a Button component that accepts text and onClick props.

Output:
```jsx
// Button.jsx
// Note: We use named exports and functional components
import React from 'react';
import PropTypes from 'prop-types';
import './Button.css'; // CSS files match component name

// Props are destructured in the parameter list
export const Button = ({ text, onClick }) => {
  // Event handlers use handle prefix
  const handleClick = (e) => {
    // We prevent default and call the passed handler
    e.preventDefault();
    onClick(e);
  };
  
  // We use className for CSS classes
  return (
    <button className="button" onClick={handleClick}>
      {text}
    </button>
  );
};

// PropTypes are always defined
Button.propTypes = {
  text: PropTypes.string.isRequired,
  onClick: PropTypes.func.isRequired,
};
```

Input:
Create a UserCard component that displays a user's name and email.

Output:
```jsx
// UserCard.jsx
// Following same conventions as before
import React from 'react';
import PropTypes from 'prop-types';
import './UserCard.css';

// User shape is defined as a separate PropType
const userShape = PropTypes.shape({
  name: PropTypes.string.isRequired,
  email: PropTypes.string.isRequired,
});

export const UserCard = ({ user }) => {
  return (
    <div className="user-card">
      <h3 className="user-card__name">{user.name}</h3>
      <p className="user-card__email">{user.email}</p>
    </div>
  );
};

UserCard.propTypes = {
  user: userShape.isRequired,
};
```

Now, please create:

Input:
Create a ProductList component that receives an array of products and renders them in a list, with each product showing name, price, and an "Add to Cart" button.
```

### 4. Contrasting Examples

Show both good and bad examples to clarify expectations.

**Example:**
```
Task: Write error handling for AWS Lambda functions following our best practices.

Here are examples:

Input:
Handle errors in a Lambda function that processes S3 events.

Good Output:
```javascript
exports.handler = async (event) => {
  try {
    // Validate input
    if (!event.Records || !Array.isArray(event.Records)) {
      console.error('Invalid event structure', { event });
      return { statusCode: 400, body: 'Invalid event structure' };
    }
    
    // Process records
    const results = await Promise.all(event.Records.map(async (record) => {
      try {
        // Process individual record
        return await processRecord(record);
      } catch (recordError) {
        // Log and continue with other records
        console.error('Error processing record', { 
          error: recordError.message,
          record,
          stackTrace: recordError.stack
        });
        return { error: recordError.message, recordId: record.s3.object.key };
      }
    }));
    
    return { statusCode: 200, body: JSON.stringify({ results }) };
  } catch (error) {
    // Structured error logging
    console.error('Lambda execution failed', { 
      error: error.message,
      stackTrace: error.stack,
      event
    });
    
    // Return appropriate error response
    return {
      statusCode: 500,
      body: JSON.stringify({ message: 'Internal server error' })
    };
  }
};
```

Bad Output (Don't do this):
```javascript
exports.handler = async (event) => {
  // No input validation
  
  // No try/catch blocks
  const results = event.Records.map((record) => {
    // Will throw if record structure is unexpected
    return processRecord(record);
  });
  
  // Simple console.log without structured data
  console.log('Processed records');
  
  // No error handling
  return { statusCode: 200, body: 'Success' };
};
```

Now, please write:

Input:
Handle errors in a Lambda function that processes DynamoDB stream events and sends notifications via SNS.
```

### 5. Template Completion

Provide partial examples that Amazon Q Developer needs to complete.

**Example:**
```
Task: Write Jest tests for React components.

Here's how we structure our tests:

```jsx
// Component to test
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
import { Counter } from './Counter';

describe('Counter', () => {
  test('renders with initial count of 0', () => {
    render(<Counter />);
    expect(screen.getByText(/count: 0/i)).toBeInTheDocument();
  });

  test('increments count when increment button is clicked', () => {
    render(<Counter />);
    const incrementButton = screen.getByRole('button', { name: /increment/i });
    fireEvent.click(incrementButton);
    expect(screen.getByText(/count: 1/i)).toBeInTheDocument();
  });

  // Additional tests...
});
```

Now, please write tests for this component:

```jsx
// TodoItem.jsx
import React from 'react';

export const TodoItem = ({ todo, onToggle, onDelete }) => {
  return (
    <div className="todo-item">
      <input 
        type="checkbox" 
        checked={todo.completed} 
        onChange={() => onToggle(todo.id)} 
      />
      <span style={{ textDecoration: todo.completed ? 'line-through' : 'none' }}>
        {todo.text}
      </span>
      <button onClick={() => onDelete(todo.id)}>Delete</button>
    </div>
  );
};
```

Start with:

```jsx
import React from 'react';
import { render, screen, fireEvent } from '@testing-library/react';
import { TodoItem } from './TodoItem';

describe('TodoItem', () => {
  // Write tests here
});
```
```

## Advanced Few-Shot Patterns

### 1. Multi-Step Examples

Show examples that involve multiple steps or transformations.

**Example:**
```
Task: Refactor legacy JavaScript code to modern ES6+.

Here's an example of our refactoring process:

Original Code:
```javascript
var UserService = function(apiClient) {
  this.apiClient = apiClient;
  this.users = [];
};

UserService.prototype.fetchUsers = function(callback) {
  var self = this;
  this.apiClient.get('/users', function(err, data) {
    if (err) {
      return callback(err);
    }
    self.users = data;
    callback(null, data);
  });
};

UserService.prototype.getUserById = function(id) {
  for (var i = 0; i < this.users.length; i++) {
    if (this.users[i].id === id) {
      return this.users[i];
    }
  }
  return null;
};
```

Step 1: Convert to ES6 class
```javascript
var UserService = class {
  constructor(apiClient) {
    this.apiClient = apiClient;
    this.users = [];
  }
  
  fetchUsers(callback) {
    var self = this;
    this.apiClient.get('/users', function(err, data) {
      if (err) {
        return callback(err);
      }
      self.users = data;
      callback(null, data);
    });
  }
  
  getUserById(id) {
    for (var i = 0; i < this.users.length; i++) {
      if (this.users[i].id === id) {
        return this.users[i];
      }
    }
    return null;
  }
};
```

Step 2: Use arrow functions, const/let, and modern array methods
```javascript
class UserService {
  constructor(apiClient) {
    this.apiClient = apiClient;
    this.users = [];
  }
  
  fetchUsers(callback) {
    this.apiClient.get('/users', (err, data) => {
      if (err) {
        return callback(err);
      }
      this.users = data;
      callback(null, data);
    });
  }
  
  getUserById(id) {
    return this.users.find(user => user.id === id) || null;
  }
}
```

Step 3: Convert to Promises/async-await
```javascript
class UserService {
  constructor(apiClient) {
    this.apiClient = apiClient;
    this.users = [];
  }
  
  async fetchUsers() {
    try {
      const data = await this.apiClient.get('/users');
      this.users = data;
      return data;
    } catch (error) {
      throw error;
    }
  }
  
  getUserById(id) {
    return this.users.find(user => user.id === id) || null;
  }
}
```

Now, please refactor this legacy code following the same steps:

```javascript
var ProductService = function(apiClient) {
  this.apiClient = apiClient;
  this.products = [];
};

ProductService.prototype.fetchProducts = function(category, callback) {
  var self = this;
  this.apiClient.get('/products?category=' + category, function(err, data) {
    if (err) {
      return callback(err);
    }
    self.products = data;
    callback(null, data);
  });
};

ProductService.prototype.getProductsByPrice = function(minPrice, maxPrice) {
  var results = [];
  for (var i = 0; i < this.products.length; i++) {
    var product = this.products[i];
    if (product.price >= minPrice && product.price <= maxPrice) {
      results.push(product);
    }
  }
  return results;
};
```
```

### 2. Comparative Examples

Show examples that highlight differences between similar but distinct tasks.

**Example:**
```
Task: Write different types of AWS Lambda handlers.

Example 1: API Gateway Lambda Handler
```javascript
// This handler processes HTTP requests from API Gateway
exports.handler = async (event) => {
  try {
    // Extract data from the HTTP request
    const body = JSON.parse(event.body || '{}');
    const pathParameters = event.pathParameters || {};
    const queryStringParameters = event.queryStringParameters || {};
    
    // Process the request
    const result = await processRequest(body, pathParameters, queryStringParameters);
    
    // Return HTTP response
    return {
      statusCode: 200,
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(result)
    };
  } catch (error) {
    return {
      statusCode: 500,
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({ error: error.message })
    };
  }
};
```

Example 2: S3 Event Lambda Handler
```javascript
// This handler processes S3 bucket events
exports.handler = async (event) => {
  try {
    // Process each record (file) from the S3 event
    const results = await Promise.all(event.Records.map(async (record) => {
      // Extract S3 details
      const bucket = record.s3.bucket.name;
      const key = decodeURIComponent(record.s3.object.key.replace(/\+/g, ' '));
      
      // Process the file
      return await processS3File(bucket, key);
    }));
    
    return { status: 'success', results };
  } catch (error) {
    console.error('Error processing S3 event', error);
    throw error; // Let AWS handle the error
  }
};
```

Now, please write:

Input:
Write a Lambda handler for processing DynamoDB stream events.
```

### 3. Parameterized Examples

Show examples with varying parameters to demonstrate flexibility.

**Example:**
```
Task: Generate TypeScript interfaces from JSON data with different complexity levels.

Example 1: Simple flat object
Input JSON:
```json
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "active": true
}
```

Output TypeScript:
```typescript
interface User {
  id: number;
  name: string;
  email: string;
  active: boolean;
}
```

Example 2: Nested object
Input JSON:
```json
{
  "id": 1,
  "name": "John Doe",
  "contact": {
    "email": "john@example.com",
    "phone": "555-1234"
  },
  "roles": ["admin", "user"]
}
```

Output TypeScript:
```typescript
interface User {
  id: number;
  name: string;
  contact: Contact;
  roles: string[];
}

interface Contact {
  email: string;
  phone: string;
}
```

Example 3: Array of objects
Input JSON:
```json
[
  {
    "id": 1,
    "productName": "Laptop",
    "price": 999.99,
    "specs": {
      "cpu": "Intel i7",
      "ram": "16GB"
    }
  },
  {
    "id": 2,
    "productName": "Phone",
    "price": 699.99,
    "specs": {
      "cpu": "A15",
      "ram": "8GB"
    }
  }
]
```

Output TypeScript:
```typescript
interface Product {
  id: number;
  productName: string;
  price: number;
  specs: ProductSpecs;
}

interface ProductSpecs {
  cpu: string;
  ram: string;
}

type Products = Product[];
```

Now, please generate TypeScript interfaces for:

Input JSON:
```json
{
  "orderId": "ORD-12345",
  "customer": {
    "id": 42,
    "name": "Jane Smith",
    "addresses": [
      {
        "type": "billing",
        "street": "123 Main St",
        "city": "Anytown",
        "zipCode": "12345"
      },
      {
        "type": "shipping",
        "street": "456 Oak Ave",
        "city": "Somewhere",
        "zipCode": "67890"
      }
    ]
  },
  "items": [
    {
      "productId": "P-100",
      "name": "Widget",
      "quantity": 2,
      "unitPrice": 19.99
    },
    {
      "productId": "P-200",
      "name": "Gadget",
      "quantity": 1,
      "unitPrice": 29.99
    }
  ],
  "totalAmount": 69.97,
  "status": "shipped"
}
```
```

## When to Use Few-Shot Learning

Few-Shot Learning is most effective for:

- **Style Guidance**: When you want code to follow specific stylistic conventions
- **Domain-Specific Tasks**: When working with specialized formats or patterns
- **Complex Transformations**: When the desired transformation is easier to show than explain
- **Consistency**: When you need multiple outputs to follow the same pattern

It may be less necessary for:

- Standard, well-known programming tasks
- Simple requests with clear, unambiguous requirements
- Tasks where you don't have strong preferences about implementation details

## Key Takeaways

- Few-Shot Learning uses examples to guide Amazon Q Developer's responses
- Effective examples should be representative, diverse, and clearly formatted
- Advanced techniques include progressive complexity, annotated examples, and contrasting examples
- Multi-step examples can demonstrate complex transformations
- Parameterized examples show how to handle varying inputs

## Next Steps

In the next section, we'll explore Iterative Refinement, a technique for progressively improving Amazon Q Developer's outputs.

---

[Next: Iterative Refinement](./03-iterative-refinement.md) | [Previous: Chain of Thought Prompting](./01-chain-of-thought.md) | [Back to Main](../README.md)
