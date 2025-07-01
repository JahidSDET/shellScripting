Here's a well-organized DevOps **reference note** for frequently used `sh` (Shell) commands. This includes **functions**, **variables**, **file operations**, **loops**, **conditions**, **cron jobs**, **log parsing**, and **exit statuses**.

---

# 🧾 DevOps Shell Scripting 
## 🧠 Basics

```sh
#!/bin/bash  # Always start scripts with the shebang line
```

### Variables

```sh
NAME="devops"
echo "Hello $NAME"
```

### Functions

```sh
greet() {
  echo "Hello, $1"
}
greet "World"
```

---

## 📁 File Operations

### Create & Write to File

```sh
echo "New content" > file.txt        # Overwrites
echo "More content" >> file.txt      # Appends
```

### Read File Line-by-Line

```sh
while read line; do
  echo "$line"
done < file.txt
```

### Check File/Dir Exists

```sh
if [ -f file.txt ]; then
  echo "File exists"
fi

if [ -d /path/to/dir ]; then
  echo "Directory exists"
fi
```

---

## 🔁 Loops and Conditions

### For Loop

```sh
for i in {1..5}; do
  echo "Number $i"
done
```

### While Loop

```sh
count=0
while [ $count -lt 5 ]; do
  echo "Count: $count"
  count=$((count + 1))
done
```

### If-Else Condition

```sh
if [ "$1" == "start" ]; then
  echo "Starting..."
elif [ "$1" == "stop" ]; then
  echo "Stopping..."
else
  echo "Unknown command"
fi
```

---

## ⏰ Cron Jobs (Scheduled Tasks)

Edit cron jobs:

```sh
crontab -e
```

Example entries:

```sh
# ┌───────────── min (0-59)
# │ ┌───────────── hour (0-23)
# │ │ ┌───────────── day of month (1-31)
# │ │ │ ┌───────────── month (1-12)
# │ │ │ │ ┌───────────── day of week (0-6, Sunday=0)
# │ │ │ │ │
# │ │ │ │ │
# * * * * * <command>

# Run script every day at 2AM
0 2 * * * /home/user/backup.sh

# Run every 5 mins
*/5 * * * * /home/user/check_service.sh
```

---

## 🔍 Log Parsing (grep, awk, sed)

### `grep` – search logs

```sh
grep "ERROR" /var/log/syslog
grep -i "failed" /var/log/auth.log
```

### `awk` – column-based parsing

```sh
awk '{print $5}' /var/log/syslog  # prints 5th column
awk '/error/ {print $0}' logfile.log
```

### `sed` – stream editor

```sh
sed 's/error/ERROR/g' logfile.log     # replace
sed -n '10,20p' logfile.log           # print lines 10-20
```

---

## ❗ Exit Status and Error Handling
$? — This holds the exit status of the last command that was run.

-eq — This means "equal to" in shell scripting.

0 — Exit status 0 means success.
### Check Last Command Status

```sh
if [ $? -ne 0 ]; then
  echo "Previous command failed"
  exit 1
fi
```

### Exit with Specific Code

```sh
if [ ! -f config.yaml ]; then
  echo "Missing config"
  exit 2
fi
```

### `set -e` – stop on error

```sh
#!/bin/bash
set -e  # Script stops if any command fails
```

---

Let me know if you'd like this as a downloadable `.md` file or formatted PDF.
