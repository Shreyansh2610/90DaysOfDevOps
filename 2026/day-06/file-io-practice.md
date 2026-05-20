# Day 06 – Linux File Read/Write Practice

## Creating the file

### Command

```bash
touch notes.txt
```

### Output

```bash
(no output)
```

---

## Writing lines into the file

### Command

```bash
echo "Linux file practice started" > notes.txt
echo "Learning file read and write commands" >> notes.txt
```

### Output

```bash
(no output)
```

---

## Using tee to append and display output

### Command

```bash
echo "tee command appends and displays output" | tee -a notes.txt
```

### Output

```txt
tee command appends and displays output
```

---

## Adding more lines

### Command

```bash
echo "cat reads the complete file" >> notes.txt
echo "head shows the first lines" >> notes.txt
echo "tail shows the last lines" >> notes.txt
```

### Output

```bash
(no output)
```

---

## Reading the full file

### Command

```bash
cat notes.txt
```

### Output

```txt
Linux file practice started
Learning file read and write commands
tee command appends and displays output
cat reads the complete file
head shows the first lines
tail shows the last lines
```

---

## Reading first 2 lines

### Command

```bash
head -n 2 notes.txt
```

### Output

```txt
Linux file practice started
Learning file read and write commands
```

---

## Reading last 2 lines

### Command

```bash
tail -n 2 notes.txt
```

### Output

```txt
head shows the first lines
tail shows the last lines
```
