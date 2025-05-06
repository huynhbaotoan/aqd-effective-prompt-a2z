# Documentation Examples

This section provides practical examples of effective prompts for generating documentation with Amazon Q Developer. Each example demonstrates key prompt engineering techniques and best practices for creating clear, comprehensive documentation.

## Basic Documentation

### Example 1: Function Documentation

**Prompt:**
```
Document this function:

function calculateDiscount(price, discountPercent) {
  if (discountPercent < 0 || discountPercent > 100) {
    throw new Error('Discount percentage must be between 0 and 100');
  }
  return price - (price * discountPercent / 100);
}
```

**Improved Prompt:**
```
Create comprehensive JSDoc documentation for this JavaScript function that calculates a discounted price:

```javascript
function calculateDiscount(price, discountPercent) {
  if (discountPercent < 0 || discountPercent > 100) {
    throw new Error('Discount percentage must be between 0 and 100');
  }
  return price - (price * discountPercent / 100);
}
```

Please include:
1. A clear description of the function's purpose
2. Parameter descriptions with types and constraints
3. Return value description with type
4. Thrown exceptions/errors
5. Example usage with inputs and outputs
6. Edge cases handling (e.g., zero price, zero discount)
7. Any performance considerations

Follow the Google JavaScript Style Guide for JSDoc formatting.
```

**Why It's Better:**
- Specifies the documentation format (JSDoc)
- Requests specific components of the documentation
- Asks for example usage
- Mentions edge cases to document
- Specifies a style guide to follow

### Example 2: Class Documentation

**Prompt:**
```
Document this class:

class ShoppingCart {
  constructor() {
    this.items = [];
  }
  
  addItem(product, quantity = 1) {
    this.items.push({ product, quantity });
  }
  
  removeItem(productId) {
    this.items = this.items.filter(item => item.product.id !== productId);
  }
  
  updateQuantity(productId, quantity) {
    const item = this.items.find(item => item.product.id === productId);
    if (item) {
      item.quantity = quantity;
    }
  }
  
  getTotal() {
    return this.items.reduce((total, item) => {
      return total + (item.product.price * item.quantity);
    }, 0);
  }
  
  clear() {
    this.items = [];
  }
}
```

**Improved Prompt:**
```
Create comprehensive documentation for this JavaScript ShoppingCart class following JSDoc standards:

```javascript
class ShoppingCart {
  constructor() {
    this.items = [];
  }
  
  addItem(product, quantity = 1) {
    this.items.push({ product, quantity });
  }
  
  removeItem(productId) {
    this.items = this.items.filter(item => item.product.id !== productId);
  }
  
  updateQuantity(productId, quantity) {
    const item = this.items.find(item => item.product.id === productId);
    if (item) {
      item.quantity = quantity;
    }
  }
  
  getTotal() {
    return this.items.reduce((total, item) => {
      return total + (item.product.price * item.quantity);
    }, 0);
  }
  
  clear() {
    this.items = [];
  }
}
```

Please include:
1. Class description explaining its purpose and usage
2. Constructor documentation
3. Documentation for each method including:
   - Description
   - Parameters with types and descriptions
   - Return values with types
   - Exceptions thrown (if any)
4. Property documentation for the items array
5. Example usage showing a complete workflow:
   - Creating a cart
   - Adding items
   - Updating quantities
   - Removing items
   - Getting the total
   - Clearing the cart
6. Any assumptions about the product object structure
7. Notes on potential edge cases or limitations

Assume this class is part of an e-commerce application and will be used by other developers on your team.
```

**Why It's Better:**
- Specifies the documentation format (JSDoc)
- Requests documentation for the class, constructor, methods, and properties
- Asks for example usage showing a complete workflow
- Requests notes on assumptions, edge cases, and limitations
- Provides context about the application and audience

## Intermediate Documentation

### Example 3: API Endpoint Documentation

