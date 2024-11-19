# Python f-string (格式化字符串)

## 1. 什么是 f-string？

f-string（格式化字符串）是 Python 3.6 及以上版本中引入的一种字符串格式化方法。f-string 使用一种非常直观和简洁的方式来嵌入表达式到字符串中，是 Python 格式化字符串的推荐方式。

f-string 以 `f` 或 `F` 开头，后面跟着一个字符串，字符串中的表达式需要用大括号 `{}` 包含。f-string 能够以更简洁和高效的方式进行字符串拼接和变量插值。

## 2. 基本语法

```python
name = "Alice"
age = 25
intro = f"My name is {name} and I am {age} years old."
print(intro)
```

- **输出**：
  ```
  My name is Alice and I am 25 years old.
  ```

- **说明**：`f"My name is {name} and I am {age} years old."` 中的大括号 `{}` 可以包含变量或表达式，f-string 会将这些变量或表达式的值插入到字符串中。

## 3. 表达式求值

f-string 中不仅可以嵌入变量，还可以嵌入任意的表达式。

```python
a = 5
b = 3
result = f"The sum of {a} and {b} is {a + b}."
print(result)
```

- **输出**：
  ```
  The sum of 5 and 3 is 8.
  ```

- **说明**：在大括号中直接进行表达式计算，f-string 会自动计算表达式的值并将结果插入到字符串中。

## 4. 格式化数字

f-string 可以用于格式化数字，支持设置小数位数、百分比等格式。

```python
pi = 3.1415926535
formatted_pi = f"Pi rounded to 2 decimal places is {pi:.2f}"
print(formatted_pi)
```

- **输出**：
  ```
  Pi rounded to 2 decimal places is 3.14
  ```

- **说明**：`{pi:.2f}` 表示将变量 `pi` 格式化为保留两位小数的浮点数。

## 5. 格式化字符串的宽度和对齐方式

可以通过 f-string 设置字符串的宽度、对齐方式等。

- **示例**：
  ```python
  name = "Alice"
  formatted_name = f"{name:>10}"
  print(formatted_name)
  ```

- **输出**：
  ```
      Alice
  ```

- **说明**：`{name:>10}` 表示将字符串 `name` 右对齐，总长度为 10 个字符。可以使用以下符号设置对齐方式：
  - `<`：左对齐
  - `>`：右对齐
  - `^`：居中对齐

## 6. 嵌套和复杂表达式

f-string 支持嵌套调用和更复杂的表达式。

```python
def get_greeting(name):
    return f"Hello, {name}!"

greeting = f"{get_greeting('Bob')} How are you today?"
print(greeting)
```

- **输出**：
  ```
  Hello, Bob! How are you today?
  ```

- **说明**：f-string 中可以嵌入函数调用或更复杂的表达式。

## 7. 使用字典和列表

f-string 可以直接从字典和列表中取值。

```python
person = {"name": "Charlie", "age": 30}
info = f"Name: {person['name']}, Age: {person['age']}"
print(info)

numbers = [10, 20, 30]
summary = f"The first number is {numbers[0]}"
print(summary)
```

- **输出**：
  ```
  Name: Charlie, Age: 30
  The first number is 10
  ```

## 8. 转义大括号

如果要在 f-string 中显示 `{` 或 `}`，需要使用双大括号进行转义。

```python
expression = f"{{Hello}}"
print(expression)
```

- **输出**：
  ```
  {Hello}
  ```

- **说明**：`{{` 和 `}}` 会被解释为单个大括号。

## 9. f-string 与其他格式化方式的对比

在 Python 中，除了 f-string 之外，还有其他几种字符串格式化方法：

- **百分号格式化**：
  ```python
  name = "Alice"
  age = 25
  intro = "My name is %s and I am %d years old." % (name, age)
  print(intro)
  ```

- **`str.format()` 方法**：
  ```python
  name = "Alice"
  age = 25
  intro = "My name is {} and I am {} years old.".format(name, age)
  print(intro)
  ```

- **f-string**：
  ```python
  name = "Alice"
  age = 25
  intro = f"My name is {name} and I am {age} years old."
  print(intro)
  ```

- **说明**：相比于其他格式化方式，f-string 更加简洁和易读，同时也能提高代码的可维护性。

## 10. 注意事项

- **Python 版本要求**：f-string 只在 Python 3.6 及以上版本中可用。
- **性能**：f-string 通常比 `%` 和 `.format()` 更高效，因为它在编译时就会进行插值操作。

## 总结

f-string 是一种强大且简洁的字符串格式化方式，能够使代码更加直观和易读。无论是基本的字符串插值，还是格式化数字、对齐字符串，f-string 都能为开发者提供灵活的解决方案。

