#!/bin/bash

TODO_FILE="todo.txt"
lineno=$1

# Validate argument
if ! [[ "$lineno" =~ ^[0-9]+$ ]]; then
  echo "❌ Invalid line number."
  exit 1
fi

# File check
if [ ! -f "$TODO_FILE" ]; then
  echo "❌ $TODO_FILE not found."
  exit 1
fi

# Line range check
total=$(wc -l < "$TODO_FILE")
if (( lineno < 1 || lineno > total )); then
  echo "❌ Line number $lineno out of range (1–$total)."
  exit 1
fi

# Already done check
if sed -n "${lineno}p" "$TODO_FILE" | grep -q "^x "; then
  echo "⚠️  Task on line $lineno is already marked done."
  exit 0
fi

# Mark as done 
sed -i "${lineno}s/^/x $(date +%F) /" "$TODO_FILE"

# Show confirmation
task=$(sed -n "${lineno}p" "$TODO_FILE")
echo "✅ Marked as done: $task"

