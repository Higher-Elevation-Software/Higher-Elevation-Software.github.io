```yaml
---
tags: 
  - python
  - data-processing
  - text-cleaning
---
```

# `data_generation/parser.py`

This Python file contains utility functions for cleaning and extracting leading comments from text content. It is likely used as part of a larger data processing or generation pipeline, where the ability to normalize text and extract metadata from files is important.

## `clean_text(text)`

This function takes a string `text` as input and returns a cleaned version of the text. It normalizes whitespace by replacing all consecutive whitespace characters with a single space, and then strips any leading or trailing whitespace.

```python
def clean_text(text):
    """Clean text by normalizing whitespace and stripping excess newlines."""
    return re.sub(r'\s+', ' ', text.strip())
```

## `extract_leading_comment(content, file_ext)`

This function takes two arguments: `content`, which is the raw text content of a file, and `file_ext`, which is the file extension. It then attempts to extract the leading comment from the file based on the file extension.

The function uses a dictionary of regular expression patterns to match the leading comment for different file types (`.rb`, `.js`, `.jsx`, and `.tsx`). If a matching pattern is found, the function returns the leading comment, stripped of any surrounding whitespace, followed by an extra newline. If no matching pattern is found, the function returns an empty string.

```python
def extract_leading_comment(content, file_ext):
    """Extract the leading comment from a file if applicable."""
    patterns = {
        ".rb": r'^(#.*\n)+',
        ".js": r'^((//.*\n)+|(/\*.*?\*/\n))',
        ".jsx": r'^((//.*\n)+|(/\*.*?\*/\n))',
        ".tsx": r'^((//.*\n)+|(/\*.*?\*/\n))'
    }
    pattern = patterns.get(file_ext)
    if pattern:
        match = re.match(pattern, content, re.DOTALL)
        if match:
            return match.group(0).strip() + "\n\n"
    return ""
```

> [!note]
> This file relies on the `re` (regular expressions) module from the Python standard library. No other external dependencies are used.

The functions in this file are likely used in a larger data processing or generation pipeline, where the ability to clean text and extract metadata from files is important. For example, this file could be used in conjunction with other files that handle data extraction, transformation, or storage.

Related files:
- [[data_generation/data_extractor.py]]
- [[data_generation/data_transformer.py]]
- [[data_generation/data_loader.py]]