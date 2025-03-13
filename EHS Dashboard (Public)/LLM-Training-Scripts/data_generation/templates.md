```yaml
---
tags:
  - python
  - documentation
  - templates
---

# data_generation/templates.py

This Python file defines a set of templates for generating various types of documentation for a given code file. These templates can be used to automatically generate summaries, technical documentation, code explanations, system interactions, security analyses, debugging tips, performance optimizations, test cases, comparative analyses, code cleanup suggestions, error handling descriptions, dependency analyses, UI/UX impact assessments, and best practices.

## Templates

The `TEMPLATES` list contains dictionaries, each representing a different type of documentation template. Each template has two keys:

1. `prompt_template`: A string that defines the prompt for the documentation generation. This string can include placeholders for the filename, context, leading comment, and file content.
2. `completion_template`: A string that defines the suffix to be added to the filename to create the output file name.

Here's an example of one of the templates:

```python
{
    "prompt_template": "Summarize the purpose and functionality of the file:\nfile: {filename} (context: {context})\n\n{leading_comment}{content}",
    "completion_template": " summary"
}
```

This template generates a summary of the file's purpose and functionality.

> [!note]
> The templates are designed to be used with a language model or other text generation system to produce the actual documentation content.

## Key Components

The templates cover a wide range of documentation aspects, including:

- **Summary**: Provides a high-level overview of the file's purpose and functionality.
- **Technical Documentation**: Generates detailed technical documentation for the file.
- **Code Explanation**: Explains how the code in the file works, including its key functions and dependencies.
- **System Interaction**: Describes how the file fits into the overall project and interacts with other components.
- **Security Risks**: Identifies potential security vulnerabilities and suggests improvements.
- **Debugging Tips**: Provides debugging tips, including common issues and troubleshooting steps.
- **Performance Analysis**: Analyzes the performance of the code and suggests potential optimizations.
- **Test Cases**: Generates unit tests and test cases to validate the functionality of the file.
- **Comparative Analysis**: Compares and contrasts the functionality of the file with another related file in the project.
- **Code Cleanup**: Identifies redundant or unused code sections.
- **Error Handling**: Explains the error-handling mechanisms and suggests improvements for robustness.
- **Dependency Analysis**: Lists all dependencies used in the file and analyzes their impact on the project.
- **UI/UX Impact**: Explains how the file contributes to the user experience and UI functionality.
- **Best Practices**: Suggests best practices for writing and maintaining the code in the file.

## Related Files

The templates in this file are used in the overall [[data_generation/generator.py]] module to generate documentation for various code files in the project.