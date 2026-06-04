# Day 20 – Bash Scripting Challenge: Log Analyzer and Report Generator

## Objective

Build a Bash script that analyzes log files, extracts important information, generates reports, and archives processed logs.

---

## Files Created

* `log_analyzer.sh`
* `log_report_<date>.txt`

---

## Features Implemented

### Task 1: Input Validation

* Accept log file path as command-line argument.
* Check if argument is provided.
* Verify file exists before processing.

### Task 2: Error Count

Counted all lines containing:

* ERROR
* Failed

Command used:

```bash
grep -Ei "ERROR|Failed" logfile.log | wc -l
```

---

### Task 3: Critical Events

Displayed CRITICAL events with line numbers.

Command used:

```bash
grep -n "CRITICAL" logfile.log
```

---

### Task 4: Top 5 Error Messages

Extracted ERROR messages and identified the most common occurrences.

Command used:

```bash
grep "ERROR" logfile.log \
| sed 's/.*ERROR[: ]*//' \
| sort \
| uniq -c \
| sort -rn \
| head -5
```

---

### Task 5: Summary Report

Generated:

```text
log_report_YYYY-MM-DD.txt
```

Report includes:

* Analysis date
* Log file name
* Total lines processed
* Total error count
* Top 5 error messages
* Critical events with line numbers

---

### Task 6: Archive Processed Logs

Created archive directory if missing:

```bash
mkdir -p archive
```

Moved processed logs:

```bash
mv logfile.log archive/
```

---

## Sample Output

```text
Total Errors Found: 89

--- Critical Events ---
84: CRITICAL Disk space below threshold
217: CRITICAL Database connection lost

--- Top 5 Error Messages ---
45 Connection timed out
32 File not found
28 Permission denied
15 Disk I/O error
9 Out of memory
```

---

## Commands and Tools Used

| Command  | Purpose                  |
| -------- | ------------------------ |
| grep     | Search log entries       |
| grep -n  | Show line numbers        |
| wc -l    | Count lines              |
| sed      | Clean error messages     |
| sort     | Sort output              |
| uniq -c  | Count occurrences        |
| head     | Display top records      |
| mkdir -p | Create archive directory |
| mv       | Move processed logs      |
| date     | Generate report filename |

---

## Key Learnings

1. Bash scripts can automate repetitive log analysis tasks.
2. Combining grep, sort, uniq, and sed provides powerful text-processing capabilities.
3. Generating reports and archiving files helps build real-world system administration workflows.

#90DaysOfDevOps
#DevOpsLearning
