```yaml
---
tags: [Python, Data Extraction, Documentation]
---

# extractor.py

This Python script is responsible for extracting and reading files from various repositories, focusing on specific file types and content length. It is part of the data generation process for the project.

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

This function extracts and reads files from a given repository path that match the specified file extensions. It uses the `glob` module to find all files with the specified extensions, and then reads the content of each file. If the content length is greater than or equal to the `MIN_CONTENT_LENGTH`, the file path and content are added to the `docs` list. The function also handles any exceptions that may occur during the file reading process.

## Logging

The script sets up basic logging configuration using the `logging` module. The log messages are formatted with the timestamp, log level, and the message.

## Usage

This script is likely used as part of a larger data generation or processing pipeline. It can be imported and used in other parts of the project to extract relevant files and their contents from the specified repositories.

> [!note]
> Make sure to update the `REPOS` dictionary with the correct paths to the repositories you want to extract files from.

## Related Files

- [[data_generation/main.py]]
- [[data_generation/preprocessor.py]]
- [[data_generation/transformer.py]]

```