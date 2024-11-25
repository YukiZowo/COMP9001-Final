# Regular Expressions 正则表达式

## 1. 什么是正则表达式？
正则表达式（Regular Expression）是一种用于匹配文本中字符模式的工具。通过定义特定的模式，正则表达式可以用于搜索、替换和处理文本。

## 2. 基础语法

### 2.1 匹配单个字符
正则表达式可以用来查找文本中的某个字符或一组字符。例如，想要匹配单词“hello”或“Hello”，可以使用以下的正则表达式：
```regex
[Hh]ello
```
- **说明**：方括号 `[]` 内的字符表示任意一个匹配，例如 `[Hh]` 匹配 'H' 或 'h'。这样可以通过一次搜索匹配两种不同的情况。

### 2.2 匹配字母范围
要查找任意字母字符，可以使用字母范围的正则表达式：
```regex
[a-z]
```
- **说明**：`[a-z]` 表示匹配任意小写字母，减号（`-`）表示一个范围。

### 2.3 匹配任意字符
可以使用单个点（`.`）来匹配任意字符。
- **示例**：
  ```regex
  Hello.world
  ```
  这个正则表达式会匹配以下字符串：
  - `Hello world`
  - `Hello-world`
  - `Hello/world`
  - `Helloworld`

### 2.4 匹配特殊字符
如果需要匹配特殊字符，比如点号 `.`，则需要使用反斜杠进行转义：
```regex
\.
```
- **说明**：反斜杠 `\` 表示对其后的字符进行转义，例如 `\.` 表示匹配点字符。

### 2.5 开头与结尾匹配
- **开头匹配**：使用 `^` 符号来匹配以特定字符开头的行。
  ```regex
  ^Hello
  ```
  - **说明**：匹配以 `Hello` 开头的行。
- **结尾匹配**：使用 `$` 符号来匹配以特定字符结尾的行。
  ```regex
  goodbye$
  ```
  - **说明**：匹配以 `goodbye` 结尾的行。

### 2.6 重复匹配符号

- `*`：匹配前面的字符 0 次或多次。
  ```regex
  a*b
  ```
  - **说明**：匹配 'b'、'ab'、'aab' 等。
- `+`：匹配前面的字符 1 次或多次。
  ```regex
  a+b
  ```
  - **说明**：匹配 'ab'、'aab'、'aaab' 等。
- `?`：匹配前面的字符 0 次或 1 次。
  ```regex
  colou?r
  ```
  - **说明**：匹配 'color' 或 'colour'。
- `{n}`：匹配前面的字符恰好 n 次。
  ```regex
  a{3}
  ```
  - **说明**：匹配 'aaa'。
- `{n,}`：匹配前面的字符至少 n 次。
  ```regex
  a{2,}
  ```
  - **说明**：匹配 'aa'、'aaa'、'aaaa' 等。
- `{n,m}`：匹配前面的字符至少 n 次，至多 m 次。
  ```regex
  a{1,3}
  ```
  - **说明**：匹配 'a'、'aa' 或 'aaa'。

## 3. 使用 Python 中的正则表达式
在 Python 中，可以使用 `re` 模块来处理正则表达式。

### 3.1 导入 `re` 模块
```python
import re
```

### 3.2 示例：匹配以特定单词开头的行
```python
import re

for line in open("mytext"):
    if re.search("^The", line):
        print(line)
```
- **说明**：上面的代码会打印出文件 `mytext` 中以 `The` 开头的所有行。

## 4. 常见正则表达式代码
| 代码 | 匹配       |
|------|------------|
| `\d`  | 任意数字    |
| `\D`  | 任意非数字  |
| `\w`  | 任意字母或数字或下划线 |
| `\W`  | 任意非字母、数字、下划线 |
| `\s`  | 任意空白字符 |
| `\S`  | 任意非空白字符 |

## 5. 分组匹配
正则表达式的一个非常有用的特性是分组（group）。使用括号 `()` 来对正则表达式进行分组，可以将匹配的子模式捕获为一个组，并在程序中查看匹配的内容。

### 5.1 示例：匹配包含特定模式的文本
```regex
([Tt]he).*(house called \w*)
```
- **说明**：
  - `([Tt]he)` 匹配 `The` 或 `the`，这是第一个分组。
  - `.*` 表示任意数量的任意字符。
  - `(house called \w*)` 匹配单词 `house called`，后面跟着一个或多个字母，这是第二个分组。

### 5.2 在 Python 中使用分组
```python
import re

pattern = r'([Tt]he).*(house called \w*)'
text = "The big house called mansion"
match = re.search(pattern, text)
if match:
    print(match.group(1))  # 输出: The
    print(match.group(2))  # 输出: house called mansion
```

### 5.3 命名分组
可以为分组显式命名，而不是使用数字。
```regex
([Tt]he).*(?P<main>house called \w*)
```
- **说明**：`(?P<main>...)` 表示给分组起名为 `main`，可以在程序中通过名字引用。
```python
import re

pattern = r'([Tt]he).*(?P<main>house called \w*)'
text = "The big house called mansion"
match = re.search(pattern, text)
if match:
    print(match.group('main'))  # 输出: house called mansion
