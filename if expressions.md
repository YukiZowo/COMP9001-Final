# Python if expression 详解

## 1. 什么是 if expression （if 表达式）？

`if` 语句是 Python 程序中非常常见的一种语句，用于检查某个条件是否成立，然后根据条件的结果执行不同的代码块。`if` 语句可以在条件为 `True` 时执行一段代码，或者在条件为 `False` 时执行另一段代码。

不过，在 Python 中，我们还可以将 `if` 语句作为一个表达式来使用，这样可以使代码更加简洁。

## 2. 常规的 if 语句

下面是一个常规的 `if` 语句的例子：

```python
if (a % 2) == 0:
    answer = 'even'
else:
    answer = 'odd'
```
- **说明**：这个 `if` 语句用于判断变量 `a` 是否为偶数，如果是，则将 `answer` 设为 `'even'`，否则设为 `'odd'`。
- **行数**：这段代码占用了四行。

## 3. 使用 if expression

我们可以将上述代码简化为一行，使用 `if` 表达式来实现：

```python
answer = 'even' if a % 2 == 0 else 'odd'
```
- **说明**：这是一行代码的 `if` 表达式形式，它可以在一个表达式中完成条件判断并返回不同的值。

## 4. if expression 的一般形式

`if` 表达式的一般形式如下：

```python
<true-answer> if <expression> else <false-answer>
```
- **说明**：
  - `<expression>`：需要进行判断的条件。
  - `<true-answer>`：如果条件为 `True`，则返回的值。
  - `<false-answer>`：如果条件为 `False`，则返回的值。

## 5. 使用场景

- **简化代码**：`if` 表达式适用于那些简单的条件判断，可以将代码压缩到一行，从而提高代码的可读性。
- **赋值语句**：当需要根据条件为变量赋值时，`if` 表达式是一种非常方便的方式。

## 6. 示例代码

### 示例 1: 判断偶数或奇数

```python
a = 5

# 使用常规的 if 语句
if (a % 2) == 0:
    answer = 'even'
else:
    answer = 'odd'
print(answer)

# 使用 if expression
answer = 'even' if a % 2 == 0 else 'odd'
print(answer)
```
- **输出**：
  ```
  odd
  odd
  ```
- **说明**：无论是使用常规的 `if` 语句，还是使用 `if` 表达式，都可以得到相同的结果。

## 7. 使用 if expression 提高代码的简洁性

在一些场景下，`if` expression 可以让代码变得更加简洁和易读，例如：

### 示例 2: 根据分数判断等级

```python
score = 85

# 使用 if expression 判断等级
grade = 'A' if score >= 90 else 'B' if score >= 80 else 'C'
print(grade)
```
- **输出**：
  ```
  B
  ```
- **说明**：通过嵌套的 `if` expression，可以根据分数判断等级，使得代码更加紧凑。

---


## 8. 练习题目：使用 if expression

### 问题 1: 使用 if expression 简化代码

**题目描述**：
如果有两个变量 `a` 和 `b`，并且希望在 `a` 大于 `b` 时打印 `a`，否则打印 `b`，可以使用如下的 `if` 语句：

```python
if a > b:
    print(a)
else:
    print(b)
```
请使用 `if` expression instead of the if statement.

**答案**：
```python
print(a) if a > b else print(b)
```
- **考点**：使用 `if` expression 替代简单的 `if-else` 语句，使代码更加简洁。

### 问题 2: 使用更复杂的 if expression

**题目描述**：
另一个语句可能如下所示：

```python
if a > b:
    print("A is larger")
elif a == b:
    print("A == B")
else:
    print("B is larger")
```
请使用更复杂的 `if` expression 来替代上面的代码。

**答案**：
```python
print("A is larger") if a > b else print("A == B") if a == b else print("B is larger")
```
- **考点**：使用嵌套的 `if` expression 替代多条件判断的 `if-elif-else` 语句，使代码更紧凑。

