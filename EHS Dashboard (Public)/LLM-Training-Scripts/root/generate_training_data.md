```yaml
---
tags: [Python, Data Generation, Machine Learning, Obsidian]
---

# generate_training_data.py

This Python script is responsible for generating training data for a machine learning model. It extracts code snippets from various repositories, creates training and validation data pairs, and writes them to separate files. The script also provides a progress dashboard and estimates the cost of the data generation process.

## Functions

### `get_file_size(filepath)`
This function takes a file path as input and returns the file size in megabytes (MB). If the file does not exist, it returns 0.

### `main()`
This is the main function that orchestrates the entire data generation process. It performs the following steps:

1. Estimates the total token usage and cost before running the script.
2. Prompts the user to confirm the execution.
3. Extracts the code documents from the specified repositories.
4. Sets up the progress bars and the user interface.
5. Iterates through the extracted documents, creates training pairs, and updates the statistics.
6. Splits the generated pairs into training and validation sets.
7. Writes the training and validation data to separate files.
8. Displays the final dashboard and logs the completion message.

## Key Components

1. **Data Extraction**: The script uses the `extract_docs` function from the `data_generation.extractor` module to extract code documents from the specified repositories.
2. **Training Data Generation**: The `create_training_pairs` function from the `data_generation.training_generator` module is used to generate training and validation data pairs from the extracted documents.
3. **Progress Tracking**: The script utilizes the `setup_progress`, `get_dashboard`, `start_ascii_animation`, and `initialize_repo_tasks` functions from the `data_generation.progress_ui` module to provide a comprehensive progress dashboard.
4. **File I/O**: The script writes the training and validation data to separate files specified by the `TRAINING_FILE` and `VALIDATION_FILE` constants.

## Dependencies

The script relies on the following external libraries:

- `os`: For file and directory operations.
- `json`: For handling JSON data.
- `random`: For shuffling the training and validation data.
- `logging`: For logging the completion message.
- `rich`: For creating the progress dashboard and user interface.

## Design Patterns

The script follows the **Separation of Concerns** design pattern by separating the data extraction, training data generation, and progress tracking into different modules (`data_generation.extractor`, `data_generation.training_generator`, and `data_generation.progress_ui`, respectively).

## Related Files

- [[data_generation.extractor]]
- [[data_generation.training_generator]]
- [[data_generation.progress_ui]]

> [!note]
> This script is part of a larger project that generates training data for a machine learning model. It is important to ensure that the file paths and other configuration settings are correct before running the script.