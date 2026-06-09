# Shell Scripting Cheat Sheet

A practical quick-reference guide for Bash/Shell scripting.

---

# Quick Reference Table

| Topic    | Key Syntax               | Example                            |
| -------- | ------------------------ | ---------------------------------- |
| Variable | `VAR="value"`            | `NAME="DevOps"`                    |
| Argument | `$1, $2`                 | `./script.sh arg1`                 |
| If       | `if [ condition ]; then` | `if [ -f file ]; then`             |
| For Loop | `for i in list; do`      | `for i in 1 2 3; do`               |
| Function | `name() { ... }`         | `greet() { echo "Hi"; }`           |
| Grep     | `grep pattern file`      | `grep -i error app.log`            |
| Awk      | `awk '{print $1}' file`  | `awk -F: '{print $1}' /etc/passwd` |
| Sed      | `sed 's/old/new/g' file` | `sed -i 's/foo/bar/g' config.txt`  |
| Cut      | `cut -d',' -f1 file.csv` | `cut -d: -f1 /etc/passwd`          |
| Sort     | `sort file.txt`          | `sort -nr scores.txt`              |

---

# 1. Basics

## Shebang

Specifies which interpreter should execute the script.

```bash
#!/bin/bash
```

---

## Running a Script

Make executable:

```bash
chmod +x script.sh
```

Run:

```bash
./script.sh
```

Or:

```bash
bash script.sh
```

---

## Comments

Single-line:

```bash
# This is a comment
```

Inline:

```bash
echo "Hello" # Print greeting
```

---

## Variables

Declare:

```bash
NAME="DevOps"
```

Use:

```bash
echo $NAME
echo "$NAME"
```

Difference:

```bash
echo "$NAME"   # Expands variable
echo '$NAME'   # Literal string
```

---

## Reading User Input

```bash
read -p "Enter your name: " NAME
echo "Hello $NAME"
```

---

## Command-Line Arguments

```bash
echo $0   # Script name
echo $1   # First argument
echo $2   # Second argument
echo $#   # Number of arguments
echo $@   # All arguments
echo $?   # Last command exit code
```

Example:

```bash
./script.sh devops linux
```

---

# 2. Operators and Conditionals

## String Comparisons

```bash
[ "$A" = "$B" ]
[ "$A" != "$B" ]
[ -z "$A" ]
[ -n "$A" ]
```

---

## Integer Comparisons

```bash
[ "$A" -eq "$B" ]
[ "$A" -ne "$B" ]
[ "$A" -lt "$B" ]
[ "$A" -gt "$B" ]
[ "$A" -le "$B" ]
[ "$A" -ge "$B" ]
```

---

## File Test Operators

```bash
-f file.txt
-d mydir
-e file
-r file
-w file
-x file
-s file
```

---

## If Statement

```bash
if [ -f file.txt ]; then
    echo "Exists"
elif [ -d mydir ]; then
    echo "Directory"
else
    echo "Not Found"
fi
```

---

## Logical Operators

```bash
[ -f file ] && echo "Exists"

[ -f file ] || echo "Missing"

! [ -f file ]
```

---

## Case Statement

```bash
case $1 in
    start)
        echo "Starting"
        ;;
    stop)
        echo "Stopping"
        ;;
    *)
        echo "Invalid option"
        ;;
esac
```

---

# 3. Loops

## For Loop (List)

```bash
for i in 1 2 3 4 5
do
    echo $i
done
```

---

## For Loop (C Style)

```bash
for ((i=1;i<=5;i++))
do
    echo $i
done
```

---

## While Loop

```bash
COUNT=1

while [ $COUNT -le 5 ]
do
    echo $COUNT
    ((COUNT++))
done
```

---

## Until Loop

```bash
COUNT=1

until [ $COUNT -gt 5 ]
do
    echo $COUNT
    ((COUNT++))
done
```

---

## Break

```bash
for i in {1..10}
do
    [ $i -eq 5 ] && break
    echo $i
done
```

---

## Continue

```bash
for i in {1..10}
do
    [ $i -eq 5 ] && continue
    echo $i
done
```

---

## Loop Over Files

```bash
for file in *.log
do
    echo $file
done
```

---

## Loop Over Command Output

```bash
cat file.txt | while read line
do
    echo "$line"
done
```

---

