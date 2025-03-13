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

4. The script then makes a test API call to the OpenAI API using the `client.chat.completions.create()` method. This call sends a simple "Say hello" message to the GPT-4 language model and retrieves the generated response.

5. If the API call is successful, the script prints the response. If an exception occurs, it prints an error message.

> [!note]
> Make sure to set the `OPENAI_API_KEY` environment variable with your actual OpenAI API key before running this script.

## Related Files

This script is a standalone example and does not have any direct dependencies on other files. However, you may want to consider creating additional scripts or modules to handle more complex OpenAI API interactions or to integrate the functionality into a larger application.

```python
import openai
import os

# Load API Key
api_key = os.getenv("OPENAI_API_KEY")
if not api_key:
    print("❌ ERROR: OpenAI API key is missing. Set OPENAI_API_KEY in your environment variables.")
    exit(1)

# Initialize client
client = openai.OpenAI(api_key=api_key)

# Test API call
try:
    response = client.chat.completions.create(
        model="gpt-4-turbo",
        messages=[{"role": "system", "content": "Say hello."}],
        temperature=0.7,
        max_tokens=50
    )
    print("✅ OpenAI API Response:", response.choices[0].message.content)
except Exception as e:
    print("❌ ERROR calling OpenAI API:", str(e))
```