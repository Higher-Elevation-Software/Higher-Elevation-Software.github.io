```yaml
---
tags: [Python, OpenAI, API]
---

# sample.py - OpenAI API Interaction

This Python script demonstrates how to interact with the OpenAI API to generate a simple text response. It loads the API key from the environment, initializes the OpenAI client, and makes a test API call to the GPT-4 language model.

## Dependencies

This script relies on the following dependencies:

- `openai` - The official OpenAI Python library for interacting with the OpenAI API.
- `os` - The built-in Python module for interacting with the operating system, used to load the API key from the environment.

## Code Walkthrough

1. The script starts by importing the necessary modules: `openai` and `os`.

2. It then loads the OpenAI API key from the environment variable `OPENAI_API_KEY`. If the API key is not found, it prints an error message and exits the script.

3. The OpenAI client is initialized using the `openai.OpenAI()` function, passing the API key as a parameter.

4. The script then makes a test API call to the OpenAI API using the `client.chat.completions.create()` method. This call sends a simple "Say hello." message to the GPT-4 language model and retrieves the generated response.

5. If the API call is successful, the script prints the response content. If an exception occurs, it prints an error message.

> [!note]
> Make sure to set the `OPENAI_API_KEY` environment variable with your actual OpenAI API key before running this script.

## Related Files

This script is a standalone example and does not have any direct dependencies on other files. However, you may want to explore the following related resources:

- [[openai-api-usage-guide]] - A guide on how to effectively use the OpenAI API in your projects.
- [[python-best-practices]] - General best practices for writing high-quality Python code.