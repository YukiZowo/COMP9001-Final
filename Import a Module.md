# Importing Modules （非考点 但很有可能会涉及到）

## 1. 什么是模块 (Module)？

在 Python 中，模块是一个包含 Python 定义和语句的文件，后缀名为 `.py`。模块可以包含函数、类和变量，甚至可以包含可执行的代码。当我们的代码越来越复杂时，可以将代码分割成多个模块，方便复用和管理。

通过导入模块，我们可以使用模块中定义的各种功能，而不需要自己重新编写。这大大提高了代码的复用性和可维护性。

## 2. 导入模块的方法

Python 提供了多种方式来导入模块，以下是常见的几种：

### 2.1 使用 `import` 导入整个模块

我们可以使用 `import` 关键字导入整个模块，然后通过 `模块名.功能` 的方式来调用模块中的内容。

```python
import math

# 使用 math 模块中的函数 (Use functions from the math module)
result = math.sqrt(16)
print(result)  # 输出: 4.0
```

- **说明**：上面的代码导入了 `math` 模块，并使用 `math.sqrt()` 函数计算 16 的平方根。

### 2.2 使用 `from ... import ...` 导入特定的功能

如果我们只需要模块中的某个特定功能，可以使用 `from ... import ...` 语句来导入，这样就不需要每次都写模块名。

```python
from math import sqrt

# 直接使用 sqrt 函数 (Directly use the sqrt function)
result = sqrt(25)
print(result)  # 输出: 5.0
```

- **说明**：这段代码只从 `math` 模块中导入了 `sqrt` 函数，因此可以直接调用 `sqrt()`。

### 2.3 使用 `as` 为模块或函数起别名

我们还可以使用 `as` 关键字为模块或函数起一个别名，方便在代码中使用。

```python
import numpy as np

# 使用别名 np 调用 numpy 模块 (Use alias np to call numpy module)
array = np.array([1, 2, 3])
print(array)  # 输出: [1 2 3]
```

- **说明**：`numpy` 模块被重命名为 `np`，这样在使用时更加简洁。

## 3. 常用模块介绍

Python 标准库包含了许多常用模块，以下是一些示例：

- **`math`**：提供基本的数学函数。
- **`random`**：用于生成随机数。
- **`datetime`**：处理日期和时间。
- **`os`**：与操作系统交互，处理文件和目录。

### 示例

```python
import random

# 生成一个 1 到 10 之间的随机数 (Generate a random number between 1 and 10)
random_number = random.randint(1, 10)
print(random_number)
```

- **说明**：`random.randint()` 函数用于生成指定范围内的随机整数。

## 4. 自定义模块

除了导入 Python 提供的标准模块，我们还可以创建自己的模块。例如，将一些常用函数放在一个 `.py` 文件中，然后在其他程序中导入使用。

### 4.1 创建一个自定义模块

创建一个名为 `my_module.py` 的文件，内容如下：

```python
# 文件: my_module.py

def greet(name):
    return f"Hello, {name}!"
```

### 4.2 导入自定义模块

在另一个文件中，可以导入并使用 `my_module` 中的函数：

```python
import my_module

message = my_module.greet("Alice")
print(message)  # 输出: Hello, Alice!
```

## 5. 导入多个功能

我们可以一次导入多个功能，使用逗号分隔：

```python
from math import sqrt, pi

print(sqrt(9))  # 输出: 3.0
print(pi)       # 输出: 3.141592653589793
```

- **说明**：这种方式可以简化代码，但在功能名称冲突时要特别小心。

## 6. 示例练习

### 练习 1: 使用 `math` 模块计算圆的面积

**任务描述**：
使用 `math` 模块中的 `pi` 常量和 `pow()` 函数，计算半径为 5 的圆的面积。

**答案**：
```python
import math

radius = 5
area = math.pi * math.pow(radius, 2)
print(area)  # 输出: 78.53981633974483
```
- **考点**：理解如何导入和使用模块中的常量和函数。

### 练习 2: 使用 `random` 模块生成随机数列表

**任务描述**：
使用 `random` 模块生成一个包含 5 个 1 到 100 之间随机整数的列表。

**答案**：
```python
import random

random_numbers = [random.randint(1, 100) for _ in range(5)]
print(random_numbers)
```
- **考点**：理解如何使用 `random` 模块生成随机数，并结合列表推导式生成随机数列表。

---

