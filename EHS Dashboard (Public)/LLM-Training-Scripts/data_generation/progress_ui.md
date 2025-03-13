```yaml
---
tags: 
  - python
  - progress-ui
  - rich
  - data-generation
---

# `data_generation/progress_ui.py`

This Python file defines a set of functions that create an elegant and interactive progress tracking user interface (UI) using the `rich` library. The UI includes a rotating ASCII animation, per-repository progress bars, and a dashboard that displays live statistics and sample data. This module is designed to be used in a larger data generation or processing pipeline to provide users with a visually engaging and informative progress tracking experience.

## `rotating_ascii()`

This function continuously rotates a set of ASCII frames to create a fun and engaging animation. It runs in a separate thread to avoid blocking the main execution.

> [!note]
> The `ASCII_FRAMES` and `ASCII_CYCLE` variables are used to define the animation sequence and cycle through the frames.

## `setup_progress()`

This function sets up a `rich.progress.Progress` object with a custom configuration, including a progress bar, task description, and time elapsed column.

## `initialize_repo_tasks(progress, repo_stats)`

This function creates individual progress bars for each repository based on the provided `repo_stats` dictionary. It returns a dictionary of `Progress` tasks, where the keys are the repository names.

## `get_dashboard(progress, stats, repo_stats, repo_tasks, data_samples)`

This function builds a refined Rich UI dashboard layout that includes the overall progress, live statistics, and a sample data preview. The dashboard is composed of several `rich.panel.Panel` objects arranged in a `rich.group.Group`.

> [!note]
> The `stats_text` and `sample_text` variables are used to format the information displayed in the dashboard panels.

## `start_ascii_animation()`

This function starts the ASCII animation in a separate thread to run continuously without blocking the main execution.

## Dependencies and Design Patterns

This module heavily relies on the `rich` library, which provides a powerful set of tools for creating visually appealing and interactive command-line interfaces. The use of the `Progress` class, `Panel` objects, and `Group` layout demonstrates the application of the Composite design pattern to build a modular and extensible UI.

The separation of concerns between the animation, progress tracking, and dashboard rendering functions follows the principles of modular design and promotes code reusability and maintainability.

## Related Files

This module is likely part of a larger data generation or processing pipeline, and it may be related to other files in the `data_generation` directory. Some potentially related files could be:

- [[data_generation/data_processor.py]]
- [[data_generation/data_loader.py]]
- [[data_generation/data_exporter.py]]

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
    stats_text = f"""
📄 Files Processed:  [bold yellow]{stats['files_processed']} / {stats['total_files']}[/bold yellow]
📂 Data Processed:   [bold cyan]{stats['processed_size']:.2f}MB / {stats['total_size']:.2f}MB[/bold cyan]
📝 Training Pairs:   [bold cyan]{stats['training_pairs']}[/bold cyan]
✅ Completion:       [bold blue]{stats['completion']}%[/bold blue]
🔄 Current Repo:     [bold red]{stats['current_repo']}[/bold red]
📄 Current File:     [bold magenta]{stats['current_file']}[/bold magenta]
    """
    stats_panel = Panel(stats_text, title="📊 Live Statistics", border_style="green")

    # Show ONE sample per file type (keyed by extension)
    file_type_samples = {}
    for sample in data_samples:
        file_ext = os.path.splitext(sample["filename"])[1]
        if file_ext not in file_type_samples:
            file_type_samples[file_ext] = sample

    sample_text = "\n\n".join(
        f"[bold magenta]{ext}[/bold magenta]: {sample['filename']} - " +
        (
            (sample['messages'][1]['content'][:50].strip() + "...")
            if len(sample['messages']) > 1 and len(sample['messages'][1]['content']) > 50
            else sample['messages'][1]['content'].strip()
        )
        for ext, sample in file_type_samples.items()
    ) if file_type_samples else "No sample data available yet."

    sample_panel = Panel(sample_text, title="📑 Sample Assistant Responses (Concise)", border_style="blue")

    return Group(
        Panel(progress, title="Overall Progress (MB)", border_style="blue"),
        stats_panel,
        sample_panel
    )

def start_ascii_animation():
    """Starts the ASCII animation in a separate thread."""
    animation_thread = threading.Thread(target=rotating_ascii, daemon=True)
    animation_thread.start()
```