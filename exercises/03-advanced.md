# Advanced Exercises

This section provides challenging exercises for experienced prompt engineers who want to master advanced techniques with Amazon Q Developer. These exercises focus on complex scenarios and sophisticated prompt engineering strategies.

## Exercise 1: Multi-Stage System Design

**Objective:** Practice guiding Amazon Q Developer through a complex system design process with multiple interdependent components.

**Instructions:**
1. Choose a complex system to design (e.g., a distributed database, a real-time analytics platform).
2. Create a series of connected prompts that guide the design process through multiple stages:
   - System requirements and constraints
   - Architecture overview
   - Component design
   - Data flow and interactions
   - Scaling and performance considerations
   - Security and reliability

**Example Task:** Designing a distributed event processing system

**Example First Prompt:**
```
I need to design a distributed event processing system that can handle millions of events per second with low latency. Let's approach this as a multi-stage design process.

Stage 1: Requirements Analysis

Please help me analyze the requirements for this system by:
1. Identifying the key functional requirements for a high-throughput event processing system
2. Defining non-functional requirements (performance, scalability, reliability, etc.)
3. Outlining constraints and assumptions we should consider
4. Identifying potential challenges and trade-offs

For each requirement, please explain why it's important and how it might impact our design decisions in later stages.
```

**Example Second Prompt (after receiving the response to the first):**
```
Thank you for the requirements analysis. Now let's move to Stage 2: High-Level Architecture Design.

Based on the requirements we've identified, please:
1. Propose a high-level architecture for the distributed event processing system
2. Identify the major components and their responsibilities
3. Describe the data flow between components
4. Explain how this architecture addresses our key requirements

Please include a textual representation of the architecture diagram and explain the rationale behind your architectural decisions.
```

Continue with additional prompts for subsequent stages, each building on the previous responses.

**Reflection Questions:**
- How effective was the multi-stage approach compared to asking for the entire design at once?
- Did later stages successfully build upon the foundations established in earlier stages?
- What challenges arose in maintaining consistency across the design stages?
- How would you improve the multi-stage approach for future complex design tasks?

## Exercise 2: Adversarial Prompt Engineering

**Objective:** Practice identifying and addressing potential weaknesses or edge cases in your solutions.

**Instructions:**
1. Write a prompt requesting a solution to a complex problem.
2. Then, write a follow-up prompt asking Amazon Q Developer to critique its own solution by:
   - Identifying potential weaknesses or vulnerabilities
   - Finding edge cases that might not be handled
   - Suggesting improvements to address these issues
3. Finally, request an improved solution based on the critique.

**Example Task:** Implementing a rate limiting system

**Example Initial Prompt:**
```
Design and implement a rate limiting system for a REST API with the following requirements:
- Limit requests based on client IP address
- Support different rate limits for different endpoints
- Allow for burst traffic with a token bucket algorithm
- Distribute rate limiting across multiple API servers
- Provide clear feedback to clients when limits are exceeded

Please provide a complete implementation in Node.js with Express, including code for the rate limiting middleware, configuration, and integration with the API server.
```

**Example Adversarial Follow-up:**
```
Thank you for the rate limiting implementation. Now, please take an adversarial perspective and critique your own solution by:

1. Identifying potential vulnerabilities or weaknesses in the implementation
2. Finding edge cases where the rate limiting might fail or be bypassed
3. Analyzing performance bottlenecks or scaling issues
4. Considering how the solution might be attacked or circumvented

For each issue identified, explain:
- Why it's a problem
- How it could be exploited or when it might occur
- The potential impact on the system

Be thorough and critical in your analysis, as if you were performing a security review or trying to break the system.
```