# 4. Functions

## Define Function

```bash
greet() {
    echo "Hello"
}
```

---

## Call Function

```bash
greet
```

---

## Function Arguments

```bash
greet() {
    echo "Hello $1"
}

greet DevOps
```

---

## Return Value

```bash
add() {
    echo $(( $1 + $2 ))
}

result=$(add 5 3)
echo $result
```

Using return:

```bash
check() {
    return 0
}
```

---

## Local Variables

```bash
greet() {
    local NAME="Linux"
    echo $NAME
}
```

---

# 5. Text Processing Commands

## grep

```bash
grep "error" app.log
grep -i "error" app.log
grep -r "error" logs/
grep -c "error" app.log
grep -n "error" app.log
grep -v "INFO" app.log
grep -E "error|warning" app.log
```

---

## awk

Print first column:

```bash
awk '{print $1}' file.txt
```

Field separator:

```bash
awk -F: '{print $1}' /etc/passwd
```

Pattern:

```bash
awk '/error/' app.log
```

BEGIN / END:

```bash
awk '
BEGIN {print "Start"}
{print $1}
END {print "End"}
' file.txt
```

---

## sed

Replace text:

```bash
sed 's/foo/bar/'
```

Global replace:

```bash
sed 's/foo/bar/g'
```

Delete line:

```bash
sed '3d' file.txt
```

In-place edit:

```bash
sed -i 's/foo/bar/g' file.txt
```

---

## cut

```bash
cut -d',' -f1 file.csv
cut -d: -f1 /etc/passwd
```

---

## sort

```bash
sort file.txt
sort -n numbers.txt
sort -r file.txt
sort -u file.txt
```

---

## uniq

```bash
uniq file.txt
uniq -c file.txt
```

---

## tr

Uppercase:

```bash
echo "devops" | tr a-z A-Z
```

Delete characters:

```bash
echo "hello123" | tr -d 0-9
```

---

## wc

```bash
wc file.txt
wc -l file.txt
wc -w file.txt
wc -c file.txt
```

---

## head / tail

```bash
head file.txt
head -n 20 file.txt

tail file.txt
tail -n 20 file.txt

tail -f app.log
```

---

# 6. Useful Patterns and One-Liners

## Delete Files Older Than 30 Days

```bash
find /backup -type f -mtime +30 -delete
```

---

## Count Lines in All Log Files

```bash
wc -l *.log
```

---

## Replace String Across Files

```bash
find . -type f -name "*.conf" -exec sed -i 's/old/new/g' {} \;
```

---

## Check Service Status

```bash
systemctl is-active nginx
```

---

## Disk Usage Alert

```bash
df -h | awk '$5+0 > 80'
```

---

## Parse JSON

```bash
cat data.json | jq '.name'
```

---

## Parse CSV

```bash
awk -F, '{print $1}' users.csv
```

---

## Real-Time Error Monitoring

```bash
tail -f app.log | grep --line-buffered ERROR
```

---

# 7. Error Handling and Debugging

## Exit Codes

Success:

```bash
exit 0
```

Failure:

```bash
exit 1
```

Check status:

```bash
echo $?
```

---

## Exit on Error

```bash
set -e
```

---

## Treat Unset Variables as Error

```bash
set -u
```

---

## Catch Pipe Errors

```bash
set -o pipefail
```

---

## Debug Mode

```bash
set -x
```

Disable:

```bash
set +x
```

---

## Trap Cleanup

```bash
cleanup() {
    echo "Cleaning up..."
}

trap cleanup EXIT
```

---

# 8. Common Best Practices

Always quote variables:

```bash
"$VAR"
```

Use meaningful variable names:

```bash
LOG_FILE="/var/log/app.log"
```

Enable strict mode:

```bash
set -euo pipefail
```

Check dependencies:

```bash
command -v jq >/dev/null || exit 1
```

Use functions for reusable code:

```bash
backup_database() {
    echo "Backing up..."
}
```

---

# Quick Debug Checklist

```bash
bash -n script.sh
```

Syntax check only.

```bash
bash -x script.sh
```

Trace execution.

```bash
shellcheck script.sh
```

Static analysis and best practices.

---

## Useful Commands to Remember

```bash
history
alias
which
whereis
type
xargs
find
locate
tee
watch
```

---

**End of Cheat Sheet**
