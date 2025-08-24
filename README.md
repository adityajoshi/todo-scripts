# todo-scripts

A lightweight set of shell scripts to manage tasks and notes using plain text.  
Built around the [`todo.txt`](https://github.com/todotxt/todo.txt) convention with zero dependencies beyond standard Unix tools.

## ✨ Features

- Add new tasks with automatic created date and default due date.
- Mark tasks as completed by line number.
- Dashboard view:
  - Today's tasks
  - Overdue tasks
- Tabular display of tasks with **Created** and **Due Date**.
- Archive completed tasks to `done.txt`.
- Support for recurring tasks (daily, weekly, monthly).
- 100% plain text, no databases or cloud lock-in.
- Designed to integrate seamlessly with Vim, shell, and git.

## 📂 Scripts Overview

The `bin` folder contains the following scripts:

| Script    | Description                                                                 |
|-----------|-----------------------------------------------------------------------------|
| `tview`   | Shows a dashboard of today's and overdue tasks in a tabular format.         |
| `ta`      | Adds a new task with optional priority, project, context, due date, and repeat interval. |
| `tdone`   | Marks a task as completed by its line number.                               |
| `tarc`    | Archives all completed tasks (lines starting with `x `) to `done.txt`.      |
| `trep`    | Schedules recurring tasks (daily, weekly, monthly) based on repeat tags.    |
| `tupd`    | Updates the due date of a task by line number.                              |

---

## 📥 Installation

### Download the Scripts

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/todo-scripts.git
   cd todo-scripts
   ```

2. **Or download manually:**
   - Click the green "Code" button on the GitHub repository page
   - Select "Download ZIP"
   - Extract the ZIP file to your desired location

### Setup

1. **Make scripts executable:**
   ```bash
   chmod +x bin/*
   ```

2. **Add to your PATH (optional but recommended):**
   
   **Option A: Add to your shell profile (~/.bashrc, ~/.zshrc, etc.):**
   ```bash
   export PATH="$PATH:/path/to/todo-scripts/bin"
   ```
   
   **Option B: Create symbolic links:**
   ```bash
   sudo ln -s /path/to/todo-scripts/bin/tview /usr/local/bin/tview
   sudo ln -s /path/to/todo-scripts/bin/ta /usr/local/bin/ta
   sudo ln -s /path/to/todo-scripts/bin/tdone /usr/local/bin/tdone
   sudo ln -s /path/to/todo-scripts/bin/tarc /usr/local/bin/tarc
   sudo ln -s /path/to/todo-scripts/bin/trep /usr/local/bin/trep
   sudo ln -s /path/to/todo-scripts/bin/tupd /usr/local/bin/tupd
   ```

3. **Reload your shell configuration:**
   ```bash
   source ~/.bashrc  # or ~/.zshrc for zsh users
   ```

### Verify Installation

Test that the scripts are working:
```bash
tview --help
```

You should see usage information for the todo dashboard script.

## 🚀 Usage

### Dashboard View (`tview`)

Display your task dashboard with today's tasks and overdue items:

```bash
tview
```

**What it shows:**
- 📌 **Today's tasks**: Tasks due today
- ⏰ **Overdue tasks**: Tasks past their due date
- Tabular format with Line, Created Date, Due Date, and Task description

**Example output:**
```
==== TASK DASHBOARD (2024-01-15) ====

📌 Today:
Line   | Created    | Due Date     | Task
---------------------------------------------------------------------------------------------
3      | 2024-01-10 | 2024-01-15   | Review project proposal due:2024-01-15

⏰ Overdue:
Line   | Created    | Due Date     | Task
---------------------------------------------------------------------------------------------
1      | 2024-01-05 | 2024-01-10   | Send weekly report due:2024-01-10
```

### Add Tasks (`ta`)

Add new tasks to your todo list:

```bash
ta "Task description" [+project] [@context] [due:YYYY-MM-DD] [repeat:daily|weekly|monthly]
```

**Options:**
- `-p <priority>`: Set priority (A-Z)
- `-r <interval>`: Set repeat interval (`daily`, `weekly`, `monthly`)
- `+project`: Add project tag
- `@context`: Add context tag
- `due:YYYY-MM-DD`: Set due date (optional, defaults to today)
- `repeat:daily|weekly|monthly`: Add repeat tag directly

**Examples:**
```bash
# Basic task
ta "Buy groceries"

# With priority
ta -p A "Important meeting"

# With project and context
ta "Review code" +work @urgent

# With custom due date
ta "Submit report" +work due:2024-01-20

# With repeat interval
ta -r weekly "Take out trash"

# Complete example
ta -p A -r monthly "Prepare report" +work @meeting due:2024-01-18
```

### Mark Tasks Complete (`tdone`)

Mark a task as completed by its line number:

```bash
tdone <line_number>
```

**Example:**
```bash
# Mark task on line 3 as complete
tdone 3
```

**Output:**
```
✅ Marked as done: x 2024-01-15 2024-01-10 Review project proposal due:2024-01-15
```

### Archive Completed Tasks (`tarc`)

Move all completed tasks (lines starting with `x `) from `todo.txt` to `done.txt`:

```bash
tarc
```

**Output:**
```
✅ Archived 2 completed task(s) to done.txt.
```

### Recurring Tasks (`trep`)

Automatically add new instances of recurring tasks based on `repeat:daily`, `repeat:weekly`, or `repeat:monthly` tags:

```bash
trep
```

This script scans your `todo.txt` for tasks with a repeat tag and due date, and adds the next occurrence when the current one is completed.

### Update Task Due Date (`tupd`)

Update the due date of a task by its line number:

```bash
tupd <task_line_number> <proposed_due_date>
```

**Example:**
```bash
tupd 5 2025-09-15
```

---

### Getting Help

All scripts support traditional help flags:

```bash
# Get help for any script
tview -h
tview --help

ta -h
ta --help

tdone -h
tdone --help

tarc -h
tarc --help

trep -h
trep --help

tupd -h
tupd --help
```

**Help output includes:**
- Complete usage instructions
- Available options and arguments
- Practical examples
- Error handling information
- Cross-references to related commands

**Alternative help methods:**
1. **Check script usage** by running without arguments:
   ```bash
   ta
   # Shows: Usage: ta [-p A] <task description> [+project] [@context] [due:YYYY-MM-DD]
   ```

2. **View script contents** to understand functionality:
   ```bash
   cat bin/tview
   cat bin/ta
   cat bin/tdone
   cat bin/tarc
   cat bin/trep
   cat bin/tupd
   ```

3. **Check if todo.txt exists**:
   ```bash
   ls -la todo.txt
   ```