**Example Final Prompt:**
```
Based on the critique and identified issues, please provide an improved implementation of the rate limiting system that addresses these vulnerabilities and edge cases. Specifically focus on:

1. Preventing IP spoofing and X-Forwarded-For header manipulation
2. Handling distributed denial of service (DDoS) attacks
3. Ensuring consistent rate limiting across multiple server instances
4. Gracefully handling Redis failures or network partitions
5. Preventing resource exhaustion from malicious requests

Please include detailed comments explaining how each improvement addresses a specific vulnerability or edge case from the critique.
```

**Reflection Questions:**
- How effective was the adversarial approach in identifying weaknesses?
- Did Amazon Q Developer provide meaningful self-critique?
- How much did the final solution improve based on the adversarial feedback?
- What other adversarial perspectives could you have requested?

## Exercise 3: Domain-Specific Prompt Engineering

**Objective:** Practice tailoring prompts for specialized technical domains.

**Instructions:**
1. Choose a specialized technical domain (e.g., machine learning, blockchain, embedded systems).
2. Research domain-specific terminology, concepts, and best practices.
3. Write a prompt that incorporates domain-specific knowledge and requirements.
4. Evaluate how well Amazon Q Developer responds to domain-specific prompts.

**Example Domain:** Machine Learning Model Deployment

**Example Prompt:**
```
I need to design a system for deploying and serving a machine learning model with the following specifications:

Model details:
- A transformer-based NLP model for text classification
- Model size: 2.3GB
- Inference time: ~100ms on CPU, ~15ms on GPU
- Input: Text (variable length, up to 512 tokens)
- Output: Classification probabilities across 12 categories
- Framework: PyTorch (ONNX-exportable)

Deployment requirements:
- Horizontal scalability to handle up to 1000 requests per second
- Maximum latency of 200ms at p99
- High availability (99.9% uptime)
- Cost-efficient resource utilization
- Monitoring of model performance and drift
- A/B testing capability for model updates
- Gradual rollout of new model versions

Please design a complete ML model serving architecture that addresses these requirements, including:

1. Infrastructure components (Kubernetes, serverless, etc.)
2. Model serving technology (TorchServe, TensorFlow Serving, custom solution, etc.)
3. Scaling strategy and load balancing
4. Model versioning and deployment workflow
5. Monitoring and observability solution
6. Cost optimization approaches

For each component, explain the rationale behind your choice and how it addresses the specific requirements of this ML deployment scenario.
```

**Reflection Questions:**
- How well did Amazon Q Developer handle the domain-specific terminology and concepts?
- Did the response demonstrate understanding of the specialized requirements?
- What domain-specific aspects were missing or could be improved in the response?
- How could you improve your prompt to get more domain-appropriate results?

## Exercise 4: Constraint-Based Problem Solving

**Objective:** Practice guiding Amazon Q Developer to solve problems under specific constraints.

**Instructions:**
1. Choose a programming problem that can be solved in multiple ways.
2. Write a prompt that imposes specific constraints on the solution (e.g., memory limits, performance requirements, restricted language features).
3. Evaluate how well Amazon Q Developer adheres to the constraints while solving the problem.

**Example Task:** Implementing a caching mechanism with constraints

**Example Prompt:**
```
Implement a least recently used (LRU) cache in JavaScript with the following constraints:

Functional requirements:
- Support get(key) and put(key, value) operations
- get(key) should return the value or -1 if not found
- put(key, value) should store the value or update it if the key exists
- When the cache reaches capacity, it should evict the least recently used item
- All operations must have O(1) time complexity

Implementation constraints:
- Do not use any built-in Map or Set objects
- Do not use any array methods with O(n) complexity (e.g., filter, find)
- Maximum memory usage of O(capacity) where capacity is the max number of items
- No external libraries or dependencies
- Must work in all modern browsers (IE11 not required)
- Code must be fully tested with unit tests
- Implementation must be less than 100 lines of code (excluding tests)

Additional requirements:
- Include detailed comments explaining the implementation
- Provide time and space complexity analysis
- Include examples of usage
- Implement proper error handling for edge cases
- Ensure the implementation is thread-safe (if applicable)

Please provide a complete implementation that satisfies all these constraints.
```

