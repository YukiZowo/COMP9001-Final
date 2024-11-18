# Shell Script 介绍

## 1. 什么是 Shell Script？

Shell 脚本是一种将一组 Shell 命令放在一个文件中并通过输入该文件的名称来运行它们的方式。它介绍了我们通常称为 Shell 编程的概念。

Shell 命令是存储在诸如 `/bin` 或 `/usr/bin` 等标准目录中的程序。

## 2. Shell 编程概念

大多数人认为 Shell 是一个命令界面，例如，我们可以输入类似 `cat myprog.py` 的命令来列出程序的文本内容。

Shell 命令是程序，这些程序的文件存储在标准目录中，比如 `/bin` 或 `/usr/bin`。

### 2.1 查看 `/bin` 目录中的命令

```shell
$ ls /bin
[         echo      mkdir     stty
bash      ed        mv        sync
cat       expr      pax       tcsh
chmod     hostname  ps        test
cp        kill      pwd       unlink
csh       ksh       realpath  wait4path
dash      launchctl rm        zsh
date      link      rmdir
```
- **说明**：这是存储在 `/bin` 目录中的文件列表，每个文件都包含一个可以执行的程序。例如，可以看到 `ls` 程序文件。

## 3. 运行命令的过程

当你键入一个命令时，Shell 程序会在这些目录中搜索与命令对应的程序文件。一旦找到文件，它就会运行程序。

如果找不到文件，它会显示错误信息。

### 3.1 错误示例

```shell
$ lls
-bash: lls: command not found
```

## 4. 使用 `which` 命令查找程序位置

`which` 命令可以显示命令文件的存储位置。例如：

```shell
$ which ls
/bin/ls
```

## 5. Shell 脚本的优势

Shell 的一个非常有用的方面是我们可以将一组命令放入一个文本文件中。例如，文件 `mycommands.sh` 可以包含如下命令：

```shell
$ cat mycommands.sh
echo "Files:"
ls
```

我们可以通过从文件中读取所有命令来让 Shell 按顺序运行它们。

### 5.1 运行 Shell 脚本

可以通过显式启动 Shell 程序并将文件名作为参数来运行文件中的命令：

```shell
$ bash mycommands.sh
Files:
mycommands.sh
```

## 6. Shell 脚本的扩展名

通常我们在文件上使用 `.sh` 扩展名来表示它包含 Shell 命令。这不是严格要求的，但可以用来提醒自己它包含 Shell 命令。

## 7. 不同的 Shell 程序

有许多不同的 Shell 程序可用。在上面的例子中，我使用的是叫做 `bash` 的 Shell（它的全称是 Bourne Again Shell，以一位名为 Steve Bourne 的 Shell 作者命名）。

Shell 中有许多特性可以用于存储在文件中的一系列 Shell 命令。

---

希望这些关于 Shell Script 的介绍能够帮助你理解并开始编写 Shell 脚本。如果你有任何问题或需要更多的例子，随时告诉我！


## 8. 练习题目：简单 Bash 脚本与命令标志

### 练习 1: 简单的 Bash 脚本 (Simple Bash Script)

**Task Description**:
Write a simple bash script `my_script.sh` which, when executed, will:
- output "This is my script!"
- create a new directory called `new_dir`
- create a file inside `new_dir` called `new_file.txt`
- write "WRITTEN IN THE FILE" to the file
  - this can be achieved by piping the output of a command to a file with `commandname "TEXT" > path/to/file.txt`
- list the contents of the current directory
- view the contents of `new_dir/new_file.txt`

You may use the following bash commands: `echo`, `mkdir`, `touch`, `ls`, `cat`.

**题目描述**：
编写一个简单的 Bash 脚本 `my_script.sh`，当它执行时，将会：
- 输出 "This is my script!"
- 创建一个名为 `new_dir` 的新目录
- 在 `new_dir` 中创建一个名为 `new_file.txt` 的文件
- 将 "WRITTEN IN THE FILE" 写入到该文件中
  - 可以通过使用命令的输出重定向到文件的方式实现，例如 `commandname "TEXT" > path/to/file.txt`
- 列出当前目录的内容
- 查看 `new_dir/new_file.txt` 的内容

可以使用以下 bash 命令：`echo`，`mkdir`，`touch`，`ls`，`cat`。

**答案**：
```bash
#!/bin/bash

# 输出信息 (Output message)
echo "This is my script!"

# 创建新目录 (Create a new directory)
mkdir new_dir

# 创建新文件 (Create a new file)
touch new_dir/new_file.txt

# 将内容写入文件 (Write to the file)
echo "WRITTEN IN THE FILE" > new_dir/new_file.txt

# 列出当前目录的内容 (List the contents of the current directory)
ls

# 查看新文件的内容 (View the contents of new_file.txt)
cat new_dir/new_file.txt
```
- **考点**：理解基本的 Bash 命令和如何将多个命令组合到一个脚本中。

### 练习 2: 使用标志 (Using Flags)

**Task Description**:
Bash commands can take arguments. For example, the `echo` command can take a string to output.

Some arguments can be "flags", which set options for the command. For example, calling `ls -l` prints the output of `ls` in the "long" format, showing more details for each file such as file size, time created, etc.

You can find out more about available flags for different commands by reading the Linux manual page for a given command. From the terminal, to read the manual page for `ls`, simply run `man ls` and use the keyboard arrows to navigate up/down. You can press `q` to quit and go back to the terminal.

Your task is to:
1. Open a terminal session in Ed (using the >_ symbol on the top-right corner of this slide).
2. Run the `ls -lrt` command (three flags `l`, `r`, `t`) and view its output.
3. Read the manual page for `ls` (accessed via `man ls`) to find out what the flags do.
4. What additional flag would you have to use to make the output human readable (i.e. such that file sizes are printed as `412K` instead of `421688`, for example)?

**题目描述**：
Bash 命令可以接受参数。例如，`echo` 命令可以接受一个要输出的字符串。

一些参数可以是“标志（flags）”，用于为命令设置选项。例如，调用 `ls -l` 会以“长”格式打印 `ls` 的输出，显示每个文件的更多详细信息，例如文件大小、创建时间等。

你可以通过阅读给定命令的 Linux 手册页了解更多可用标志。在终端中，要读取 `ls` 的手册页，只需运行 `man ls`，并使用键盘箭头上下导航。你可以按 `q` 退出并返回终端。

你的任务是：
1. 在 Ed 中打开一个终端会话（使用此幻灯片右上角的 >_ 符号）。
2. 运行 `ls -lrt` 命令（包含三个标志 `l`，`r`，`t`），查看其输出。
3. 阅读 `ls` 的手册页（通过 `man ls` 访问），找出这些标志的作用。
4. 你需要使用什么额外的标志使输出对人类更加友好（例如，使文件大小以 `412K` 而不是 `421688` 的形式打印）？

**答案**：
1. `ls -lrt` 命令使用了三个标志：
   - `-l`：以详细格式显示。
   - `-r`：逆序排列。
   - `-t`：按修改时间排序。
2. 要使输出对人类更加友好，可以使用标志 `-h`（即 `ls -lh`），使文件大小以更易读的格式显示，例如 `K`、`M`。
- **考点**：理解如何使用标志来修改命令的行为，以及如何查找命令的详细信息（手册页）。