**Prompt:**
```
Document this API endpoint:

app.post('/api/orders', authenticateUser, async (req, res) => {
  try {
    const { items, shippingAddress, paymentMethod } = req.body;
    
    if (!items || !items.length) {
      return res.status(400).json({ error: 'No items in order' });
    }
    
    if (!shippingAddress) {
      return res.status(400).json({ error: 'Shipping address is required' });
    }
    
    if (!paymentMethod) {
      return res.status(400).json({ error: 'Payment method is required' });
    }
    
    const order = await Order.create({
      userId: req.user.id,
      items,
      shippingAddress,
      paymentMethod,
      status: 'pending'
    });
    
    res.status(201).json({ 
      orderId: order.id,
      status: order.status,
      createdAt: order.createdAt
    });
  } catch (error) {
    console.error('Order creation error:', error);
    res.status(500).json({ error: 'Failed to create order' });
  }
});
```

**Improved Prompt:**
```
Create comprehensive API documentation for this Express.js endpoint that creates a new order:

```javascript
app.post('/api/orders', authenticateUser, async (req, res) => {
  try {
    const { items, shippingAddress, paymentMethod } = req.body;
    
    if (!items || !items.length) {
      return res.status(400).json({ error: 'No items in order' });
    }
    
    if (!shippingAddress) {
      return res.status(400).json({ error: 'Shipping address is required' });
    }
    
    if (!paymentMethod) {
      return res.status(400).json({ error: 'Payment method is required' });
    }
    
    const order = await Order.create({
      userId: req.user.id,
      items,
      shippingAddress,
      paymentMethod,
      status: 'pending'
    });
    
    res.status(201).json({ 
      orderId: order.id,
      status: order.status,
      createdAt: order.createdAt
    });
  } catch (error) {
    console.error('Order creation error:', error);
    res.status(500).json({ error: 'Failed to create order' });
  }
});
```

Please create documentation in OpenAPI/Swagger format that includes:

1. Endpoint overview:
   - Description
   - URL path
   - HTTP method
   - Authentication requirements

2. Request details:
   - Headers required
   - Request body schema with all fields, types, and constraints
   - Example request body

3. Response details:
   - Success response code and schema
   - Example success response
   - All possible error responses with codes and messages
   - Example error responses

4. Security considerations:
   - Authentication requirements
   - Authorization details
   - Rate limiting information

5. Additional information:
   - Any side effects (e.g., emails sent, inventory updated)
   - Related endpoints
   - Idempotency considerations

Assume this API is part of an e-commerce platform's order management system and will be used by frontend developers and third-party integrators.
```

**Why It's Better:**
- Specifies the documentation format (OpenAPI/Swagger)
- Requests specific components of the API documentation
- Asks for example requests and responses
- Includes security considerations
- Provides context about the API's purpose and audience

### Example 4: Configuration File Documentation

**Prompt:**
```
Document this configuration file:

{
  "server": {
    "port": 3000,
    "host": "localhost",
    "timeout": 30000
  },
  "database": {
    "host": "db.example.com",
    "port": 5432,
    "username": "app_user",
    "password": "${DB_PASSWORD}",
    "database": "myapp",
    "pool": {
      "min": 5,
      "max": 20
    }
  },
  "logging": {
    "level": "info",
    "format": "json",
    "output": ["console", "file"],
    "file": {
      "path": "/var/log/myapp.log",
      "maxSize": "10m",
      "maxFiles": 5
    }
  },
  "cache": {
    "enabled": true,
    "ttl": 3600,
    "type": "redis",
    "redis": {
      "host": "redis.example.com",
      "port": 6379
    }
  }
}
```

