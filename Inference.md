# Linux Command Line Assignment

## 1. Directory Navigation and Basic Operations

**mkdir ev4** * **Inference:** This creates a new directory named `ev4` in the current working path. The `mkdir` command is the standard way to initialize new folders in the Linux filesystem.

**cd ev4** * **Inference:** Changes the shell's focus into the `ev4` folder. All subsequent relative commands will now occur inside this directory.

**mkdir 47** * **Inference:** Creates a sub-directory named `47` (my roll number) inside `ev4`. This demonstrates how to build a nested directory hierarchy.

**cd 47** * **Inference:** Navigates into the folder named `47`. This is now my deepest working level in this assignment.

**pwd** * **Result:** `/home/nihal/ev4/47`  
* **Inference:** The **Print Working Directory** command provides the absolute path from the root `/` down to my current location. It is essential for verifying exactly where you are in the system tree.

**cd -** * **Result:** `/home/nihal/ev4`  
* **Inference:** The hyphen `-` acts as a toggle. It moves the user back to the *previous* directory they were in before the last `cd` command.

**cd -** * **Result:** `/home/nihal/ev4/47`  
* **Inference:** Using the toggle again brings me back to where I started. This is highly efficient for jumping between two specific folders without typing long paths.

**cd .** * **Result:** `/home/nihal/ev4/47`  
* **Inference:** The single dot `.` refers to the "current directory." Navigating into `.` does nothing, but it is a fundamental concept used when running local scripts or moving files to your current spot.

**cd ..** * **Result:** `/home/nihal/ev4`  
* **Inference:** The double dot `..` refers to the "parent directory." This moves the user one level up in the hierarchy.

**cd ~** * **Result:** `/home/nihal`  
* **Inference:** The tilde `~` is a shortcut for the current user's **Home** directory. This is the private space where the user has full permissions.

