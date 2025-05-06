# Context and Specificity

## The Power of Context

Context is crucial for getting high-quality responses from Amazon Q Developer. Without adequate context, even the most sophisticated AI will struggle to provide relevant and accurate assistance.

## Types of Context to Include

### 1. Technical Environment

**What to Include:**
- Programming language and version
- Frameworks and libraries being used
- AWS services involved
- Development environment details
- Target deployment environment

**Example:**
```
I'm working with Python 3.9, FastAPI, and boto3 to build a service that will be deployed as an AWS Lambda function behind API Gateway.
```

### 2. Project Background

**What to Include:**
- Project purpose and goals
- Current development stage
- Team structure (if relevant)
- Timeline constraints
- Existing architecture

**Example:**
```
This is part of a customer-facing analytics dashboard we're building. We've already implemented the data collection pipeline, and now we need to create the visualization components.
```

### 3. Code Context

**What to Include:**
- Related code that might affect the solution
- Database schemas
- API contracts
- Dependencies between components
- Existing patterns or conventions

**Example:**
```
Here's our current database schema:

CREATE TABLE users (
  id UUID PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE user_preferences (
  user_id UUID REFERENCES users(id),
  preference_key VARCHAR(50) NOT NULL,
  preference_value TEXT NOT NULL,
  PRIMARY KEY (user_id, preference_key)
);

The function needs to work with this existing schema.
```

### 4. Constraints and Requirements

**What to Include:**
- Performance requirements
- Security considerations
- Compliance requirements
- Backward compatibility needs
- Resource limitations

**Example:**
```
The solution must:
- Handle up to 1000 requests per second
- Comply with GDPR requirements for data handling
- Work within Lambda's 512MB memory allocation
- Complete processing within 200ms
```

## The Art of Specificity

Specificity is about being precise and detailed in your requests. It eliminates ambiguity and guides Amazon Q Developer toward your desired outcome.

### Techniques for Increasing Specificity

#### 1. Use Precise Terminology

**Less Specific:**
```
Generate code to process data from a database.
```

**More Specific:**
```
Generate a Python function that queries a PostgreSQL database for user transaction records from the last 7 days and calculates the average transaction amount per user.
```

#### 2. Specify Input and Output Formats

**Less Specific:**
```
Write code to convert data formats.
```

**More Specific:**
```
Write a JavaScript function that converts a CSV string input into a JSON array of objects, where the first row of the CSV represents the property names for each object.
```

#### 3. Provide Examples

**Less Specific:**
```
Generate a function to validate email addresses.
```

**More Specific:**
```
Generate a function to validate email addresses. The function should:
- Return true for valid emails like "user@example.com" or "name.surname+tag@company-name.co.uk"
- Return false for invalid emails like "user@" or "user@.com" or "@example.com"
- Check for proper domain format
- Allow for subdomains
```

#### 4. Quantify When Possible

**Less Specific:**
```
Make this code more efficient.
```

**More Specific:**
```
Optimize this Python function to reduce its execution time by at least 30% when processing arrays with 10,000+ elements. The current function takes approximately 500ms to process 10,000 elements.
```

#### 5. Specify Edge Cases

**Less Specific:**
```
Write a function to divide two numbers.
```

**More Specific:**
```
Write a TypeScript function to divide two numbers that:
- Handles division by zero by returning null
- Returns the result rounded to 2 decimal places
- Throws a typed error if non-numeric inputs are provided
- Handles very large numbers (up to 10^15)
```

## Balancing Context and Conciseness

While context and specificity are important, there's a balance to strike:

1. **Prioritize Relevance**: Include only context that directly impacts the solution
2. **Organize Information**: Use clear sections and formatting
3. **Eliminate Redundancy**: Don't repeat the same information multiple times
4. **Focus on Critical Details**: Emphasize what's most important for the task

## Context Injection Techniques

### 1. Progressive Disclosure

Start with essential context and add more as needed through follow-up prompts.

**Initial Prompt:**
```
Generate a basic AWS Lambda function in Python that processes S3 events.
```

**Follow-up:**
```
Now enhance the function to extract EXIF data from image files and store it in DynamoDB.
```

### 2. Context Categorization

Organize context into clear categories to make it easier to process.

```
ENVIRONMENT:
- Python 3.9
- AWS Lambda with 512MB memory
- S3 trigger for image uploads

REQUIREMENTS:
- Extract EXIF data from uploaded images
- Store metadata in DynamoDB
- Handle errors gracefully
- Support JPEG and PNG formats

CONSTRAINTS:
- Complete processing within 10 seconds
- Minimize Lambda execution cost
```

### 3. Visual Separation

Use formatting to separate different types of context.

```
# TASK
Generate a Python function to process image uploads in AWS Lambda

# EXISTING CODE
def lambda_handler(event, context):
    # TODO: Implement image processing
    pass

# REQUIREMENTS
- Extract image metadata
- Store in DynamoDB
- Handle errors

# EXPECTED OUTPUT
Complete Python function ready to deploy as Lambda
```

## Key Takeaways

- Context provides the background information Amazon Q Developer needs to generate relevant solutions
- Specificity eliminates ambiguity and guides the AI toward precise outcomes
- Different types of context (technical, project, code, constraints) serve different purposes
- Balance detail with conciseness by focusing on relevant information
- Organize context clearly to make it easier for Amazon Q Developer to process

## Next Steps

In the next section, we'll explore advanced prompt engineering techniques that build upon these fundamentals.

---

[Next: Chain of Thought Prompting](../advanced/01-chain-of-thought.md) | [Previous: Prompt Structure and Components](./03-structure.md) | [Back to Main](../README.md)