**Improved Prompt:**
```
Create comprehensive documentation for this JSON configuration file used in a Node.js application:

```json
{
  "server": {
    "port": 3000,
    "host": "localhost",
    "timeout": 30000
  },
  "database": {
    "host": "db.example.com",
    "port": 5432,
    "username": "app_user",
    "password": "${DB_PASSWORD}",
    "database": "myapp",
    "pool": {
      "min": 5,
      "max": 20
    }
  },
  "logging": {
    "level": "info",
    "format": "json",
    "output": ["console", "file"],
    "file": {
      "path": "/var/log/myapp.log",
      "maxSize": "10m",
      "maxFiles": 5
    }
  },
  "cache": {
    "enabled": true,
    "ttl": 3600,
    "type": "redis",
    "redis": {
      "host": "redis.example.com",
      "port": 6379
    }
  }
}
```

Please create documentation that includes:

1. Overview of the configuration file's purpose and usage
2. Detailed explanation of each section:
   - Server configuration
   - Database configuration
   - Logging configuration
   - Cache configuration

3. For each configuration option, include:
   - Description of the option's purpose
   - Data type and format
   - Default value (if any)
   - Required vs. optional status
   - Valid values or constraints
   - Environment variable substitution (like ${DB_PASSWORD})

4. Examples of common configuration changes for different environments:
   - Development
   - Testing
   - Production

5. Best practices for:
   - Securing sensitive configuration values
   - Configuration file management
   - Environment-specific configurations

6. Troubleshooting common configuration issues

Format the documentation in Markdown suitable for inclusion in a project's README or documentation site.
```

**Why It's Better:**
- Requests documentation for each section and option
- Asks for information about data types, defaults, and constraints
- Requests examples for different environments
- Includes best practices and troubleshooting
- Specifies the output format (Markdown)

## Advanced Documentation

### Example 5: Architecture Documentation

**Prompt:**
```
Document the architecture of a microservices e-commerce system.
```

**Improved Prompt:**
```
Create comprehensive architecture documentation for a microservices-based e-commerce system with the following components:

1. User Service: Handles authentication, authorization, and user profile management
2. Product Catalog Service: Manages product information, categories, and search
3. Inventory Service: Tracks product availability and manages stock levels
4. Order Service: Processes customer orders and manages order lifecycle
5. Payment Service: Handles payment processing and integrates with payment gateways
6. Notification Service: Sends emails, SMS, and push notifications
7. Analytics Service: Collects and processes business metrics and user behavior

For this architecture documentation, please include:

1. System Overview:
   - High-level architecture diagram (describe it textually)
   - Key design principles and patterns used
   - Technology stack for each service

2. For each microservice:
   - Purpose and responsibilities
   - Key APIs and endpoints
   - Data model overview
   - Dependencies on other services
   - Scaling considerations

3. Cross-cutting concerns:
   - Service discovery and registration
   - API gateway configuration
   - Authentication and authorization flow
   - Data consistency strategy
   - Logging and monitoring approach
   - Error handling and resilience patterns

4. Communication patterns:
   - Synchronous communication (REST, gRPC)
   - Asynchronous communication (message queues, event streaming)
   - Event-driven architecture components

5. Deployment and DevOps:
   - Containerization strategy
   - Kubernetes resource organization
   - CI/CD pipeline overview
   - Environment strategy

6. Security considerations:
   - Authentication mechanisms
   - Authorization approach
   - Data protection measures
   - API security

Format the documentation in Markdown suitable for a technical audience of software engineers and architects who will be implementing and maintaining this system.
```

**Why It's Better:**
- Specifies the components of the microservices system
- Requests specific sections for the architecture documentation
- Asks for details about each microservice
- Includes cross-cutting concerns and communication patterns
- Specifies the audience and format

### Example 6: SDK Documentation

**Prompt:**
```
Document a payment processing SDK.
```

