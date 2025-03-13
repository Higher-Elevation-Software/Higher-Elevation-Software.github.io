```yaml
---
tags:
  - python
  - data-generation
  - templates
---

# data_generation/templates.py

This file defines a set of templates for generating various types of documentation for a given Python file. These templates can be used to automatically generate summaries, technical documentation, code explanations, system interactions, security analyses, debugging tips, performance optimizations, test cases, comparative analyses, code cleanup suggestions, error handling explanations, dependency analyses, UI/UX impact assessments, and best practices for the file.

## Templates

The `TEMPLATES` list contains a set of dictionaries, each representing a different type of documentation that can be generated. Each dictionary has two keys:

1. `prompt_template`: A string template that defines the prompt for the documentation generation. This template can include placeholders for the filename, context, leading comment, and file content.
2. `completion_template`: A string that defines the suffix to be added to the filename to create the output file name for the generated documentation.

Here's an example of one of the templates:

```python
{
    "prompt_template": "Summarize the purpose and functionality of the file:\nfile: {filename} (context: {context})\n\n{leading_comment}{content}",
    "completion_template": " summary"
}
```

This template generates a summary of the file's purpose and functionality.

## Key Components

The main components of this file are:

1. **TEMPLATES**: A list of dictionaries, each representing a different type of documentation that can be generated.
2. **Prompt Templates**: The `prompt_template` strings that define the prompts for the documentation generation.
3. **Completion Templates**: The `completion_template` strings that define the suffixes to be added to the filename to create the output file names.

## Dependencies and Design Patterns

This file does not have any external dependencies. It follows a simple template-based approach to generating documentation, which can be easily extended or modified to suit the specific needs of the project.

## Related Files

This file is part of the `data_generation` module, and it may be used in conjunction with other files in the same module or the overall project. Some related files might include:

- [[data_generation/generator.py]]
- [[data_generation/utils.py]]

## Notes

> [!note]
> The templates defined in this file are designed to be flexible and customizable. You may need to adjust the prompts and completion templates to fit the specific requirements of your project.