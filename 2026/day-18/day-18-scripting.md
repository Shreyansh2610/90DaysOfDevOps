# Day 18 – Shell Scripting: Functions & Intermediate Concepts

## Objective

Learn how to write reusable shell scripts using functions, work with local variables, understand strict mode (`set -euo pipefail`), and build a real-world system information reporting script.

---

# Task 1: Basic Functions

## File: `functions.sh`

```bash
#!/usr/bin/env bash

greet() {
    local name="$1"
    echo "Hello, $name!"
}

add() {
    local num1="$1"
    local num2="$2"
    echo $((num1 + num2))
}

greet "Shreyansh"

echo "Sum: $(add 10 20)"
```

### Output

```text
Hello, Shreyansh!
Sum: 30
```

---

# Task 2: Functions with Return Values

## File: `disk_check.sh`

```bash
#!/usr/bin/env bash

check_disk() {
    echo "===== Disk Usage ====="
    df -h /
}

check_memory() {
    echo
    echo "===== Memory Usage ====="
    free -h
}

main() {
    check_disk
    check_memory
}

main
```

### Output

```text
===== Disk Usage =====

Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        98G   23G   71G  25% /

===== Memory Usage =====

               total        used        free      shared
Mem:           7.7Gi       1.2Gi       2.9Gi       90Mi
Swap:          2.0Gi          0B       2.0Gi
```

---

# Task 3: Strict Mode – set -euo pipefail

## File: `strict_demo.sh`

```bash
#!/usr/bin/env bash

set -euo pipefail

echo "Strict mode enabled"

# Uncomment one block at a time

# Example 1: Undefined variable
# echo $UNDEFINED_VAR

# Example 2: Failed command
# ls /path/does/not/exist

# Example 3: Pipeline failure
# false | true

echo "Script completed successfully"
```

### Output

```text
Strict mode enabled
Script completed successfully
```

## Explanation

### set -e

Exit immediately if any command returns a non-zero exit status.

Example:

```bash
ls /invalid/path
echo "This line will not execute"
```

### set -u

Treat undefined variables as errors.

Example:

```bash
echo $MY_VARIABLE
```

Output:

```text
unbound variable
```

### set -o pipefail

Causes a pipeline to fail if any command in the pipeline fails.

Example:

```bash
false | true
```

Without `pipefail`, the pipeline succeeds.

With `pipefail`, the script exits with an error.

---

# Task 4: Local Variables

## File: `local_demo.sh`

```bash
#!/usr/bin/env bash

local_function() {
    local message="I am local"
    echo "Inside function: $message"
}

global_function() {
    message="I am global"
    echo "Inside function: $message"
}

echo "Using local variable"
local_function

echo "Outside function: ${message:-Not Defined}"

echo

echo "Using global variable"
global_function

echo "Outside function: $message"
```

### Output

```text
Using local variable
Inside function: I am local
Outside function: Not Defined

Using global variable
Inside function: I am global
Outside function: I am global
```

---

# Task 5: System Info Reporter

## File: `system_info.sh`

```bash
#!/usr/bin/env bash

set -euo pipefail

print_header() {
    echo
    echo "=================================================="
    echo "$1"
    echo "=================================================="
}

system_info() {
    print_header "Hostname & OS Information"

    echo "Hostname : $(hostname)"
    echo "OS       : $(uname -s)"
    echo "Kernel   : $(uname -r)"
}

uptime_info() {
    print_header "System Uptime"

    uptime -p
}

disk_usage() {
    print_header "Top 5 Largest Directories"

    du -ah / 2>/dev/null | sort -rh | head -n 5
}

memory_usage() {
    print_header "Memory Usage"

    free -h
}

cpu_processes() {
    print_header "Top 5 CPU Consuming Processes"

    ps -eo pid,ppid,cmd,%cpu --sort=-%cpu | head -n 6
}

main() {
    system_info
    uptime_info
    disk_usage
    memory_usage
    cpu_processes
}

main
```

### Sample Output

```text
==================================================
Hostname & OS Information
==================================================
Hostname : ubuntu-server
OS       : Linux
Kernel   : 5.15.0

==================================================
System Uptime
==================================================
up 2 days, 3 hours

==================================================
Top 5 Largest Directories
==================================================
4.0G  /
1.2G  /var
750M  /usr
190M  /home
92M   /opt

==================================================
Memory Usage
==================================================
<free -h output>

==================================================
Top 5 CPU Consuming Processes
==================================================
PID   PPID CMD                 %CPU
1234  1    python3             12.3
2345  1234 node                5.6
```

---

# What I Learned

## 1. Functions Improve Reusability

Functions allow code to be organized into reusable blocks, making scripts cleaner and easier to maintain.

## 2. Strict Mode Prevents Hidden Bugs

Using:

```bash
set -euo pipefail
```

helps catch errors early and makes scripts safer for production use.

## 3. Local Variables Reduce Side Effects

Using the `local` keyword prevents variables from leaking outside a function and avoids accidental overwrites.

---

# Repository Structure

```text
2026/
└── day-18/
    ├── functions.sh
    ├── disk_check.sh
    ├── strict_demo.sh
    ├── local_demo.sh
    ├── system_info.sh
    └── day-18-scripting.md
```

## Submission

```bash
git add .
git commit -m "Complete Day 18 - Shell Scripting Functions & Intermediate Concepts"
git push origin main
```

## Hashtags

```text
#90DaysOfDevOps
#ShellScripting
#Linux
#DevOps
#Automation
#LearningInPublic
```