```

## 6. 匹配括号字符
如果想匹配括号字符 `(` 或 `)`，可以使用反斜杠进行转义：
```regex
\(
```
- **说明**：例如，`\(` 会匹配左括号字符。

---

## 7. Regex 基础练习

这里有一些练习可以帮助你练习使用正则表达式和 Python 的 `re` 模块。

### 练习 1: 匹配大小写不敏感的单词
**Exercise 1: Matching Case-Insensitive Words**

编写一个 Python 程序，读取文件 `python.txt` 并打印所有包含单词 "python" 或 "Python" 的行（大小写不敏感匹配）。使用正则表达式匹配这两种形式。  
Write a Python program that reads from `python.txt` and prints all lines that contain the word "python" or "Python" (case-insensitive match). Use a regular expression to match both forms of the word.

**Example:**

**Input file:**
```
I am learning Python.
python is powerful.
This is just some text.
```
**Expected Output:**
```
I am learning Python.
python is powerful.
```

**解答**：
```python
import re

with open('python.txt', 'r') as file:
    for line in file:
        if re.search(r'(?i)python', line):
            print(line.strip())
```
- **说明**：`(?i)` 用于启用不区分大小写的匹配。

### 练习 2: 匹配包含句点的单词
**Exercise 2: Matching Words with Periods**

编写一个 Python 程序，查找并打印文件 `dots.txt` 中包含单词 "hello.world" 的所有行，其中句点（`.`）被视为字面字符而不是通配符。  
Write a Python program that finds and prints all lines from `dots.txt` that contain the word "hello.world" where the dot (.) is treated as a literal character and not as a wildcard.

**Example:**

**Input file:**
```
hello.world is amazing.
hello world is different.
```
**Expected Output:**
```
hello.world is amazing.
```

**解答**：
```python
import re

with open('dots.txt', 'r') as file:
    for line in file:
        if re.search(r'hello\.world', line):
            print(line.strip())
```
- **说明**：使用 `\.` 来匹配句点字符，而不是将其作为通配符。

### 练习 3: 匹配以特定单词结尾的行
**Exercise 3: Matching Lines That End with a Specific Word**

编写一个 Python 程序，打印文件 `done.txt` 中以单词 "done" 结尾的所有行（区分大小写）。  
Write a Python program that prints all lines that end with the word "done" (case-sensitive match) from the file `done.txt`.

**Example:**

**Input file:**
```
I am done.
Finally done
The task is done
I will finish soon.
```
**Expected Output:**
```
Finally done
The task is done
```

**解答**：
```python
import re

with open('done.txt', 'r') as file:
    for line in file:
        if re.search(r'done$', line):
            print(line.strip())
```
- **说明**：`$` 用于匹配行尾，因此 `done$` 匹配以 `done` 结尾的行。



## 8. Regex 高级练习

### 练习 1: 查找包含非数字的行
**Exercise 1: Find Lines Containing Non-Digits**

编写一个 Python 程序，读取文件 `mix.txt`，并打印包含任何非数字字符的行。
Write a Python program that reads from a file (`mix.txt`) and prints lines that contain any character other than digits.

**Example:**

**Input file:**
```
12345
67890
Hello123
Welcome to 2023!
999
```
**Expected Output:**
```
Hello123
Welcome to 2023!
```

**解答**：
```python
import re

with open('mix.txt', 'r') as file:
    for line in file:
        if re.search(r'\D', line):
            print(line.strip())
```
- **说明**：`\D` 表示匹配任意非数字字符。

### 练习 2: 提取字母数字单词
**Exercise 2: Match Alphanumeric Words**

编写一个 Python 程序，读取文件并提取所有字母数字单词。
Write a Python program to read a file and extract all alphanumeric words.

**Example:**

**Input file:**
```
Hello, world! This is 2024.
Welcome_to the future?
Regex is fun, right?
```
**Expected Output:**
```
['Hello', 'world', 'This', 'is', '2024']
['Welcome', 'to', 'the', 'future']
['Regex', 'is', 'fun', 'right']
```

**解答**：
```python
import re

with open('input.txt', 'r') as file:
    for line in file:
        words = re.findall(r'\b\w+\b', line)
        print(words)
```
- **说明**：`\b` 表示单词边界，`\w+` 表示匹配一个或多个字母、数字或下划线。

### 练习 3: 使用分组提取并打印匹配的单词
**Exercise 3: Extract and Print Words Matching Different Patterns Using Groups**

编写一个程序，使用正则表达式分组来匹配包含以下内容的行：
- 一个名字（以大写字母开头）。
- 一个年龄（两位数的数字）。
- 一个地点（以大写字母开头的单词）。

Write a program that uses regular expression groups to match lines that contain:
- A name (which starts with a capital letter).
- An age (which is a two-digit number).
- A location (a word that starts with a capital letter).

**Example:**

**Input file:**
```
Alice 25 lives in Paris
Bob 30 lives in New York
Charlie 28 lives in London
Diana 32 lives in Tokyo
```
**Expected Output:**
```
Name: Alice, Age: 25, Location: Paris
Name: Bob, Age: 30, Location: New York
Name: Charlie, Age: 28, Location: London
Name: Diana, Age: 32, Location: Tokyo
```

**解答**：
```python
import re

pattern = r'(?P<name>[A-Z][a-z]+) (?P<age>\d{2}) lives in (?P<location>[A-Z][a-zA-Z]*)'

with open('input.txt', 'r') as file:
    for line in file:
        match = re.search(pattern, line)
        if match:
            name = match.group('name')
            age = match.group('age')
            location = match.group('location')
            print(f'Name: {name}, Age: {age}, Location: {location}')
```
- **说明**：使用命名分组 `(?P<name>...)` 来提取名字、年龄和地点。

---


