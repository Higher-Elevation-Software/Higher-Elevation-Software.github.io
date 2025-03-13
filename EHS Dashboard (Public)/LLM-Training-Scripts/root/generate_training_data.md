```yaml
---
tags: [Python, Data Generation, Training Data, Obsidian]
---
```

# generate_training_data.py

This Python script is responsible for generating training data for a machine learning model. It extracts code snippets from various repositories, creates training and validation data pairs, and writes them to separate files. The script also provides a progress dashboard and estimates the cost of the data generation process.

## Functions

### `get_file_size(filepath)`
This function calculates the file size in megabytes (MB) for the given file path.

> [!note]
> If the file does not exist, the function returns 0.

### `main()`
The main function of the script, which orchestrates the entire data generation process. It performs the following steps:

1. Estimates the total token usage and cost before running the data generation.
2. Prompts the user to confirm the execution of the script.
3. Extracts the code documents from the specified repositories.
4. Sets up the progress bars and the user interface.
5. Iterates through the extracted documents, creates training data pairs, and updates the statistics.
6. Splits the generated data into training and validation sets.
7. Writes the training and validation data to their respective files.
8. Displays the final dashboard and logs the completion of the process.

## Dependencies

The script relies on the following external libraries:

- `os`: Provides functions for interacting with the operating system.
- `json`: Handles the serialization and deserialization of JSON data.
- `random`: Generates random numbers for shuffling the training data.
- `logging`: Provides logging functionality.
- `rich.live`: Enables the creation of a live-updating console display.
- `rich.panel`: Allows the creation of panels in the console display.
- `data_generation.extractor`: Extracts code documents from the specified repositories.
- `data_generation.training_generator`: Generates training data pairs from the extracted documents.
- `data_generation.progress_ui`: Handles the setup and management of the progress dashboard.

## Design Patterns

The script follows the following design patterns:

1. **Separation of Concerns**: The script separates the concerns of data extraction, training data generation, and progress UI management into different modules and functions.
2. **Modular Design**: The script is organized into several functions, each with a specific responsibility, making the code more maintainable and easier to understand.
3. **Live Updating Dashboard**: The script uses the `rich.live` module to create a live-updating dashboard that displays the progress of the data generation process.

## Related Files

- [[data_generation.extractor]]
- [[data_generation.training_generator]]
- [[data_generation.progress_ui]]