**cd /** * **Result:** `/`  
* **Inference:** This moves the user to the **Root** directory, the absolute base of the Linux filesystem containing system configuration, binaries, and libraries.

**ls -l** * **Inference:** This performs a "long listing." It displays not just names, but file permissions, owners, groups, file size, and the last modified timestamp.

**cd media** * **Result:** `/media`  
* **Inference:** Since I am already at the root `/`, I can enter `media` using a relative path. This directory is typically used for mounting external drives like USBs.

**cd** * **Result:** `/home/nihal`  
* **Inference:** Using `cd` with no arguments is the fastest way to return to your **Home** directory from anywhere in the system.

**pwd** * **Result:** `/home/nihal`  
* **Inference:** Confirms that the bare `cd` command successfully returned the shell to the home path.

**cd media** * **Result:** `Error: No such file or directory`  
* **Inference:** This fails because the shell is looking for a folder named `media` *inside* my home folder. Relative paths only work if the folder exists within the current directory.

**cd /media** * **Result:** `/media`  
* **Inference:** This succeeds because it uses an **absolute path**. Starting with a `/` tells the system to start looking from the Root, regardless of where the user currently is.

**ls -l** * **Inference:** Lists the contents of the system's media mount points with full metadata.

**ls -al** * **Inference:** The `-a` flag stands for "all." This displays hidden files (those starting with a dot), such as `.bashrc` or `.profile`, which are hidden in a standard `ls`.

---

## 2. File and Directory Management

**cd ~/ev4/47** * **Inference:** Combines the home shortcut `~` with a specific path to jump directly to the target folder in one step.

**mkdir emptydummy** * **Inference:** Creates a directory named `emptydummy`.

**mkdir dummy** * **Inference:** Creates another directory named `dummy`.

**cd dummy** * **Inference:** Navigates into the `dummy` folder to begin file operations.

**touch file1** **touch file2** * **Inference:** The `touch` command creates empty files if they don't exist, or updates the timestamp if they do. Here, it initializes two new blank files.

**ls -l** * **Inference:** Confirms the creation of `file1` and `file2`.

**rm -i file2** * **Inference:** The `-i` flag stands for **interactive**. The system will pause and ask "remove regular empty file 'file2'?" before proceeding. This is a safety measure to prevent accidental deletion.

**ls -l** * **Inference:** Confirms that `file2` has been permanently deleted.

**cd ..** * **Inference:** Moves back to the `47` directory.

**rm emptydummy** * **Result:** `Error: Is a directory`  
* **Inference:** By default, `rm` only works on files. It refuses to delete a directory unless the recursive flag is used.

**rmdir emptydummy** * **Inference:** `rmdir` is a specialized command that **only** removes empty directories. It is safer than `rm -r` because it won't delete data by mistake.

**rmdir dummy** * **Result:** `Error: Directory not empty`  
* **Inference:** `rmdir` fails here because `dummy` still contains `file1`. This confirms that `rmdir` protects against accidental loss of files.

**rm -r dummy** * **Inference:** The `-r` (recursive) flag tells the system to enter the directory and delete everything inside it first, then delete the directory itself.

---

## 3. Creating and Manipulating File Content

**cat >file1.txt** (Input: "My first line", CTRL+D)  
* **Inference:** The `>` operator redirects the terminal's standard input into the file. `cat` captures what I type until I signal the end of the file with `CTRL+D`.

**cat >file2.txt** (Input: "Hello Second line", CTRL+D)  
* **Inference:** Creates a second file with the specified text content.

**cat >file3.txt** (Input: "Hello line", CTRL+D)  
* **Inference:** Creates a third file for testing append and merge operations.

**cat file1.txt file2.txt > file_combined.txt** * **Inference:** `cat` reads the contents of both files in order, and the `>` operator pipes that combined text into a new file named `file_combined.txt`. If the file already existed, it would be overwritten.

**cat file_combined.txt** * **Inference:** Displays the result of the merger. Tab-completion (typing `file_c` + Tab) is a shell feature that saves time and prevents spelling errors.

**cat file3.txt >> file_combined.txt** * **Inference:** The `>>` operator is for **appending**. Instead of replacing the contents of `file_combined.txt`, it adds the text from `file3.txt` to the very bottom of the existing content.

**cat file_combined.txt** * **Inference:** Shows that the file now contains all three lines from the previous files.

**grep -i hello file*** * **Inference:** `grep` is a powerful search tool. The `-i` flag makes the search case-insensitive, and `file*` tells it to search every file in the directory that starts with the word "file".

**cp file1.txt ~/ev4** * **Inference:** Creates a duplicate of `file1.txt` and places it one level up in the `ev4` folder. The original file remains in the current folder.

**mv file_combined.txt combined** * **Inference:** The `mv` command is used for both moving and renaming. Since no new path is specified, it simply renames `file_combined.txt` to `combined`.

---

## 4. File Permissions (Chmod)



**chmod u+x combined** * **Inference:** Grants **Execute** (`x`) permission to the **User** (`u`). This allows the owner to run the file as a program or script.

**chmod g-r combined** * **Inference:** Removes **Read** (`r`) permission from the **Group** (`g`). Now, other users in the same group cannot view the content of this file.

**chmod 777 combined** * **Inference:** Sets the most permissive state possible. In octal, `7` is the sum of $4 (read) + 2 (write) + 1 (execute)$. Applying `777` gives full control (rwxrwxrwx) to the User, Group, and all others.

---

## 5. User Management and Messaging

**sudo useradd alice** * **Inference:** Adds a new user account named `alice` to the system. `sudo` is required because modifying the user database (`/etc/passwd`) is a restricted administrative action.

**sudo passwd alice** * **Inference:** Prompts the administrator to set or change the login password for the user `alice`.

**sudo userdel alice** * **Inference:** Removes the user `alice` from the system.

**write alice** * **Inference:** This is an internal communication tool. If `alice` is logged into another terminal session on the same server, this command opens a direct text pipe to her screen for real-time "chatting."

**mesg y / mesg n** * **Inference:** These controls permission for the `write` command. `mesg y` allows others to send you messages, while `mesg n` blocks them to prevent interruptions.
