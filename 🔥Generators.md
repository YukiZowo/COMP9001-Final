# Python Generators 详解

## 1. 什么是 Generator？
Generator 是一种特殊的迭代器，用于以惰性方式（lazy evaluation）生成序列中的值。Generator 可以通过函数使用 `yield` 关键字来定义。它们提供了一种节省内存的方法来生成大规模的数据，而不是一次性将所有数据保存在内存中。

## 2. 定义 Generator
Generator 是通过包含 `yield` 语句的函数来定义的。每次调用 `yield` 时，函数的执行状态会被冻结，直到下次迭代继续。

### 2.1 使用 `yield` 定义 Generator
```python
# 定义一个简单的 generator
def countdown(n):
    print("Countdown from", n)
    while n > 0:
        yield n
        n -= 1

# 使用 generator
fun = countdown(5)
print(next(fun))  # 输出: Countdown from 5 \n 5
print(next(fun))  # 输出: 4
```
- **说明**：`countdown` 是一个 generator，每次调用 `yield` 时都会返回当前的计数值并暂停执行，直到下次调用 `next()` 时继续执行。
- **输出**：
  ```
  Countdown from 5
  5
  4
  3
  2
  1
  ```
- 当函数遇到 `yield` 时，会冻结当前状态，并在下次调用 `next()` 时继续执行。Generator 可以反复启动直到执行结束。

### 2.2 与普通函数的区别
- 普通函数使用 `return` 语句来返回结果，一旦返回，函数的执行结束。
- Generator 使用 `yield`，每次 `yield` 都会暂停函数的执行并返回值，但不会结束函数，直到没有更多的值可生成。
- Generator 可以像“活着”的函数对象一样被多次调用。

## 3. Generator 表达式
Generator 表达式与列表推导式相似，但它们使用小括号 `()` 而不是方括号 `[]`，并且不会一次性生成所有元素，而是逐个生成。

### 3.1 语法
```python
# 使用 generator 表达式生成一个数值的平方序列
squares = (x * x for x in range(5))
for square in squares:
    print(square)
```
- **说明**：`(x * x for x in range(5))` 是一个 generator 表达式，它按需逐个生成平方值。
- **输出**：
  ```
  0
  1
  4
  9
  16
  ```

## 4. Generator 的优点
- **节省内存**：Generator 不会一次性将所有元素存入内存，而是按需生成值，非常适合处理大数据量。
- **惰性求值**：Generator 在需要时才生成元素，避免了不必要的计算。

## 5. 常用场景
- **大数据处理**：当数据量很大，无法一次性加载到内存时，Generator 是非常合适的选择。
- **流数据处理**：例如从网络流、日志文件中按行读取数据。

### 5.1 示例：读取大文件
```python
def read_large_file(file_path):
    with open(file_path, 'r') as file:
        for line in file:
            yield line

# 使用 generator 读取大文件
for line in read_large_file('large_file.txt'):
    print(line.strip())
```
- **说明**：`read_large_file` 是一个 generator，用于逐行读取大文件。这种方式避免了一次性将整个文件加载到内存中。

## 6. `yield from` 语法
`yield from` 是 Python 3.3 引入的一种简化生成器代码的语法，用于从子迭代器中生成值。

### 6.1 示例
```python
def generator_a():
    yield 1
    yield 2

# 使用 yield from 引用子生成器
def generator_b():
    yield from generator_a()
    yield 3

for value in generator_b():
    print(value)
```
- **说明**：`yield from generator_a()` 将子生成器 `generator_a` 中的所有值生成出来。
- **输出**：
  ```
  1
  2
  3
  ```

## 7. Generator 的内置函数
- **`next()`**：用于获取 generator 的下一个值。
  ```python
  gen = countdown(3)
  print(next(gen))  # 输出: Countdown from 3 \n 3
  print(next(gen))  # 输出: 2
  ```
- **`iter()`**：将可迭代对象转换为迭代器（包括 generator）。

## 8. Generator 的其他特性
- **协程（Coroutine）**：Generator 在技术上也被称为“协程”（co-routine），可以用来在特定时间点暂停执行，然后继续。
- **与 for 循环结合使用**：Generator 本质上是“迭代器”，可以直接在 `for` 循环中使用。
  ```python
  for n in countdown(6):
      print(n)
  ```
  - **说明**：在 `for` 循环中，generator 会自动调用 `next()`，直到所有值都被生成。

## 9. 简单生成器的另一种形式
除了使用 `yield` 关键字定义生成器外，还可以通过类似列表推导式的方式创建生成器对象。

### 9.1 示例
```python
# 从日志文件中提取字段的生成器
def extract_field():
    field = (line.rsplit(None, 1)[1] for line in open("apache.log"))
    for value in field:
        print(value)
```
- **说明**：在上面的代码中，`field` 是一个 generator 表达式，用于提取日志文件的最后一个字段。生成器对象可以用作迭代器，用于简化循环任务。

## 10. Generator 练习题

### 10.1 Task 1: Square Numbers Generator
编写一个名为 `square_numbers` 的生成器函数，该函数接收一个数字 `n`，并生成从 1 到 `n` 的每个数字的平方。  
Write a generator function called square_numbers that takes a number n and yields the square of each number from 1 to n.

#### 示例
```python
def square_numbers(n):
    for i in range(1, n + 1):
        yield i * i

# 使用示例
for square in square_numbers(5):
    print(square)
```
**输出**：
```
1
4
9
16
25
```

### 10.2 Task 2: Word Lengths Generator
创建一个名为 `word_lengths` 的生成器函数，该函数接收一个单词列表，并生成每个单词的长度。  
Create a generator function called word_lengths that takes a list of words and yields the length of each word.

#### 示例
```python
def word_lengths(words):
    for word in words:
        yield len(word)

# 使用示例
words = ["apple", "banana", "kiwi", "grapefruit"]
for length in word_lengths(words):
    print(length)
```
**输出**：
```
5
6
4
10
```

### 10.3 Task 3: Even Number Generator
使用生成器表达式生成从 1 到 100 的所有偶数。  
For this task, we'll use a *generator expression* to generate even numbers from 1 to 100.

#### 示例
```python
# 生成从 1 到 100 的偶数的生成器表达式
even_gen = (x for x in range(1, 101) if x % 2 == 0)

# 使用示例
for even in even_gen:
    print(even)
```
**输出**：
```
2
4
6
8
10
12
...
100
```

---
