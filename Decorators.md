# Python Decorators 详解

## 1. 什么是 Decorator？

Decorator（装饰器）是 Python 中的一种高级特性，允许你在不修改函数本身的情况下为其添加功能。装饰器的核心思想是将一个函数包装在另一个函数中，自动完成一些功能的增强或修改。

## 2. 为什么使用 Decorator？

有时候我们需要为已有的函数添加功能，但又不想直接修改它的代码。这样可以使用装饰器来“包装”这个函数，动态地添加功能而无需修改函数的代码。

例如，在一个轻量级的 Web 服务器系统（如 [bottle](http://bottlepy.org)）中，有一组用于复杂数据处理的装饰器函数。

## 3. Decorator 的基本用法

装饰器通常通过 `@` 符号来使用，将其放在函数的定义之前。

### 3.1 示例：使用装饰器处理 URL 请求

```python
@route('/hello')
def hello():
    return "Hello World!"
```

- **说明**：`@route('/hello')` 表示将接下来的函数 `hello()` 包装在函数 `route()` 中，参数为 `'/hello'`。
- 当请求到达 `/hello` URL 时，会运行函数 `hello()`。

## 4. 自定义 Decorator

你可以自己编写装饰器来为函数添加前后处理逻辑，而无需修改函数本身。

### 4.1 编写自定义装饰器

```python
def doit(fun):
    def wrap(*args, **kwargs):
        print("before")
        result = fun(*args, **kwargs)
        print("after")
        return result
    return wrap
```

- **说明**：
  - `doit(fun)` 是一个装饰器，它接受一个函数 `fun` 作为参数。
  - `wrap(*args, **kwargs)` 是包装函数，添加了执行前后的打印语句。
  - 最终返回的 `wrap` 函数就是被装饰的版本。

### 4.2 使用自定义装饰器

```python
@doit
def addup(x, y):
    return x + y

print(addup(1, 2))
```

- **说明**：`@doit` 装饰了函数 `addup()`。
- **输出**：
  ```
  before
  after
  3
  ```
- **解释**：装饰器在调用 `addup(1, 2)` 时，会先打印 `before`，然后执行 `addup` 函数并得到结果，最后打印 `after`。

## 5. 装饰器的应用场景

- **日志记录 (Logging)**：在函数执行前后记录日志，方便调试和排查问题。
- **性能计时** (Performance Timing)：记录函数的执行时间，用于性能监控。
- **访问控制** (Access Control)：检查用户权限，决定是否允许调用某个函数。
- **事务处理** (Transaction Handling)：例如在数据库操作中，用装饰器来处理事务的开始和结束。

### 5.1 示例：计时装饰器

```python
import time

def timer(fun):
    def wrap(*args, **kwargs):
        start_time = time.time()
        result = fun(*args, **kwargs)
        end_time = time.time()
        print(f"Execution time: {end_time - start_time} seconds")
        return result
    return wrap

@timer
def slow_function():
    time.sleep(2)
    print("Function finished")

slow_function()
```

- **说明**：
  - `timer(fun)` 是一个计时装饰器，用于测量函数的执行时间。
  - 在调用 `slow_function()` 时，会先记录开始时间，执行函数，然后记录结束时间，并输出执行时间。
- **输出**：
  ```
  Function finished
  Execution time: 2.0 seconds
  ```

## 6. 多个装饰器的使用

一个函数可以被多个装饰器修饰，从上到下依次应用。

### 6.1 示例：多个装饰器

```python
def decorator1(fun):
    def wrap(*args, **kwargs):
        print("Decorator 1: Before")
        result = fun(*args, **kwargs)
        print("Decorator 1: After")
        return result
    return wrap

def decorator2(fun):
    def wrap(*args, **kwargs):
        print("Decorator 2: Before")
        result = fun(*args, **kwargs)
        print("Decorator 2: After")
        return result
    return wrap

@decorator1
@decorator2
def greet():
    print("Hello!")

greet()
```

- **说明**：
  - 函数 `greet()` 被 `@decorator1` 和 `@decorator2` 修饰。
  - 调用顺序为：先应用 `decorator2`，再应用 `decorator1`。
- **输出**：
  ```
  Decorator 1: Before
  Decorator 2: Before
  Hello!
  Decorator 2: After
  Decorator 1: After
  ```

## 7. 装饰器的注意事项

- **函数元数据丢失**：被装饰的函数会失去原有的名称、文档字符串等元数据。可以使用 `functools.wraps()` 来保留这些元数据。

### 7.1 示例：保留元数据

```python
from functools import wraps

def doit(fun):
    @wraps(fun)
    def wrap(*args, **kwargs):
        print("before")
        result = fun(*args, **kwargs)
        print("after")
        return result
    return wrap

@doit
def addup(x, y):
    """Add two numbers."""
    return x + y

print(addup.__name__)  # 输出: addup
print(addup.__doc__)   # 输出: Add two numbers.
```

- **说明**：`@wraps(fun)` 用于保留被装饰函数的元数据，例如函数名和文档字符串。

---


## 8. Decorator 实践练习

### 练习 1: 基本装饰器 (Basic Decorator)

**任务描述**：创建一个记录函数执行过程的装饰器。Create a decorator that logs the execution of a function.

编写一个名为 `log_execution` 的装饰器，在函数运行之前打印 "Executing function..."，在函数结束后打印 "Function executed!"。将该装饰器应用于函数 `greet`，使其打印问候信息。  
Write a decorator called `log_execution` that prints "Executing function..." before the function runs and "Function executed!" after the function finishes. Apply this decorator to a function `greet` that prints a greeting message.

```python
# 定义装饰器 log_execution
def log_execution(fun):
    def wrap(*args, **kwargs):
        print("Executing function...")
        result = fun(*args, **kwargs)
        print("Function executed!")
        return result
    return wrap

# 使用装饰器
@log_execution
def greet():
    print("Hello, welcome!")

greet()
```
- **输出**：
  ```
  Executing function...
  Hello, welcome!
  Function executed!
  ```
- **考点**：理解如何创建基本的装饰器，以及如何在函数执行的前后添加额外的逻辑。

### 练习 2: 带参数的装饰器 (Decorator with Arguments)

**任务描述**：创建一个装饰器，用于检查函数参数是否有效。Create a decorator that checks for valid arguments.

编写一个名为 `validate_args` 的装饰器，检查传递给函数的参数是否是特定类型（例如 `int` 或 `float`）。如果提供了无效的参数，打印 "Invalid argument!" 并返回 `None`，否则执行函数。将该装饰器应用于函数 `add`，该函数用于将两个数字相加。
Write a decorator called `validate_args` that checks if the arguments provided to a function are of a specific type (e.g., `int` or `float`). If an invalid argument is provided, print "Invalid argument!" and return `None`. Otherwise, execute the function. Apply this decorator to a function add that adds two numbers together.

```python
# 定义装饰器 validate_args
def validate_args(fun):
    def wrap(*args, **kwargs):
        if all(isinstance(arg, (int, float)) for arg in args):
            return fun(*args, **kwargs)
        else:
            print("Invalid argument!")
            return None
    return wrap

# 使用装饰器
@validate_args
def add(x, y):
    return x + y

print(add(2, 3))      # 输出: 5
print(add(2, "three")) # 输出: Invalid argument!
```
- **考点**：学习如何创建带参数检查功能的装饰器，确保函数的输入符合预期。

### 练习 3: 可复用的计时装饰器 (Reusable Decorator for Timing Functions)

**任务描述**：创建一个装饰器，用于测量函数的执行时间。Create a decorator that measures the execution time of a function.

编写一个名为 `measure_time` 的装饰器，记录函数执行的时间。将该装饰器应用于函数 `factorial_iterative`，该函数用于计算一个数的阶乘。
Write a decorator called `measure_time` that records the time taken to execute a function. Apply this decorator to a function `factorial_iterative` that calculates the factorial of a number.

```python
import time

# 定义装饰器 measure_time
def measure_time(fun):
    def wrap(*args, **kwargs):
        start_time = time.time()
        result = fun(*args, **kwargs)
        end_time = time.time()
        print(f"Time taken to execute: {end_time - start_time} seconds")
        return result
    return wrap

# 使用装饰器
@measure_time
def factorial_iterative(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result

print(factorial_iterative(25))
```
- **输出**：
  ```
  Time taken to execute: <time> seconds
  15511210043330985984000000
  ```
- **考点**：学习如何使用 `time` 库来计算函数的执行时间，以及如何创建一个可复用的计时装饰器。

---

