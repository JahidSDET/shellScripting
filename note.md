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


Sure! Here's the **updated short note** with **examples added to the system info table**:

---

### 🕒 **Cron Job (Scheduled Tasks)**

**Cron** is used to schedule scripts or commands to run automatically at specific times.

**Syntax (`crontab -e`):**

```
* * * * * /path/to/command
│ │ │ │ │
│ │ │ │ └─ Day of week (0-6, Sun=0)
│ │ │ └─── Month (1-12)
│ │ └───── Day of month (1-31)
│ └─────── Hour (0-23)
└───────── Minute (0-59)
```

**Examples:**

* `0 9 * * * /home/user/backup.sh`
  ➤ Run backup every day at **9 AM**
* `*/15 * * * * /home/user/ping_check.sh`
  ➤ Run ping check **every 15 minutes**
* `@reboot /home/user/startup_task.sh`
  ➤ Run script **at system startup**

---

### 🖥️ **System Information Commands**

| Purpose         | Command               | Example Output (Sample)               |
| --------------- | --------------------- | ------------------------------------- |
| System uptime   | `uptime`              | `12:01 up 3 days, 4:23, 3 users`      |
| Kernel version  | `uname -r`            | `5.15.0-91-generic`                   |
| OS info         | `cat /etc/os-release` | `Ubuntu 22.04.4 LTS`                  |
| Disk usage      | `df -h`               | `/dev/sda1  40G  20G  18G  54% /`     |
| Memory usage    | `free -h`             | `Mem: 7.6G used, 8.2G total`          |
| CPU info        | `lscpu`               | `Intel i7 @ 2.60GHz, 8 cores`         |
| Logged-in users | `who`                 | `user  tty1  Jul 2 08:10`             |
| Top processes   | `top` or `htop`       | Interactive table of CPU/memory usage |
| IP Address      | `hostname -I`         | `192.168.1.100`                       |

---

Let me know if you'd like to turn this into a PDF cheat sheet or add more admin tools (like `journalctl`, `systemctl`, etc.).

