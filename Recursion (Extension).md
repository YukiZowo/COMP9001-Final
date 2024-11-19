# Recursion 递归

## 1. 什么是递归函数？

在之前的函数基础课程中，我们以斐波那契数列为例，讨论了一个调用自身的函数。这样的函数被称为“递归函数”。递归解决方案可以非常优雅，但递归并不是解决问题的唯一方式。

**递归**是指当一个函数通过调用自身来解决问题的过程。

虽然递归解决方案有时非常简洁和优雅，但并非总是必要的。很多情况下，迭代的方式更高效且更容易理解。

## 2. 阶乘例子 (Factorial Example)

### 2.1 阶乘的定义

一个数字 `n` 的阶乘，用符号 `n!` 表示，计算方式如下：

```
n! = n × (n - 1) × (n - 2) × ⋯ × 3 × 2 × 1
```

### 2.2 迭代解决方案

通过迭代的方式计算阶乘的 Python 代码如下：

```python
def fact_iterative(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result
```

### 2.3 递归解决方案

我们也可以使用递归来定义阶乘：

```
n! = n × (n - 1)!, with 1! = 1
```

在 Python 中实现递归方式的阶乘：

```python
def fact_recursive(n):
    if n == 1:
        return 1
    else:
        return n * fact_recursive(n - 1)
```

递归版本的代码更少，通常也更清晰。

- **基例 (Base Case)**：条件 `n == 1` 被称为基例。当基例满足时，函数停止调用自身并返回 1。
- **递归步骤 (Recursive Case)**：在递归情况下，函数逐步将问题缩小，将 `n` 与 `n-1` 的阶乘相乘。

## 3. 递归的适用场景

递归特别适合用于解决那些可以分解为相似子问题的任务，比如搜索或遍历数据结构。

### 3.1 二分查找 (Binary Search)

递归的一个实际应用例子是**二分查找**，这是一种在有序列表中查找元素的快速方法。

#### 二分查找的工作原理 (Plain English)

1. 对列表进行排序。
2. 重复以下步骤：
   - 检查列表的中间元素是否是目标值。
   - 如果是，找到目标。
   - 如果列表只剩一个元素且不是目标，搜索失败。
   - 如果目标值大于中间元素，在列表的后半部分继续搜索。
   - 如果目标值小于中间元素，在列表的前半部分继续搜索。

二分查找比逐个检查元素的线性查找要快得多，尤其是对于大型数据集。

#### 二分查找的递归代码

```python
def binary_search_recursive(sorted_list, target):
    # 基例：如果列表为空，则表示未找到目标 (Base case: if the list is empty, the target is not found)
    if len(sorted_list) == 0:
        return False
    
    # 找到中间索引 (Find the middle index)
    mid_index = len(sorted_list) // 2
    mid_element = sorted_list[mid_index]
    
    # 如果中间元素是目标值，返回 True (found) (If the middle element is the target, return True)
    if mid_element == target:
        return True
    
    # 如果目标小于中间元素，搜索前半部分 (If the target is smaller than the middle element, search the first half)
    elif target < mid_element:
        return binary_search_recursive(sorted_list[:mid_index], target)
    
    # 如果目标大于中间元素，搜索后半部分 (If the target is larger than the middle element, search the second half)
    else:
        return binary_search_recursive(sorted_list[mid_index + 1:], target)
```

## 4. 递归与迭代的比较

| 特性                 | 递归                          | 迭代                |
|---------------------|-------------------------------|---------------------|
| 代码长度            | 通常较短                       | 通常较长           |
| 可读性              | 适合解决分治问题，代码简洁     | 逻辑直观，适合简单循环 |
| 性能                | 对于深度递归可能会有性能问题   | 通常更高效         |

递归在解决分治问题（如二分查找、快速排序）时非常有用，但在一些情况下，迭代的实现更加高效，因为递归可能会导致栈溢出，尤其是递归深度很大时。

## 5. 递归的优缺点

### 5.1 优点

- **代码简洁**：递归代码通常比迭代代码更短、更清晰，特别适用于可以自然地分解为子问题的情况。
- **适合解决复杂问题**：递归特别适合解决某些分治类问题，如树的遍历、图的深度优先搜索等。

### 5.2 缺点

- **性能问题**：递归调用会占用系统栈内存，如果递归层次很深，可能会导致栈溢出。
- **效率较低**：递归有时会因为重复计算相同子问题而导致效率较低，例如经典的斐波那契数列递归求解。

## 6. 递归的改进技巧

### 6.1 尾递归优化 (Tail Recursion Optimization)

在某些编程语言中，尾递归可以被优化，以避免深度递归导致的栈溢出。尾递归指的是递归调用是函数中的最后一步。例如：

```python
def tail_recursive_factorial(n, acc=1):
    if n == 1:
        return acc
    else:
        return tail_recursive_factorial(n - 1, n * acc)
```

在 Python 中，尾递归并不会自动优化，但理解尾递归对于递归思想的掌握是有帮助的。

### 6.2 记忆化递归 (Memoization)

通过记忆化（缓存中间结果），可以避免递归过程中重复计算相同子问题。例如，可以使用 `functools.lru_cache` 装饰器来优化斐波那契数列的计算：

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fib(n):
    if n <= 1:
        return n
    else:
        return fib(n - 1) + fib(n - 2)
```

通过记忆化，递归计算斐波那契数列的效率得到了显著提高。

---

