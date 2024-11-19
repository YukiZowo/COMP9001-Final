# NumPy 详解

## 1. 什么是 NumPy？

If you want to do some very fast calculation in a Python program, you may have to use a different way of storing data. Python lists are not as efficient or high speed as an array. The NUMPY package implements arrays using the **C language** and lets you store your data in very fast arrays.



NumPy 是 Python 中用于科学计算的基础库之一，提供了高效的多维数组对象（ndarray）以及丰富的函数库来操作这些数组。它是数据分析和机器学习的核心工具之一。

- **ndarray**: NumPy 提供了一个强大的多维数组对象，称为 ndarray，这个对象可以用于高效地存储和操作大型数据集。

## 2. NumPy 的基本功能

NumPy 的主要功能包括：

- **多维数组支持**: 提供多维数组对象 ndarray。
- **矢量化计算**: 对数组的运算不需要显式的循环，能够进行快速矢量化运算。
- **数学函数库**: 提供了大量的数学函数用于数组的操作。

## 3. 安装 NumPy

可以使用 `pip` 来安装 NumPy：

```bash
pip install numpy
```

## 4. 创建数组

可以使用 NumPy 创建不同类型的数组。

### 4.1 使用 `array()` 函数创建数组

```python
import numpy as np

# 创建一个一维数组
arr1 = np.array([1, 2, 3, 4, 5])
print(arr1)

# 创建一个二维数组
arr2 = np.array([[1, 2, 3], [4, 5, 6]])
print(arr2)
```

- **说明**：`np.array()` 函数可以将 Python 的列表或元组转换为 NumPy 数组。

### 4.2 使用 `arange()` 和 `linspace()` 函数创建数组

```python
# 使用 arange() 创建数组
arr = np.arange(0, 10, 2)  # 从 0 到 10，步长为 2
print(arr)

# 使用 linspace() 创建等间隔的数组
arr_lin = np.linspace(0, 1, 5)  # 在 0 到 1 之间创建 5 个等间隔的点
print(arr_lin)
```

- **说明**：
  - `np.arange(start, stop, step)`：创建从 `start` 到 `stop`，步长为 `step` 的数组。
  - `np.linspace(start, stop, num)`：在 `start` 到 `stop` 之间生成 `num` 个等间隔的值。

## 5. 数组的基本操作

### 5.1 数组属性

可以使用以下属性来查看数组的基本信息：

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr.shape)  # 数组的形状
print(arr.size)   # 数组的元素总数
print(arr.ndim)   # 数组的维数
print(arr.dtype)  # 数组中元素的数据类型
```

- **说明**：
  - `shape`：返回数组的形状（各维度大小）。
  - `size`：返回数组中元素的总个数。
  - `ndim`：返回数组的维数。
  - `dtype`：返回数组中元素的数据类型。

### 5.2 数组运算

NumPy 提供了很多对数组的操作，例如加减乘除等。

```python
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])

# 数组加法
print(arr1 + arr2)

# 数组乘法
print(arr1 * arr2)

# 数组中的每个元素加 10
print(arr1 + 10)
```

- **说明**：数组之间的运算是元素级的。

### 5.3 数组的索引和切片

可以通过索引和切片来访问数组中的元素。

```python
arr = np.array([[1, 2, 3], [4, 5, 6]])

# 访问特定元素
print(arr[1, 2])  # 输出 6

# 访问特定行或列
print(arr[0, :])  # 输出第一行 [1 2 3]
print(arr[:, 1])  # 输出第二列 [2 5]
```

- **说明**：与 Python 的列表类似，NumPy 数组支持多维索引和切片。

## 6. 常用函数

### 6.1 数学函数

NumPy 提供了很多常用的数学函数，可以对数组中的每个元素进行运算。

```python
arr = np.array([1, 2, 3, 4, 5])

# 计算平方根
print(np.sqrt(arr))

# 计算自然指数
print(np.exp(arr))

# 计算正弦值
print(np.sin(arr))
```

- **说明**：这些函数可以直接作用于数组中的每个元素，而不需要显式地编写循环。

### 6.2 聚合函数

NumPy 还提供了一些用于计算数组中元素的聚合值的函数。

```python
arr = np.array([1, 2, 3, 4, 5])

# 计算数组元素的总和
print(np.sum(arr))

# 计算数组元素的均值
print(np.mean(arr))

# 计算数组元素的最大值
print(np.max(arr))
```

- **说明**：这些函数可以快速计算数组中所有元素的聚合值。

## 7. NumPy 的广播机制

广播是指 NumPy 在执行算术运算时，自动地对不同形状的数组进行扩展，使它们具有相同的形状，从而可以进行运算。

### 7.1 示例：广播机制

```python
arr1 = np.array([[1, 2, 3], [4, 5, 6]])
arr2 = np.array([1, 2, 3])