**Improved Prompt:**
```
Create comprehensive SDK documentation for a payment processing library called "PaymentPro SDK" with the following features:

1. Payment processing (credit cards, ACH, digital wallets)
2. Customer management
3. Subscription billing
4. Payment method tokenization
5. Refund processing
6. Webhook event handling

The SDK is available for multiple platforms:
- JavaScript (Node.js and browser)
- Python
- Java
- Ruby

Please create documentation that includes:

1. Getting Started guide:
   - Installation instructions for each platform
   - Authentication and API key setup
   - Basic configuration
   - Simple payment processing example

2. Core Concepts:
   - Key terminology and entities (transactions, customers, payment methods, etc.)
   - SDK architecture and design principles
   - Security features and best practices
   - Error handling approach

3. API Reference (focus on the JavaScript version):
   - Payment methods
     - `createPayment(options)`: Process a payment
     - `getPayment(paymentId)`: Retrieve payment details
     - `refundPayment(paymentId, options)`: Process a refund
   - Customer methods
     - `createCustomer(customerData)`: Create a customer
     - `updateCustomer(customerId, data)`: Update customer information
     - `deleteCustomer(customerId)`: Delete a customer
   - Subscription methods
     - `createSubscription(customerId, planId, options)`: Create a subscription
     - `updateSubscription(subscriptionId, options)`: Update a subscription
     - `cancelSubscription(subscriptionId, options)`: Cancel a subscription

4. For each method, include:
   - Description
   - Parameters with types and descriptions
   - Return values
   - Error codes and handling
   - Example code in JavaScript
   - Edge cases and limitations

5. Advanced Topics:
   - Handling webhooks
   - Testing and sandbox environment
   - Compliance and security (PCI DSS)
   - Handling international payments
   - Implementing recurring billing

6. Migration Guide:
   - Upgrading from previous versions
   - Breaking changes
   - Deprecated features

Format the documentation in Markdown suitable for publishing on a developer portal.
```

**Why It's Better:**
- Specifies the SDK name and features
- Lists the supported platforms
- Requests specific sections for the documentation
- Includes method signatures and parameters
- Asks for example code
- Specifies the output format and intended publication

## Specialized Documentation

### Example 7: User Guide Documentation

**Prompt:**
```
Create a user guide for a mobile app.
```

**Improved Prompt:**
```
Create a comprehensive user guide for "FitTrack Pro," a fitness tracking mobile app with the following features:

1. Workout tracking (strength training, cardio, flexibility)
2. Nutrition logging and meal planning
3. Progress tracking with charts and statistics
4. Social features for connecting with friends
5. Integration with fitness wearables
6. Goal setting and achievement tracking

The user guide should be written for end users with varying levels of technical expertise and should include:

1. Introduction:
   - App overview and value proposition
   - Supported devices and requirements
   - How to download and install

2. Getting Started:
   - Account creation and setup
   - Profile configuration
   - Connecting devices and services
   - Navigation overview (main screens and menus)
   - Key settings and preferences

3. Feature Walkthroughs (for each major feature):
   - Step-by-step instructions with clear action items
   - Screenshots descriptions (indicate where screenshots would be placed)
   - Tips and best practices
   - Common issues and solutions

4. Advanced Features:
   - Custom workout creation
   - Nutrition plan customization
   - Advanced analytics
   - Social sharing options
   - Exporting data

5. Troubleshooting:
   - Common issues and their solutions
   - FAQ section
   - Contact support information

6. Privacy and Data:
   - What data is collected
   - How to manage privacy settings
   - How to export or delete your data

Format the user guide in Markdown with clear headings, bullet points, numbered lists for sequential instructions, and callouts for important notes or warnings. The tone should be friendly, encouraging, and accessible to non-technical users.
```

**Why It's Better:**
- Specifies the app name and features
- Defines the target audience
- Requests specific sections for the user guide
- Includes step-by-step instructions and screenshots
- Specifies the tone and formatting

### Example 8: API Migration Guide

**Prompt:**
```
Create a migration guide for an API update.
```