**Reflection Questions:**
- How well did Amazon Q Developer adhere to the specified constraints?
- Did imposing constraints lead to a more creative or efficient solution?
- Which constraints were most effective in guiding the implementation?
- What additional constraints could you add to further challenge the solution?

## Exercise 5: Comprehensive System Implementation

**Objective:** Practice requesting and managing the implementation of a complete system with multiple components.

**Instructions:**
1. Define a moderately complex system with multiple interconnected components.
2. Create a series of prompts that:
   - Define the overall system architecture
   - Request implementations of individual components
   - Guide the integration of components
   - Address cross-cutting concerns

**Example Task:** Building a real-time collaborative markdown editor

**Example Architecture Prompt:**
```
I want to build a real-time collaborative markdown editor with the following features:
- Multiple users can edit the same document simultaneously
- Changes are synchronized in real-time across all users
- Markdown preview is updated as users type
- Document history and version control
- User presence indicators showing who is currently editing
- Access control with different permission levels

Please design a comprehensive architecture for this system, including:
1. Frontend architecture (React components, state management)
2. Backend services and APIs
3. Real-time synchronization mechanism
4. Data storage approach
5. Authentication and authorization system

For each component, explain its purpose, responsibilities, and how it interacts with other components.
```

**Example Component Implementation Prompt (after receiving the architecture):**
```
Based on the architecture you designed, I'd like to implement the real-time synchronization component. Please provide:

1. A complete implementation of the real-time synchronization service, including:
   - Server-side code for managing WebSocket connections
   - Conflict resolution algorithm (e.g., Operational Transformation or CRDT)
   - Message format for synchronizing changes
   - Error handling and recovery mechanisms

2. The corresponding client-side implementation that:
   - Connects to the synchronization service
   - Sends local changes to the server
   - Applies remote changes to the local document
   - Handles connection issues and reconnection

Please provide production-ready code with appropriate error handling, logging, and comments.
```

Continue with additional prompts for other components and integration.

**Reflection Questions:**
- How effective was breaking down the system into components for implementation?
- Did the implementations maintain consistency with the overall architecture?
- What challenges arose when integrating the components?
- How would you improve your approach for future complex system implementations?

## Exercise 6: Prompt Chaining for Complex Workflows

**Objective:** Practice creating chains of prompts that build upon each other to accomplish complex tasks.

**Instructions:**
1. Define a complex workflow that involves multiple steps and decision points.
2. Create a series of prompts where each prompt:
   - Builds on the output of previous prompts
   - Makes decisions based on previous results
   - Progressively refines the solution

**Example Workflow:** Analyzing and optimizing a web application's performance

**Example Prompt Chain:**

Prompt 1: Analysis of performance metrics
```
I have a React web application with performance issues. Here are the key metrics from Lighthouse:

- First Contentful Paint: 3.2s
- Largest Contentful Paint: 5.8s
- Time to Interactive: 7.4s
- Total Blocking Time: 850ms
- Cumulative Layout Shift: 0.12
- JavaScript bundle size: 2.4MB (uncompressed)
- Number of HTTP requests: 47

Please analyze these metrics and identify:
1. The most critical performance issues
2. Likely causes of these issues
3. Areas to focus optimization efforts
4. Specific metrics we should aim to improve first

Provide a prioritized list of potential performance issues based on this analysis.
```

Prompt 2: Bundle analysis (based on the response to Prompt 1)
```
Based on your analysis, let's focus on the JavaScript bundle size issue. Here's the output from webpack-bundle-analyzer:

Main bundle (2.4MB):
- react and react-dom: 120KB
- redux and related packages: 150KB
- moment.js: 230KB
- lodash: 180KB
- three.js: 560KB
- various UI component libraries: 450KB
- application code: 710KB

Please analyze this bundle breakdown and recommend:
1. Specific opportunities for reducing bundle size
2. Libraries that could be replaced with lighter alternatives
3. Techniques for code splitting and lazy loading
4. Prioritized action items for bundle optimization
```

