# Python Lambda Functions （不考）

## 1. 什么是 Lambda 函数？

Lambda 函数，也称为匿名函数，是 Python 中一种简短而灵活的方式来定义没有名称的函数。与普通的 `def` 语句不同，lambda 函数只需一行代码即可创建函数。

Lambda 函数通常用于需要一个简单函数且该函数只会在有限范围内使用的情况下，比如作为参数传递给其他函数或者处理列表中的元素。

## 2. Lambda 函数的语法

Lambda 函数的语法非常简洁，使用 `lambda` 关键字定义，格式如下：

```python
lambda 参数列表: 表达式
```

- `参数列表`：定义函数的输入参数，可以是多个，用逗号分隔。
- `表达式`：返回的计算结果。

Lambda 函数可以看作是一个单行函数，它的表达式部分就是函数的返回值。

### 2.1 示例

```python
# 普通函数 (Regular function)
def add(x, y):
    return x + y

# Lambda 函数 (Lambda function)
add_lambda = lambda x, y: x + y

print(add(3, 5))          # 输出: 8
print(add_lambda(3, 5))   # 输出: 8
```

- **说明**：
  - `add` 是一个使用 `def` 定义的函数，它接收两个参数并返回它们的和。
  - `add_lambda` 是一个等价的 lambda 函数，它也接收两个参数并返回它们的和。

## 3. Lambda 函数的应用场景

Lambda 函数通常用于以下场景：

1. **作为函数参数**：
   Lambda 函数可以作为参数传递给其他函数，例如 `map()`、`filter()` 和 `sorted()`。

   ```python
   # 使用 lambda 在列表中每个元素上应用平方操作
   numbers = [1, 2, 3, 4, 5]
   squared_numbers = list(map(lambda x: x ** 2, numbers))
   print(squared_numbers)  # 输出: [1, 4, 9, 16, 25]
   ```

2. **作为排序的自定义键函数**：
   Lambda 函数常被用来定义排序的规则，比如在 `sorted()` 函数中使用。

   ```python
   # 根据第二个元素对列表进行排序
   pairs = [(1, 2), (3, 1), (5, 0)]
   sorted_pairs = sorted(pairs, key=lambda x: x[1])
   print(sorted_pairs)  # 输出: [(5, 0), (3, 1), (1, 2)]
   ```

## 4. Lambda 函数与普通函数的对比

| 特性                | Lambda 函数                      | 普通函数 (`def` 定义) |
|---------------------|--------------------------------|-----------------------|
| 是否有名称          | 没有                          | 有                   |
| 代码行数            | 一行代码                       | 多行代码             |
| 可读性              | 通常只用于简单的操作，适合短小 | 适合复杂逻辑         |
| 使用场景            | 函数参数、列表操作等            | 通用用途             |

## 5. Lambda 函数的局限性

- Lambda 函数只能包含一个表达式，不能包含复杂的语句。
- Lambda 函数的可读性较低，适合简短的逻辑，过于复杂时建议使用普通函数。

## 6. 示例练习

### 练习 1: 使用 Lambda 计算平方 (Square Calculation)

**任务描述**：
使用 lambda 函数计算给定整数的平方值。

**答案**：
```python
square = lambda x: x ** 2
print(square(4))  # 输出: 16
```
- **考点**：理解 lambda 函数的定义和如何使用它进行简单的数学运算。

### 练习 2: 使用 Lambda 进行列表过滤 (Filtering List with Lambda)

**任务描述**：
使用 lambda 函数和 `filter()` 函数，过滤列表中的所有偶数。

**答案**：
```python
numbers = [1, 2, 3, 4, 5, 6, 7, 8]
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)  # 输出: [2, 4, 6, 8]
```
- **考点**：理解如何将 lambda 函数与 `filter()` 一起使用来进行列表元素的筛选。

---

