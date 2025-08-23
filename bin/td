#!/bin/bash
# Sectioned todo.txt dashboard with due: and tabular format

TODO_FILE="todo.txt"
TODAY=$(date +%Y-%m-%d)

if [ ! -f "$TODO_FILE" ]; then
  echo "No todo.txt file found at $TODO_FILE"
  exit 1
fi

print_table() {
  # Args: filter_mode
  mode=$1
  awk -v today="$TODAY" -v mode="$mode" '
    function print_header() {
      printf "\n%-6s | %-10s | %-12s | %s\n", "Line", "Created", "Due Date", "Task"
      print "---------------------------------------------------------------------------------------------"
    }
    {
      crea="-"
      due="-"
      line=NR
      txt=$0

      if ($1 ~ /^[0-9]{4}-[0-9]{2}-[0-9]{2}$/) {
        crea=$1
        sub(/^[0-9]{4}-[0-9]{2}-[0-9]{2} /,"",txt)
      }
      if (match($0,/due:([0-9]{4}-[0-9]{2}-[0-9]{2})/,arr)) {
        due=arr[1]
      }

      if ($0 !~ /^x /) {
        if (mode=="today" && due==today) {
          if (!printed++) print_header()
          printf "%-6s | %-8s | %-12s | %s\n", line, crea, due, txt
        }
        else if (mode=="overdue" && due!="-") {
          if (due < today) {
            if (!printed++) print_header()
            printf "%-6s | %-8s | %-12s | %s\n", line, crea, due, txt
          }
        }
      }
    }
  ' "$TODO_FILE"
}

echo "==== TASK DASHBOARD ($TODAY) ===="

echo -e "\n📌 Today:"
print_table "today" || echo "  No tasks for today"

echo -e "\n⏰ Overdue:"
print_table "overdue" || echo "  No overdue tasks"
