# Prompt Structure and Components

## The Anatomy of an Effective Prompt

A well-structured prompt for Amazon Q Developer typically contains several key components. Understanding these components and how to arrange them will significantly improve your results.

## Core Components of a Prompt

### 1. Task Definition

The task definition clearly states what you want Amazon Q Developer to do.

**Examples:**
- "Generate a function that..."
- "Explain how this code works..."
- "Debug the following code..."
- "Refactor this code to..."

**Best Practices:**
- Use action verbs to specify the exact task
- Be explicit about the expected output format
- Place the task definition at the beginning of your prompt

### 2. Context

Context provides background information that helps Amazon Q Developer understand the broader situation.

**Examples:**
- "I'm building a web application that processes user uploads..."
- "This code is part of a data processing pipeline that handles large CSV files..."
- "We're using React 18 with TypeScript in a Next.js project..."

**Best Practices:**
- Include relevant technical environment details
- Mention frameworks, libraries, or AWS services being used
- Explain the purpose of the code within the larger system
- Keep context concise but informative

### 3. Input/Code

This is the actual code or description that Amazon Q Developer will work with.

**Examples:**
- Code snippets that need to be explained, debugged, or refactored
- Descriptions of functionality for code generation
- Error messages for debugging assistance

**Best Practices:**
- Use code blocks with proper formatting and syntax highlighting
- Provide complete, runnable code when possible
- Include relevant imports or dependencies
- Comment key parts if they need special attention

### 4. Requirements and Constraints

These are specific conditions that the solution must satisfy.

**Examples:**
- "The function must be thread-safe..."
- "Optimize for readability over performance..."
- "Use only standard library functions..."
- "The solution must work with AWS Lambda..."

**Best Practices:**
- Be explicit about non-negotiable requirements
- Specify performance considerations
- Mention compatibility requirements
- List any limitations or restrictions

### 5. Expected Output Format

This describes how you want the response to be structured.

**Examples:**
- "Provide the solution as a complete Python class..."
- "Explain the code line by line..."
- "Format the response as a markdown table..."
- "Include comments explaining your reasoning..."

**Best Practices:**
- Specify the programming language if applicable
- Indicate the level of detail needed
- Request specific formatting if important
- Ask for explanations if you want reasoning

## Prompt Templates

Here are some templates for common scenarios:

### Code Generation Template

```
Task: Generate [type of code] that [performs specific function]

Context: I'm working on [project description] using [technologies/frameworks]. 

Requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

Expected Output: Please provide a complete [language] [code type] with comments explaining key parts.
```

### Code Explanation Template

```
Task: Explain how the following [language] code works

Code:
    [code snippet]


Context: This is part of [larger system description].

Expected Output: Please provide a detailed explanation with:
- Overall purpose
- Step-by-step breakdown
- Key concepts used
- Any potential issues or edge cases
```

### Debugging Template

```
Task: Debug the following code that's [description of issue]

Code:
    [problematic code]

Error Message:
[error message if available]

Context: This happens when [conditions when error occurs].

Expected Output: Please identify the issue, explain why it's happening, and provide a fixed version of the code.
```

### Refactoring Template

```
Task: Refactor this code to [improvement goal]

Original Code:
    [code to refactor]


Context: This code is [context about the code's purpose and environment].

Requirements:
- [Specific refactoring requirement]
- Maintain the same functionality
- [Any other constraints]

Expected Output: Please provide the refactored code with comments explaining your changes and their benefits.
```

## Putting It All Together

Let's see a complete example of a well-structured prompt:

```
Task: Generate a Python function that processes AWS S3 event notifications and extracts metadata from newly uploaded images.

Context: I'm building a serverless image processing pipeline using AWS Lambda, S3, and DynamoDB. When users upload images to an S3 bucket, I need to extract metadata and store it in DynamoDB.

Requirements:
- The function should handle S3 event notifications from Lambda
- Extract image metadata (dimensions, format, size, creation date)
- Use the Pillow library for image processing
- Handle potential errors gracefully
- Support JPEG, PNG, and GIF formats
- Optimize for Lambda execution (minimize memory usage)

Expected Output: Please provide a complete Python function with error handling, appropriate logging, and comments explaining the key parts. Include example usage as a Lambda handler.
```

## Key Takeaways

- Well-structured prompts have clear components that guide Amazon Q Developer
- Different tasks may require different prompt structures
- Being explicit about your requirements leads to better results
- Templates can help ensure you include all necessary components
- The order of information matters - task definition first, followed by context and details

## Next Steps

In the next section, we'll explore how to provide effective context and specificity in your prompts.

---

[Next: Context and Specificity](./04-context.md) | [Previous: Understanding Amazon Q Developer's Capabilities](./02-capabilities.md) | [Back to Main](../README.md)