# arr2 的形状会广播为与 arr1 相同，然后进行逐元素相加
print(arr1 + arr2)
```

- **说明**：这里 `arr2` 的形状会被自动扩展为与 `arr1` 兼容的形状，然后逐元素相加。

## 8. NumPy 练习

### 练习 1: 创建数组

**任务描述**：使用 `arange()` 函数创建一个包含从 0 到 15 的数组，并将其重新形状为一个 3x5 的二维数组。

```python
import numpy as np

# 创建数组并重新形状
arr = np.arange(15).reshape(3, 5)
print(arr)
```

- **输出**：
  ```
  [[ 0  1  2  3  4]
   [ 5  6  7  8  9]
   [10 11 12 13 14]]
  ```
- **考点**：熟悉 `arange()` 和 `reshape()` 函数。

### 练习 2: 数组运算

**任务描述**：创建两个形状相同的数组，对它们进行加法和乘法运算。

```python
arr1 = np.array([[1, 2, 3], [4, 5, 6]])
arr2 = np.array([[7, 8, 9], [10, 11, 12]])

# 数组加法
print(arr1 + arr2)

# 数组乘法
print(arr1 * arr2)
```

- **输出**：
  ```
  [[ 8 10 12]
   [14 16 18]]
  [[ 7 16 27]
   [40 55 72]]
  ```
- **考点**：理解数组的元素级运算。

### 练习 3: 使用广播机制

**任务描述**：创建一个二维数组和一个一维数组，并利用广播机制对它们进行相加。

```python
arr1 = np.array([[1, 2, 3], [4, 5, 6]])
arr2 = np.array([10, 20, 30])

# 广播机制相加
print(arr1 + arr2)
```

- **输出**：
  ```
  [[11 22 33]
   [14 25 36]]
  ```
- **考点**：理解广播机制在不同形状数组间的应用。

### 练习 4: NumPy 基础操作 (Numpy Basics)

**Task Description**: When declaring an array, we simply pass a list (of lists) to the `np.array()` constructor, as shown in our program. We want to try out some of the basic operations in numpy. Refer to the official Numpy documentation to complete the program.

**任务描述**：声明一个数组并使用一些基本操作来操作它，如示例程序中使用 `np.array()` 构造函数传递一个列表（或列表的列表）来声明数组。我们希望尝试一些基本的 NumPy 操作。请参考官方的 Numpy 文档完成该程序。

```python
import numpy as np

# 声明数组 (Declare an array)
my_array = np.array([
    [1, 2, 3],
    [4, 5, 6]
])

# 展示数组 (Showing off my array!)
print('My array:', my_array)

# 数组形状 (Shape of the array)
print('Shape:', my_array.shape)

# 打印第一行 (Print the first row)
print('First row:', my_array[0])

# 打印中间列 (Print the middle column)
print('Middle col:', my_array[:, 1])

# 打印每行的和 (Print the sum of each row)
print('Sum over rows:', my_array.sum(axis=1))

# 将每个元素乘以 10 (Multiply every element by 10)
print('Ten times:', my_array * 10)
```

- **考点**：熟悉数组的基本操作，包括索引、形状、切片和算术运算。



### 练习 5: 数据科学实战 (Data Science Like a Pro)

**Task Description**: In this exercise, we revisit the Gini index calculations problem we have worked on in previous lessons. Load the data from the `data.csv` file and calculate the difference in Gini index values between two years for each country. Find the country with the most significant increase.

**任务描述**：在本练习中，我们将重温之前课程中涉及的基尼指数计算问题。从 `data.csv` 文件中加载数据，计算每个国家两个年份之间基尼指数的差异。找出变化幅度最大的国家。

```python
import csv
import numpy as np

# 从 CSV 文件加载数据 (Load data from the CSV file)
with open('data.csv', newline='') as csvfile:
    reader = csv.reader(csvfile)
    header = next(reader)  # 跳过标题行 (Skip the header row)
    
    countries_list = []  # 国家列表 (List of countries)
    data_list = []  # 数据列表 (List of data)
    for row in reader:
        countries_list.append(row[0])  # 添加国家名称 (Append country name)
        data_list.append([float(row[1]), float(row[2])])  # 添加数据 (Append data)

# 将列表转换为 NumPy 数组 (Create a NumPy array from the data list)
data = np.array(data_list)
print(data)

# 打印数组的形状 (Print the shape of the array)
print('Shape:', data.shape)

# 计算两个年份之间的变化 (Compute the change between the two years)
changes = data[:, 0] - data[:, 1]

# 获取最大变化值 (Get the value of the largest change)
max_change_value = changes.max()

# 获取最大变化的索引 (Get the index of the largest change)
index_largest_increase = np.argmax(changes)

# 获取对应国家的名称 (Get the name of the corresponding country)
country_largest_increase = countries_list[index_largest_increase]

# 打印最大变化的国家及变化值 (Print the country with the largest increase and the change value)
print(f'{country_largest_increase} had the largest increase, at {max_change_value:.2f} points')
```

- **考点**：熟悉从 CSV 文件加载数据，使用 NumPy 进行数据操作，查找最大值及对应索引。

---


