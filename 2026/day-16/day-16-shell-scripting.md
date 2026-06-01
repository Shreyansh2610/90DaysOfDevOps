# Day 16 – Shell Scripting Basics

## Objective

Learn the fundamentals of shell scripting, including:

* Shebang (`#!/bin/bash`)
* Variables
* User input using `read`
* Conditional statements (`if-else`)
* File existence checks
* Basic automation with shell scripts

---

# Task 1: Your First Script

## Script: hello.sh

```bash
#!/bin/bash

echo "Hello, DevOps!"
```

### Make Executable

```bash
chmod +x hello.sh
```

### Run Script

```bash
./hello.sh
```

### Output

```text
Hello, DevOps!
```

### What Happens If You Remove the Shebang?

The shebang tells Linux which interpreter should execute the script.

Without the shebang:

```bash
./hello.sh
```

The script may still work if your current shell is Bash, but it becomes less portable and can fail when executed by a different shell.

---

# Task 2: Variables

## Script: variables.sh

```bash
#!/bin/bash

NAME="Shreyansh"
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"
```

### Run

```bash
chmod +x variables.sh
./variables.sh
```

### Output

```text
Hello, I am Shreyansh and I am a DevOps Engineer
```

### Single Quotes vs Double Quotes

#### Double Quotes

```bash
echo "Hello $NAME"
```

Output:

```text
Hello Shreyansh
```

#### Single Quotes

```bash
echo 'Hello $NAME'
```

Output:

```text
Hello $NAME
```

### Difference

* Double quotes expand variables.
* Single quotes treat everything as plain text.

---

# Task 3: User Input with read

## Script: greet.sh

```bash
#!/bin/bash

read -p "Enter your name: " NAME
read -p "Enter your favourite tool: " TOOL

echo "Hello $NAME, your favourite tool is $TOOL"
```

### Run

```bash
./greet.sh
```

### Sample Output

```text
Enter your name: Shreyansh
Enter your favourite tool: Docker

Hello Shreyansh, your favourite tool is Docker
```

---

# Task 4: If-Else Conditions

## Script: check_number.sh

```bash
#!/bin/bash

read -p "Enter a number: " NUM

if [ "$NUM" -gt 0 ]; then
    echo "Positive Number"
elif [ "$NUM" -lt 0 ]; then
    echo "Negative Number"
else
    echo "Zero"
fi
```

### Sample Output

```text
Enter a number: 10
Positive Number
```

```text
Enter a number: -5
Negative Number
```

```text
Enter a number: 0
Zero
```

---

## Script: file_check.sh

```bash
#!/bin/bash

read -p "Enter filename: " FILE

if [ -f "$FILE" ]; then
    echo "File exists."
else
    echo "File does not exist."
fi
```

### Sample Output

```text
Enter filename: hello.sh
File exists.
```

```text
Enter filename: test.sh
File does not exist.
```

---

# Task 5: Combine It All

## Script: server_check.sh

```bash
#!/bin/bash

SERVICE="ssh"

read -p "Do you want to check the status? (y/n): " CHOICE

if [ "$CHOICE" = "y" ]; then

    if systemctl is-active --quiet "$SERVICE"; then
        echo "$SERVICE is active."
    else
        echo "$SERVICE is not active."
    fi

else
    echo "Skipped."
fi
```

### Sample Output (Active Service)

```text
Do you want to check the status? (y/n): y

ssh is active.
```

### Sample Output (Skipped)

```text
Do you want to check the status? (y/n): n

Skipped.
```

---

# Key Learnings

## 1. Importance of Shebang

The shebang (`#!/bin/bash`) specifies which interpreter executes the script and ensures consistent behavior.

## 2. Variables and User Input

Variables store data, while the `read` command allows interactive user input during script execution.

## 3. Conditional Logic

Using `if`, `elif`, and `else` enables scripts to make decisions and automate system administration tasks.

---

# Directory Structure

```text
2026/
└── day-16/
    ├── day-16-shell-scripting.md
    ├── hello.sh
    ├── variables.sh
    ├── greet.sh
    ├── check_number.sh
    ├── file_check.sh
    └── server_check.sh
```

---

# Git Commands

```bash
git add .
git commit -m "Day 16: Shell Scripting Basics"
git push origin main
```
