```yaml
---
tags:
  - python
  - data-generation
  - training
  - openai
  - documentation
---

# data_generation/training_generator.py

This Python file is responsible for generating training data for an AI-powered code assistant. It utilizes the OpenAI API to provide dynamic responses to various prompts related to code analysis, documentation, debugging, security, and testing.

The file includes the following key components:

## Configuration Constants

- `MAX_PROMPT_TOKENS`: The maximum number of tokens allowed in the prompt sent to the OpenAI API.
- `OPENAI_API_KEY`: The API key for accessing the OpenAI API.
- `USE_OPENAI`: A flag to enable or disable the use of the OpenAI API for testing purposes.

## OpenAI API Client

The file sets up an OpenAI API client using the provided API key.

## Logging Setup

The file configures logging to provide informative messages during the execution of the code.

## Utility Functions

1. `estimate_task_cost()`: Estimates the total token usage and cost before running the code generation process.
2. `call_openai_api(prompt)`: Sends a request to the OpenAI API to generate a response based on the provided prompt.
3. `generate_assistant_response(prompt_type, filename, content, context)`: Generates an AI-driven response dynamically using the OpenAI API.
4. `create_training_pairs(filepath, content, repo_name)`: Creates training pairs from the given file content, using the "summarize" prompt type as an example.

## Dependencies

The file attempts to import the `extract_docs` function and the `REPOS` dictionary from the `data_generation.extractor` module. If the import fails, it provides fallback implementations.

> [!note]
> The `extract_code_statistics` function is a stub implementation that should be replaced with your actual logic as needed.

## Related Files

- [[data_generation/parser.py]]
- [[data_generation/tokenizer.py]]
- [[data_generation/templates.py]]
- [[data_generation/extractor.py]]

```python
import os
import json
import re
import openai
import logging
from data_generation.parser import clean_text, extract_leading_comment
from data_generation.tokenizer import estimate_token_count, truncate_text_by_tokens
from data_generation.templates import TEMPLATES

# Attempt to import extract_docs and REPOS; provide fallbacks if not available.
try:
    from data_generation.extractor import extract_docs, REPOS
except ImportError:
    REPOS = {}
    def extract_docs(path, extensions):
        return []

# Stub for extract_code_statistics.
def extract_code_statistics(content, filename):
    """
    Extract basic code statistics from the given content.
    This is a stub implementation; replace with your actual logic as needed.
    """
    lines = content.count("\n")
    functions = len(re.findall(r"def\s+\w+\(", content))
    imports = len(re.findall(r"import\s+\w+", content))
    dependencies = []  # Extend this logic to extract dependencies if needed.
    return {
        "lines": lines,
        "functions": functions,
        "imports": imports,
        "dependencies": dependencies
    }

# 🛠 Configuration Constants
MAX_PROMPT_TOKENS = 1500
OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")  # Ensure API key is set
USE_OPENAI = True  # ✅ Set to False to disable OpenAI API calls for testing

# ✅ OpenAI API Client (Fixes SDK v1.0+ compatibility)
client = openai.OpenAI() if OPENAI_API_KEY else None

# ✅ Setup Logging
logging.basicConfig(level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s")

TOKEN_COST_PER_1K = 0.002  # Approximate cost per 1K tokens for GPT-4-Turbo

# ... (rest of the code)
```