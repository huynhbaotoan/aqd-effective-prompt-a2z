# Beginner Exercises

This section provides hands-on exercises to help you practice basic prompt engineering techniques with Amazon Q Developer. These exercises are designed for beginners who are new to prompt engineering and want to develop their skills.

## Exercise 1: Basic Function Generation

**Objective:** Practice creating clear prompts for generating simple functions.

**Instructions:**
1. Write a prompt asking Amazon Q Developer to create a JavaScript function that converts a temperature from Fahrenheit to Celsius.
2. Evaluate the response based on correctness, readability, and error handling.
3. Refine your prompt to improve the result, adding specific requirements like:
   - Function name
   - Parameter validation
   - Rounding options
   - Documentation

**Example Starting Prompt:**
```
Create a JavaScript function that converts temperature from Fahrenheit to Celsius.
```

**Improvement Ideas:**
- Specify the function name and parameters
- Request input validation
- Ask for comments or documentation
- Request example usage
- Specify rounding behavior

**Reflection Questions:**
- How did your initial prompt perform?
- What specific improvements made the biggest difference?
- What aspects of the function did Amazon Q Developer assume that you didn't specify?

## Exercise 2: Error Handling Practice

**Objective:** Learn to request proper error handling in generated code.

**Instructions:**
1. Write a prompt asking Amazon Q Developer to create a function that reads a JSON file in Node.js.
2. Evaluate the error handling in the response.
3. Refine your prompt to specifically request comprehensive error handling for:
   - File not found
   - Invalid JSON
   - Permission issues
   - Unexpected data formats

**Example Starting Prompt:**
```
Write a Node.js function to read and parse a JSON file.
```

**Improvement Ideas:**
- Specify the types of errors to handle
- Request specific error messages
- Ask for try/catch blocks
- Request async/await or Promise-based implementation
- Specify how errors should be reported (thrown, returned, logged)

**Reflection Questions:**
- Did your initial prompt result in any error handling?
- How comprehensive was the error handling in the improved response?
- What error scenarios did you forget to specify?

## Exercise 3: Documentation Requests

**Objective:** Practice requesting well-documented code.

**Instructions:**
1. Write a prompt asking Amazon Q Developer to create a utility function for formatting dates.
2. Evaluate the documentation in the response.
3. Refine your prompt to request specific documentation elements:
   - Function purpose
   - Parameter descriptions
   - Return value description
   - Example usage
   - Edge cases

**Example Starting Prompt:**
```
Create a JavaScript utility function for formatting dates in different formats.
```

**Improvement Ideas:**
- Specify a documentation style (JSDoc, etc.)
- Request specific documentation sections
- Ask for examples with different inputs
- Request edge case documentation
- Specify the level of detail needed

**Reflection Questions:**
- How well-documented was the initial response?
- Which documentation elements were most useful?
- How did specifying a documentation style affect the result?

## Exercise 4: Contextual Information

**Objective:** Practice providing relevant context in your prompts.

**Instructions:**
1. Write a prompt asking Amazon Q Developer to create a function that validates a form input.
2. Evaluate the response based on how well it meets your unstated needs.
3. Refine your prompt by adding contextual information:
   - The programming language and framework (e.g., React, Vue)
   - The type of form (e.g., registration, contact)
   - The specific fields to validate
   - Validation rules and requirements
   - How validation errors should be handled

**Example Starting Prompt:**
```
Create a function that validates form input.
```

**Improvement Ideas:**
- Specify the technology stack
- Describe the form's purpose and fields
- Define validation rules for each field
- Explain how validation errors should be displayed
- Provide context about the user experience

**Reflection Questions:**
- How did the lack of context affect the initial response?
- Which contextual details had the biggest impact on improving the result?
- What assumptions did Amazon Q Developer make when context was missing?

## Exercise 5: Iterative Refinement

**Objective:** Practice the iterative prompt refinement process.

