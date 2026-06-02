# Day 17 – Shell Scripting: Loops, Arguments & Error Handling

## Objective

Learn how to use loops, command-line arguments, package installation automation, and error handling in Bash scripts.

---

## Task 1: For Loop

### for_loop.sh

```bash
#!/bin/bash

fruits=("Apple" "Banana" "Mango" "Orange" "Grapes")

for fruit in "${fruits[@]}"
do
    echo "$fruit"
done
```

### Output

```text
Apple
Banana
Mango
Orange
Grapes
```

### count.sh

```bash
#!/bin/bash

for i in {1..10}
do
    echo "$i"
done
```

### Output

```text
1
2
3
4
5
6
7
8
9
10
```

---

## Task 2: While Loop

### countdown.sh

```bash
#!/bin/bash

read -p "Enter a number: " num

while [ "$num" -ge 0 ]
do
    echo "$num"
    num=$((num - 1))
done

echo "Done!"
```

### Output

```text
Enter a number: 5
5
4
3
2
1
0
Done!
```

---

## Task 3: Command-Line Arguments

### greet.sh

```bash
#!/bin/bash

if [ $# -eq 0 ]
then
    echo "Usage: ./greet.sh <name>"
    exit 1
fi

echo "Hello, $1!"
```

### args_demo.sh

```bash
#!/bin/bash

echo "Script Name: $0"
echo "Total Arguments: $#"
echo "All Arguments: $@"
```

---

## Task 4: Install Packages via Script

### install_packages.sh

```bash
#!/bin/bash

if [ "$EUID" -ne 0 ]
then
    echo "Please run this script as root."
    exit 1
fi

packages=("nginx" "curl" "wget")

for pkg in "${packages[@]}"
do
    if dpkg -s "$pkg" &>/dev/null
    then
        echo "$pkg is already installed. Skipping..."
    else
        echo "$pkg is not installed. Installing..."
        apt update -y
        apt install -y "$pkg"
    fi
done
```

---

## Task 5: Error Handling

### safe_script.sh

```bash
#!/bin/bash

set -e

mkdir /tmp/devops-test || echo "Directory already exists"

cd /tmp/devops-test || {
    echo "Failed to enter directory"
    exit 1
}

touch sample.txt || {
    echo "Failed to create file"
    exit 1
}

echo "Script executed successfully."
```

---

## Key Learnings

1. Learned how to automate repetitive tasks using for and while loops.
2. Learned to pass and process command-line arguments using $1, $#, $@, and $0.
3. Learned basic error handling using set -e, exit codes, and conditional operators (||).

## Conclusion

Day 17 focused on making shell scripts more practical and production-ready by introducing loops, arguments, package management automation, and error handling techniques.
