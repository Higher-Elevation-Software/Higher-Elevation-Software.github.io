```yaml
---
tags: [Python, Data Extraction, Documentation]
---

# extractor.py

This Python script is responsible for extracting and reading files from various repositories, focusing on specific file types and content length. It is part of the data generation process for the dashboard application.

## Constants

The script defines several constants that are used throughout the code:

- `MIN_CONTENT_LENGTH`: The minimum content length for a file to be considered for extraction.
- `MAX_FILE_SIZE_MB`: The maximum file size (in megabytes) for a file to be processed. Files larger than this size will be skipped.
- `REPOS`: A dictionary that defines the repository paths and the file extensions to be extracted from each repository.
- `EXCLUDED_DIRS`: A set of directory names that should be excluded from the file extraction process.

## Functions

### `should_skip_file(filepath)`

This function determines whether a file should be skipped based on its size or the directory it is located in. It checks if the file is in an excluded directory or if the file size exceeds the `MAX_FILE_SIZE_MB` limit.

### `extract_docs(repo_path, extensions)`

This function extracts and reads files from the specified repository path that match the given file extensions. It uses the `glob` module to find all files with the specified extensions, and then reads the content of each file. If the content length is greater than or equal to the `MIN_CONTENT_LENGTH`, the file path and content are added to the `docs` list. The function also handles any exceptions that may occur during the file reading process.

## Logging

The script sets up basic logging configuration using the `logging` module. The log messages are formatted with the timestamp, log level, and the message.

## Usage

This script is likely used as part of a larger data generation or processing pipeline for the dashboard application. It can be called with the appropriate repository paths and file extensions to extract the necessary content for further processing or analysis.

> [!note]
> This script assumes the existence of several repositories, including `dashboard-webapp`, `dashboard-api`, `dashboard-ui`, and `main-setup-repo`. The file paths and extensions are hardcoded in the `REPOS` dictionary.

## Related Files

- [[data_generation/processor.py]]
- [[data_generation/transformer.py]]
- [[data_generation/loader.py]]

```python
import os
import glob
import logging

# Constants
MIN_CONTENT_LENGTH = 50
MAX_FILE_SIZE_MB = 5  # Skip files larger than 5MB

# Repository paths and file types
REPOS = {
    "dashboard-webapp": {"path": "../dashboard-webapp", "extensions": [".md", ".rb", ".js", ".jsx", ".yml", ".json"]},
    "dashboard-api": {"path": "../dashboard-api", "extensions": [".md", ".rb", ".yml", ".json"]},
    "dashboard-ui": {"path": "../dashboard-ui", "extensions": [".md", ".js", ".jsx", ".tsx", ".yml", ".json"]},
    "main-setup-repo": {"path": "../main-setup-repo", "extensions": [".md", ".sh", ".yml", ".json"]}
}

# ✅ Setup Logging
logging.basicConfig(level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s")

EXCLUDED_DIRS = {"node_modules", "dist", "build", "coverage", ".git", ".venv", "__pycache__"}

def should_skip_file(filepath):
    """Determines if a file should be skipped based on size or directory."""
    if any(skip in filepath for skip in EXCLUDED_DIRS):
        return True
    if os.path.getsize(filepath) / (1024 * 1024) > MAX_FILE_SIZE_MB:
        logging.warning(f"⚠️ Skipping large file: {filepath} (> {MAX_FILE_SIZE_MB}MB)")
        return True
    return False

def extract_docs(repo_path, extensions):
    """Extract and read files matching the given extensions."""
    docs = []
    for ext in extensions:
        pattern = os.path.join(repo_path, '**', '*' + ext)
        for filepath in glob.glob(pattern, recursive=True):
            if not os.path.isfile(filepath) or should_skip_file(filepath):
                continue

            try:
                with open(filepath, 'r', encoding='utf-8', errors='ignore') as f:
                    content = f.read()
                    if len(content) >= MIN_CONTENT_LENGTH:
                        docs.append((filepath, content))
            except Exception as e:
                logging.error(f"❌ Error reading {filepath}: {e}")

    logging.info(f"✅ Extracted {len(docs)} files from {repo_path}")
    return docs
```