**Instructions:**
1. Write a prompt asking Amazon Q Developer to create a simple to-do list application in HTML, CSS, and JavaScript.
2. Evaluate the initial response and identify areas for improvement.
3. Write a follow-up prompt that refines specific aspects of the solution:
   - Request improvements to the UI design
   - Ask for additional features (e.g., due dates, priorities)
   - Request better code organization
   - Ask for performance optimizations

**Example Starting Prompt:**
```
Create a simple to-do list application using HTML, CSS, and JavaScript.
```

**Example Follow-up Prompt:**
```
The to-do list application looks good, but I'd like to make these improvements:
1. Add the ability to set due dates for tasks
2. Implement task categories or tags
3. Improve the mobile responsiveness of the UI
4. Add local storage to persist tasks between page reloads

Please update the code with these enhancements.
```

**Reflection Questions:**
- How effective was the iterative approach compared to trying to get everything in one prompt?
- What aspects were easier to refine in follow-up prompts?
- How did Amazon Q Developer maintain consistency between iterations?

## Exercise 6: Comparing Alternative Approaches

**Objective:** Practice requesting and evaluating alternative solutions.

**Instructions:**
1. Write a prompt asking Amazon Q Developer to provide two different approaches to implementing a search function for an array of objects.
2. Ask for a comparison of the approaches in terms of:
   - Performance characteristics
   - Code readability
   - Flexibility for future changes
   - Browser compatibility
3. Based on the comparison, request a recommendation for which approach to use.

**Example Prompt:**
```
Please provide two different approaches to implement a search function that filters an array of product objects based on a search term. The function should search across multiple fields (name, description, category) and support partial matches.

For each approach:
1. Provide the implementation code
2. Explain how it works
3. Discuss its performance characteristics
4. Highlight its strengths and weaknesses

Then compare the two approaches and recommend which one would be better for a web application with potentially thousands of products.
```

**Reflection Questions:**
- How thorough was the comparison between approaches?
- Did Amazon Q Developer provide meaningful performance analysis?
- Was the recommendation well-justified?
- What additional information could you have requested to make the comparison more useful?

## Exercise 7: Specifying Requirements Clearly

**Objective:** Practice writing prompts with clear, specific requirements.

**Instructions:**
1. Choose a common programming task (e.g., pagination, form validation, data filtering).
2. Write a prompt with vague, general requirements.
3. Then rewrite the prompt with specific, detailed requirements including:
   - Exact functionality needed
   - Input and output formats
   - Performance requirements
   - Edge cases to handle
   - Error scenarios
4. Compare the responses to both prompts.

**Example Vague Prompt:**
```
Create a pagination component for a web application.
```

**Example Specific Prompt:**
```
Create a React pagination component with the following requirements:

Functionality:
- Display page numbers from 1 to the total number of pages
- Show "Previous" and "Next" buttons
- Highlight the current page
- If there are many pages, show ellipsis (...) and only a subset of page numbers

Props:
- totalItems (number): Total number of items to paginate
- itemsPerPage (number): Number of items per page
- currentPage (number): Current active page
- onPageChange (function): Callback when page changes

Visual Requirements:
- Responsive design that works on mobile and desktop
- Accessible with proper ARIA attributes
- Support for keyboard navigation

Edge Cases:
- Handle cases with 0 items
- Handle cases with only 1 page
- Handle very large numbers of pages (e.g., 1000+)

Please provide the complete component code, including styles and documentation.
```

**Reflection Questions:**
- How much did the specificity of requirements affect the quality of the response?
- Which requirements had the biggest impact on the result?
- What details did you forget to specify that would have improved the result further?

## Next Steps

After completing these beginner exercises, you should have a better understanding of how to craft effective prompts for Amazon Q Developer. In the next section, we'll explore intermediate exercises that build on these fundamentals.

---

[Next: Intermediate Exercises](./02-intermediate.md) | [Previous: Documentation Examples](../examples/04-documentation.md) | [Back to Main](../README.md)