Prompt 3: Implementation plan (based on the response to Prompt 2)
```
Thank you for the bundle optimization recommendations. Now I'd like to create an implementation plan for these optimizations.

For each of the following recommendations you made:
1. Replacing moment.js with date-fns
2. Implementing code splitting for routes
3. Using lodash-es with tree shaking
4. Lazy loading the 3D visualization components that use three.js

Please provide:
- Specific implementation steps
- Code examples showing the changes needed
- Expected impact on bundle size
- Potential risks or side effects
- Testing approach to verify the optimization

Focus on practical implementation details that our development team can follow.
```

Continue with additional prompts based on the evolving optimization process.

**Reflection Questions:**
- How effectively did the prompt chain guide the overall workflow?
- Did later prompts successfully build on information from earlier responses?
- What decision points were most important in the workflow?
- How would you improve the prompt chain for similar complex workflows?

## Exercise 7: Hybrid Human-AI Problem Solving

**Objective:** Practice combining your expertise with Amazon Q Developer's capabilities to solve complex problems.

**Instructions:**
1. Choose a complex problem in your area of expertise.
2. Break down the problem into parts where:
   - You provide domain expertise and critical thinking
   - Amazon Q Developer provides implementation details or analysis
3. Create prompts that clearly delineate your contributions and what you expect from Amazon Q Developer.

**Example Task:** Designing a custom authentication system

**Example Prompt:**
```
I'm designing a custom authentication system for a multi-tenant SaaS application. I've already made the following architectural decisions based on our specific requirements:

1. We'll use a JWT-based authentication system with short-lived access tokens (15 minutes) and longer-lived refresh tokens (7 days).

2. We need to support multiple authentication methods:
   - Username/password
   - OAuth2 with Google and Microsoft
   - SAML for enterprise customers

3. We've decided to store user data in PostgreSQL with the following schema:
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255),
  two_factor_enabled BOOLEAN DEFAULT FALSE,
  last_login TIMESTAMP,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE tenants (
  id UUID PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  domain VARCHAR(255) UNIQUE,
  settings JSONB,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE user_tenants (
  user_id UUID REFERENCES users(id),
  tenant_id UUID REFERENCES tenants(id),
  role VARCHAR(50) NOT NULL,
  PRIMARY KEY (user_id, tenant_id)
);
```

4. For security reasons, we need to implement:
   - Rate limiting on authentication attempts
   - Automatic lockout after failed attempts
   - Secure token storage on the client side
   - Ability to revoke all sessions for a user

Based on these decisions, I need your help with:

1. Implementing the token generation and validation logic:
   - How to securely generate JWTs
   - What claims to include in the tokens
   - How to handle token validation and renewal
   - Secure storage and transmission of tokens

2. Designing the refresh token rotation strategy:
   - How to securely implement refresh token rotation
   - How to detect and prevent refresh token reuse
   - Database schema for tracking active tokens

3. Implementing tenant-specific authentication logic:
   - How to handle users belonging to multiple tenants
   - How to encode tenant information in tokens
   - How to enforce tenant-specific permissions

Please provide detailed implementation recommendations and code examples for these specific aspects of the authentication system.
```

**Reflection Questions:**
- How well did the hybrid approach leverage both your expertise and Amazon Q Developer's capabilities?
- Did clearly delineating your decisions help Amazon Q Developer provide more relevant assistance?
- What aspects of the problem benefited most from your human expertise?
- How would you adjust the balance between human and AI contributions in future prompts?

## Next Steps

After completing these advanced exercises, you should have mastered sophisticated prompt engineering techniques for Amazon Q Developer. In the next section, we'll explore real-world scenarios where you can apply these skills to solve practical problems.

---

[Next: Real-world Scenarios](./04-real-world.md) | [Previous: Intermediate Exercises](./02-intermediate.md) | [Back to Main](../README.md)
