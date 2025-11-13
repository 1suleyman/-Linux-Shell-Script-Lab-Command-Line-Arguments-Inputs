# 🧮 Linux Shell Script Lab – Command Line Arguments & Inputs

In this lab, I learned how to **pass dynamic values into Bash scripts using command-line arguments** (`$1`, `$2`, etc.).
The focus was on replacing hard-coded values with variables, debugging parameter order, and making scripts more reusable for real-world DevOps automation.

---

## 📋 Lab Overview

**Goal:**

* Replace static variables with **command-line parameters**
* Understand positional variables (`$1`, `$2`, …)
* Debug and fix scripts to accept external inputs
* Improve flexibility and reusability of shell scripts

**Learning Outcomes:**

* Use `$1`, `$2`, etc. to capture command-line arguments
* Build scripts that respond dynamically to user input
* Debug variable substitution and command order
* Understand how argument count affects script behavior

---

## 🛠 Step-by-Step Journey

### Step 1 — Update the Rocket Script to Use a Command-Line Argument

Script path: `/home/bob/create-and-launch-rocket`

**Original (static):**

```bash
mission_name=luna-mission
```

**Fixed:**

```bash
mission_name=$1
```

✅ `$1` now captures the first argument passed when the script is executed, e.g.:

```bash
bash create-and-launch-rocket mars-mission
```

→ launches the *Mars Mission* dynamically.

---

### Step 2 — Inspect `print-capital.sh`

Running the script:

```bash
bash /home/bob/print-capital.sh
```

Output:

```
Capital city of UK is London
```

✅ Confirmed that the original script prints a static message.

---

### Step 3 — Update Script to Accept Two Arguments

Modified `/home/bob/print-capital.sh` to accept both **country** and **capital** as command-line arguments.

**Original:**

```bash
echo "Capital city of UK is London"
```

**Fixed:**

```bash
echo "Capital city of $1 is $2"
```

✅ Test:

```bash
bash print-capital.sh Nigeria Abuja
```

Output:

```
Capital city of Nigeria is Abuja
```

---

### Step 4 — Fix `backup-file.sh` to Use a Command-Line Argument

**Goal:** Allow the file name to be passed dynamically.

Script path: `/home/bob/backup-file.sh`

**Original:**

```bash
file_name="some-file"
cp $file_name ${file_name}_bkp
```

**Fixed:**

```bash
set -e
file_name=$1
cp $file_name ${file_name}_bkp
echo "Done"
```

✅ Test:

```bash
bash backup-file.sh create-and-launch-rocket
```

→ Successfully creates `create-and-launch-rocket_bkp`.

---

### Step 5 — Identify How Many Arguments `update_shell.sh` Uses

Opened `/home/bob/update_shell.sh` in `vi` and found:

```bash
$1
$2
```

✅ The script uses **two command-line arguments**.

---

### Step 6 — Debug and Fix `update_shell.sh`

**Original (broken):**

```bash
new_shell="$2"
username_name="$1"
usermod -s $user_name $new_shell
```

**Issues:**

* Variable order reversed in `usermod` command.
* Incorrect variable name used (`user_name` instead of `username_name`).
* Quotation marks not needed around variable assignment.

**Fixed:**

```bash
username_name=$1
new_shell=$2
usermod -s $new_shell $username_name
```

✅ The script now correctly updates a user’s shell and home directory when valid inputs are provided.

---

## 🧠 Key Concepts Reinforced

| Concept                   | Description                                                                   |
| ------------------------- | ----------------------------------------------------------------------------- |
| **Positional parameters** | `$1`, `$2`, etc. represent command-line arguments in the order they’re passed |
| **Dynamic variables**     | Replace hard-coded values to make scripts reusable                            |
| **Argument count**        | Number of arguments determines script behavior                                |
| **Variable order**        | Always maintain correct parameter order in system commands                    |
| **Testing scripts**       | Use `bash scriptname arg1 arg2` to verify argument handling                   |

---

## 🧩 Common Mistakes & Fixes

| ❌ Mistake                                     | ✅ Fix                                  |
| --------------------------------------------- | -------------------------------------- |
| `mission_name=luna-mission`                   | `mission_name=$1`                      |
| Hard-coded `UK` and `London`                  | `echo "Capital city of $1 is $2"`      |
| `file_name="some-file"`                       | `file_name=$1`                         |
| Misordered `usermod -s $user_name $new_shell` | `usermod -s $new_shell $username_name` |

---

## 💡 Notes / Tips

* Use **positional arguments** for flexibility when automating similar tasks.
* Always **validate** inputs before running system-level commands like `usermod`.
* Remember: `$0` is the script name, `$1`–`$9` are arguments.
* Test with sample data to ensure variables expand as expected.
* For more complex scripts, consider adding `"$@"` or `"$#"` to handle multiple arguments or count them dynamically.

---

## ✅ Summary Commands

| Task                 | Command                                 |
| -------------------- | --------------------------------------- |
| Edit script          | `vi /home/bob/create-and-launch-rocket` |
| Save & exit          | `:wq`                                   |
| Run with 1 arg       | `bash script.sh arg1`                   |
| Run with 2 args      | `bash script.sh arg1 arg2`              |
| Check argument count | `echo $#`                               |
| Print all args       | `echo $@`                               |

---

### 🏁 End of Lab

Successfully updated multiple scripts to accept **command-line inputs** instead of fixed values.
✅ Learned positional parameters `$1`, `$2`
✅ Replaced static variables with dynamic arguments
✅ Fixed parameter ordering and syntax in real-world scenarios

This lab deepened understanding of **input handling and script reusability** — key skills for **automation-ready DevOps scripting**.
