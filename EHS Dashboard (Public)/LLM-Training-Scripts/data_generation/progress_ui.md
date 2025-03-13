```yaml
---
tags: 
  - python
  - progress-ui
  - rich
  - data-generation
---

# `data_generation/progress_ui.py`

This Python file defines a set of functions that create an elegant and interactive progress tracking user interface (UI) using the `rich` library. The UI includes a rotating ASCII animation, per-repository progress bars, and a dashboard that displays live statistics and sample data. This module is designed to be used in a larger data generation or processing pipeline to provide users with a visually appealing and informative progress tracking experience.

## `rotating_ascii()`

This function continuously rotates a set of ASCII frames to create a fun and engaging animation. It runs in a separate thread to avoid blocking the main execution.

> [!note]
> The `time.sleep(0.2)` function call ensures a smooth animation by introducing a short delay between each frame.

## `setup_progress()`

This function sets up a `rich.progress.Progress` object with a custom configuration, including a progress bar, task description, and time elapsed column.

## `initialize_repo_tasks(progress, repo_stats)`

This function creates individual progress bars for each repository based on the provided `repo_stats` dictionary. It returns a dictionary of `rich.progress.Task` objects, where the keys are the repository names and the values are the corresponding progress tasks.

## `get_dashboard(progress, stats, repo_stats, repo_tasks, data_samples)`

This function builds a refined Rich UI dashboard layout that includes the overall progress, live statistics, and a sample data preview. The dashboard is constructed using the `rich.panel.Panel` and `rich.group.Group` classes.

> [!note]
> The `file_type_samples` dictionary is used to display one sample per file type, ensuring that the sample preview section remains concise.

## `start_ascii_animation()`

This function starts the ASCII animation in a separate thread, allowing it to run continuously without blocking the main execution.

> [!note]
> The `daemon=True` parameter ensures that the animation thread is terminated when the main program exits.

## Dependencies

This module relies on the following external libraries:

- [[rich]]: A Python library for creating rich terminal user interfaces, including progress bars, panels, and text formatting.
- `os`: A built-in Python module for interacting with the operating system.
- `json`: A built-in Python module for working with JSON data.
- `itertools`: A built-in Python module for working with iterators.
- `time`: A built-in Python module for working with time-related functions.
- `threading`: A built-in Python module for creating and managing threads.

## Design Patterns

This module follows the **Separation of Concerns** design pattern by separating the progress tracking functionality into distinct functions. This makes the code more modular, maintainable, and easier to test.

## Architecture

The `progress_ui.py` module is part of the larger `data_generation` package, which likely contains other modules responsible for data processing, transformation, and storage. This module is designed to be integrated into a larger data pipeline to provide users with a visually appealing and informative progress tracking experience.

```python
# progress_ui.py
import os
import json
from rich.console import Console, Group
from rich.progress import Progress, BarColumn, TextColumn, TimeElapsedColumn
from rich.panel import Panel
from itertools import cycle
import time
import threading

console = Console()

# Fun ASCII Animation for Engagement
ASCII_FRAMES = ["🚀  ", "🚀🚀 ", "🚀🚀🚀", "  🚀🚀", "   🚀", "    🚀"]
ASCII_CYCLE = cycle(ASCII_FRAMES)

def rotating_ascii():
    """Continuously rotates the ASCII animation for a fun effect."""
    while True:
        console.print(f"[bold cyan]{next(ASCII_CYCLE)}[/bold cyan]", end="\r")
        time.sleep(0.2)

def setup_progress():
    """Set up an elegant Rich progress tracking UI."""
    progress = Progress(
        BarColumn(),
        TextColumn("[bold blue]{task.description}"),
        TimeElapsedColumn(),
    )
    return progress

def initialize_repo_tasks(progress, repo_stats):
    """Creates individual progress bars for each repository."""
    repo_tasks = {}
    for repo_name, data in repo_stats.items():
        repo_tasks[repo_name] = progress.add_task(
            f"[green]{repo_name}[/green]", total=data["total_files"]
        )
    return repo_tasks

def get_dashboard(progress, stats, repo_stats, repo_tasks, data_samples):
    """
    Builds a refined Rich UI dashboard layout with per-repo progress tracking and a sample data preview.
    The header has been removed from the group to prevent duplication.
    """
    # Code omitted for brevity

def start_ascii_animation():
    """Starts the ASCII animation in a separate thread."""
    animation_thread = threading.Thread(target=rotating_ascii, daemon=True)
    animation_thread.start()
```