**Improved Prompt:**
```
Create a comprehensive API migration guide for developers transitioning from v1 to v2 of the "CloudStore API," a cloud storage service API. The v2 API includes breaking changes, new features, and performance improvements.

Key changes in v2:
1. Authentication: Moving from API keys to OAuth 2.0
2. Endpoints: Base URL change from api.cloudstore.com/v1/* to api.cloudstore.com/v2/*
3. Response format: Standardized error responses and pagination
4. Rate limiting: New tiered rate limits based on account type
5. New features: Batch operations, webhooks, and advanced search
6. Deprecated features: Legacy file conversion endpoints

Please create a migration guide that includes:

1. Overview:
   - Migration timeline and deadlines
   - Summary of key changes
   - Benefits of upgrading

2. Breaking Changes:
   - Detailed explanation of each breaking change
   - Side-by-side comparison of v1 vs v2 (request/response examples)
   - Required code changes

3. Authentication Changes:
   - Step-by-step guide to migrate from API keys to OAuth 2.0
   - Setting up OAuth clients
   - Handling tokens and refresh flows
   - Security best practices

4. Endpoint Migration:
   - Complete mapping of v1 endpoints to v2 equivalents
   - Changed parameters and response structures
   - Handling pagination changes

5. New Features:
   - How to implement and benefit from new features
   - Best practices for batch operations
   - Setting up and handling webhooks

6. Migration Strategies:
   - Phased migration approach
   - Testing recommendations
   - Handling both versions during transition
   - Monitoring and troubleshooting

7. Code Examples:
   - Migration examples in multiple languages (JavaScript, Python, Java)
   - Before/after code samples for common operations

8. Frequently Asked Questions:
   - Common migration issues and solutions
   - Performance considerations
   - Backward compatibility details

Format the guide in Markdown suitable for technical developers who are familiar with the v1 API and need to update their integrations.
```

**Why It's Better:**
- Specifies the API name and version
- Lists key changes in the new version
- Requests specific sections for the migration guide
- Includes before/after code examples
- Asks for migration strategies and FAQ
- Specifies the audience and format

## Documentation with Specific Focus

### Example 9: Security Documentation

**Prompt:**
```
Document security best practices for a web application.
```

**Improved Prompt:**
```
Create comprehensive security documentation for a web application built with the following stack:
- Frontend: React with Redux
- Backend: Node.js with Express
- Database: MongoDB
- Authentication: JWT-based authentication
- Hosting: AWS (EC2, S3, CloudFront)

The documentation should serve as a security guide for the development team and include:

1. Authentication and Authorization:
   - Secure JWT implementation best practices
   - Token storage, renewal, and invalidation
   - Role-based access control implementation
   - Multi-factor authentication recommendations
   - Session management security

2. Data Protection:
   - Input validation and sanitization strategies
   - Protection against common injection attacks (SQL, NoSQL, XSS)
   - Sensitive data handling (PII, payment information)
   - Data encryption (in transit and at rest)
   - Database security configuration

3. API Security:
   - Secure API design principles
   - Rate limiting and throttling implementation
   - CORS configuration best practices
   - API authentication and authorization
   - Error handling and information leakage prevention

4. Frontend Security:
   - Secure state management
   - Protection against XSS attacks
   - Content Security Policy implementation
   - Secure use of third-party libraries
   - Client-side validation best practices

5. Infrastructure Security:
   - AWS security best practices
   - Network security configuration
   - HTTPS implementation and certificate management
   - Security monitoring and logging
   - Backup and disaster recovery from a security perspective

6. Development Practices:
   - Secure coding guidelines
   - Dependency management and vulnerability scanning
   - Security code review process
   - Security testing (SAST, DAST, penetration testing)
   - CI/CD pipeline security

7. Compliance Considerations:
   - GDPR requirements
   - OWASP Top 10 mitigations
   - PCI DSS considerations (if handling payments)
   - Security documentation and policy requirements

For each section, include:
- Specific code examples where applicable
- Configuration snippets
- Tools and libraries recommendations
- Common vulnerabilities and their mitigations
- Verification and testing procedures

Format the documentation in Markdown suitable for inclusion in a team wiki or developer documentation portal.
```

**Why It's Better:**
- Specifies the technology stack
- Requests specific sections focused on security
- Asks for code examples and configuration snippets
- Includes compliance considerations
- Specifies the audience and format

### Example 10: Performance Documentation

**Prompt:**
```
Document performance optimization techniques.
```

**Improved Prompt:**
```
Create comprehensive performance optimization documentation for a high-traffic e-commerce web application with the following stack:
- Frontend: React with Next.js
- Backend: Node.js microservices
- Database: PostgreSQL and Redis
- Cloud Infrastructure: AWS (ECS, RDS, ElastiCache, CloudFront)

The application serves millions of users monthly with peak traffic during sales events. The documentation should cover performance optimization across all layers of the application and include:

1. Frontend Performance:
   - JavaScript and React optimization techniques
   - Bundle size optimization strategies
   - Lazy loading and code splitting
   - Image and asset optimization
   - Caching strategies (browser cache, service workers)
   - Performance metrics and monitoring (Core Web Vitals)

2. API and Backend Performance:
   - Node.js performance tuning
   - Microservice optimization
   - API design for performance
   - Caching strategies (Redis, in-memory)
   - Database query optimization
   - Connection pooling and resource management

3. Database Performance:
   - PostgreSQL query optimization
   - Indexing strategies
   - Database scaling approaches
   - Read replicas and connection pooling
   - Data partitioning and sharding
   - Query monitoring and profiling

4. Infrastructure and Scaling:
   - Auto-scaling configuration
   - Load balancing optimization
   - CDN configuration and edge caching
   - Container optimization
   - Resource allocation best practices
   - Cost-effective scaling strategies

5. Monitoring and Analysis:
   - Performance monitoring tools and setup
   - Key metrics to track
   - Alerting thresholds and strategies
   - Performance testing methodologies
   - Analyzing performance bottlenecks
   - Continuous performance monitoring

6. High-Traffic Event Preparation:
   - Capacity planning
   - Load testing strategies
   - Traffic management techniques
   - Graceful degradation approaches
   - DDoS protection measures
   - War room procedures

For each optimization technique, include:
- Description and benefits
- Implementation guidelines with code examples where applicable
- Expected performance impact
- Trade-offs and considerations
- Tools and libraries recommendations
- Verification and measurement approaches

Format the documentation in Markdown with clear sections, code examples, and diagrams (described textually) to illustrate complex concepts.
```

**Why It's Better:**
- Specifies the application type and technology stack
- Provides context about traffic and usage patterns
- Requests specific sections focused on performance
- Asks for implementation guidelines and code examples
- Includes monitoring and high-traffic event preparation
- Specifies the format and visual elements

## Key Takeaways

1. **Be Specific About Documentation Type**: Clearly state what kind of documentation you need (API reference, user guide, architecture documentation, etc.).

2. **Specify Format and Style**: Indicate the desired documentation format (Markdown, JSDoc, OpenAPI, etc.) and any style guides to follow.

3. **Request Specific Sections**: Break down the documentation into specific sections or components.

4. **Ask for Examples**: Request examples, sample code, or use cases to illustrate concepts.

5. **Provide Context**: Include information about the audience, purpose, and where the documentation will be used.

6. **Include Edge Cases and Limitations**: Ask for documentation of edge cases, limitations, and potential issues.

7. **Request Visual Elements**: When appropriate, ask for diagrams, flowcharts, or other visual aids (described textually).

8. **Specify Tone and Language**: Indicate the desired tone and language level based on the target audience.

9. **Include Best Practices**: Request sections on best practices, common pitfalls, and troubleshooting.

10. **Format Code Properly**: Use proper code formatting for any code that needs to be documented.

## Next Steps

In the next section, we'll explore practical exercises for applying prompt engineering techniques.

---

[Next: Beginner Exercises](../exercises/01-beginner.md) | [Previous: Debugging Examples](./03-debugging.md) | [Back to Main](../README.md)
