# 类的特性（Class Features）

在 Python 中，类是面向对象编程的核心。类的特性包括特殊方法、继承和特殊变量，这些是编写高级 Python 程序的重要工具。

---

## 1. 特殊方法（Special Methods）
特殊方法是以双下划线开头和结尾的函数（例如 `__init__`、`__str__`），也被称为 "魔法方法"。它们允许我们自定义类的行为，如对象的初始化、打印、比较等。

### 常见的特殊方法
| 方法            | 作用                                                             | 示例                                       |
|-----------------|----------------------------------------------------------------|-------------------------------------------|
| `__init__`      | 初始化方法，用于创建对象时初始化属性。                            | `obj = MyClass(arg1, arg2)`               |
| `__str__`       | 定义对象的字符串表示，`print(obj)` 时会调用。                     | `print(obj)`                              |
| `__repr__`      | 定义对象的官方字符串表示，用于调试。                              | `repr(obj)` 或交互式解释器直接输入对象名  |
| `__len__`       | 定义 `len(obj)` 的行为。                                         | `len(obj)`                                |
| `__getitem__`   | 定义对象的索引行为，允许通过 `obj[key]` 访问数据。                | `obj[key]`                                |
| `__setitem__`   | 定义对象的赋值行为，允许通过 `obj[key] = value` 设置数据。         | `obj[key] = value`                        |
| `__call__`      | 使对象可以像函数一样调用。                                       | `obj(args)`                               |
| `__eq__`        | 定义相等比较（`==`）。                                           | `obj1 == obj2`                            |
| `__lt__`        | 定义小于比较（`<`）。                                            | `obj1 < obj2`                             |

#### 示例代码：特殊方法
```python
class MyClass:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"MyClass(name={self.name}, age={self.age})"

    def __len__(self):
        return self.age

# 测试
obj = MyClass("Alice", 25)
print(obj)             # 调用 __str__: 输出 MyClass(name=Alice, age=25)
print(len(obj))        # 调用 __len__: 输出 25
```


## 2. 继承（Inheritance）

继承是面向对象编程的核心概念之一，允许一个类从另一个类中继承属性和方法，从而实现代码的复用。

### 关键点
1. **父类和子类**：
   - **父类（或基类）**：提供基础功能的类。
   - **子类**：继承父类的功能，并可以扩展或重写父类的方法。

2. **方法重写**：
   - 子类通过定义与父类同名的方法，可以覆盖或重写父类的方法。

3. **`super()` 函数**：
   - 用于在子类中调用父类的方法或构造函数。

#### 继承的基本语法
```python
class ParentClass:
    # 父类方法
    def greet(self):
        print("Hello from ParentClass")

class ChildClass(ParentClass):
    # 子类方法
    def greet(self):
        super().greet()  # 调用父类的方法
        print("Hello from ChildClass")
```
#### 示例代码：继承与方法重写
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def sound(self):
        print("Animals make sounds")

class Dog(Animal):
    def sound(self):
        print(f"{self.name} says Woof!")

# 测试代码
dog = Dog("Buddy")
dog.sound()  # 输出：Buddy says Woof!
```

#### 示例代码：使用 super() 调用父类方法
```python
class Parent:
    def __init__(self, name):
        self.name = name

    def display(self):
        print(f"Parent name: {self.name}")

class Child(Parent):
    def __init__(self, name, age):
        super().__init__(name)  # 调用父类的构造函数
        self.age = age

    def display(self):
        super().display()  # 调用父类的方法
        print(f"Child age: {self.age}")

# 测试代码
child = Child("Alice", 12)
child.display()
# 输出：
# Parent name: Alice
# Child age: 12
```

### 多重继承
在 Python 中，一个子类可以从多个父类继承。这种机制被称为**多重继承**。
#### 多重继承的语法
```python
class Parent1:
    def method1(self):
        print("Method from Parent1")

class Parent2:
    def method2(self):
        print("Method from Parent2")

class Child(Parent1, Parent2):
    pass

# 测试代码
child = Child()
child.method1()  # 输出：Method from Parent1
child.method2()  # 输出：Method from Parent2
```

### 注意：MRO（方法解析顺序）
- 如果一个方法在多个父类中出现，Python 会根据 **MRO（Method Resolution Order）** 来决定调用顺序。

- 可以通过 `ClassName.mro()` 查看类的继承顺序。
```python
print(Child.mro())
```


## 3. 特殊变量（Special Variables）

特殊变量是 Python 提供的一些预定义属性或变量，通常以双下划线开头和结尾（如 `__name__` 和 `__dict__`）。这些变量用于存储类、对象或模块的元信息，帮助开发者调试、运行模块逻辑等。

---

### 常见的特殊变量及其作用

| 特殊变量         | 作用                                           | 示例                                    |
|------------------|----------------------------------------------|----------------------------------------|
| `__dict__`       | 存储对象或类的所有属性（以字典形式）。           | `obj.__dict__`                         |
| `__name__`       | 存储当前模块的名称。主模块为 `"__main__"`，否则为模块名。 | `if __name__ == "__main__":`           |
| `__class__`      | 存储对象所属的类。                            | `obj.__class__`                        |
| `__module__`     | 存储对象所属模块的名称。                      | `obj.__module__`                       |
| `__doc__`        | 存储类或函数的文档字符串（docstring）。          | `print(MyClass.__doc__)`               |
| `__annotations__`| 存储类或函数的类型注解。                      | `def func(x: int) -> str: pass`        |



### 3.1. 什么是特殊变量？
Python 类中的特殊变量，也称为魔法变量或 dunder（double underscore）变量，以双下划线（`__`）开头和结尾。它们通常用于提供对象的元信息，或在特定情况下被 Python 解释器自动调用。

以下是一些常见的 Python 类特殊变量及其详细说明。

### 3.2. 常见的类特殊变量

#### 3.2.1 `__init__`
- **定义**：`__init__` 是类的构造方法，用于在创建对象时初始化实例的属性。
- **使用**：
  ```python
  class Car:
      def __init__(self, brand, model):
          self.brand = brand
          self.model = model

  car = Car('Toyota', 'Corolla')
  print(car.brand)  # 输出: Toyota
  ```
- **说明**：`__init__` 在类实例化时自动调用。

#### 3.2.2 `__str__`
- **定义**：`__str__` 方法定义对象的“可打印”字符串表示形式。
- **使用**：
  ```python
  class Car:
      def __init__(self, brand, model):
          self.brand = brand
          self.model = model

      def __str__(self):
          return f"Car(brand='{self.brand}', model='{self.model}')"

  car = Car('Toyota', 'Corolla')
  print(car)  # 输出: Car(brand='Toyota', model='Corolla')
  ```
- **说明**：`__str__` 方法主要用于 `print()` 函数或 `str()` 函数的输出。

#### 3.2.3 `__repr__`
- **定义**：`__repr__` 方法返回对象的正式字符串表示，主要用于调试。
- **使用**：
  ```python
  class Car:
      def __init__(self, brand, model):
          self.brand = brand
          self.model = model

      def __repr__(self):
          return f"Car(brand='{self.brand}', model='{self.model}')"

  car = Car('Toyota', 'Corolla')
  print(repr(car))  # 输出: Car(brand='Toyota', model='Corolla')
  ```
- **说明**：`__repr__` 通常用于开发者调试，而 `__str__` 用于用户输出。

#### 3.2.4 `__dict__`
- **定义**：`__dict__` 是一个存储对象可写属性的字典。
- **使用**：
  ```python
  class Car:
      def __init__(self, brand, model):
          self.brand = brand
          self.model = model

  car = Car('Toyota', 'Corolla')
  print(car.__dict__)  # 输出: {'brand': 'Toyota', 'model': 'Corolla'}
  ```
- **说明**：`__dict__` 提供了对象的所有属性和值的映射关系，通常用于检查对象的属性。

#### 3.2.5 `__class__`
- **定义**：`__class__` 用于获取对象所属的类。
- **使用**：
  ```python
  car = Car('Toyota', 'Corolla')
  print(car.__class__)  # 输出: <class '__main__.Car'>
  ```
- **说明**：`__class__` 常用于获取对象的类型信息。

#### 3.2.6 `__name__`
- **定义**：`__name__` 通常用于类或模块名，表示模块或类的名称。
- **使用**：
  ```python
  class Car:
      pass

  print(Car.__name__)  # 输出: Car
  ```
- **说明**：`__name__` 通常用于调试或记录日志以查看类或模块的名称。

#### 3.2.7 `__module__`
- **定义**：`__module__` 返回定义类的模块名。
- **使用**：
  ```python
  class Car:
      pass

  car = Car()
  print(car.__module__)  # 输出: '__main__'
  ```
- **说明**：当类定义在不同模块中时，`__module__` 可以帮助确认类的来源。

#### 3.2.8 `__bases__`
- **定义**：`__bases__` 是一个元组，包含类的所有父类。
- **使用**：
  ```python
  class Vehicle:
      pass

  class Car(Vehicle):
      pass

  print(Car.__bases__)  # 输出: (<class '__main__.Vehicle'>,)
  ```
- **说明**：`__bases__` 可以用于查看一个类的继承结构。

#### 3.2.9 `__slots__`
- **定义**：`__slots__` 用于限制类实例的属性，减少内存占用。
- **使用**：
  ```python
  class Car:
      __slots__ = ['brand', 'model']

      def __init__(self, brand, model):
          self.brand = brand
          self.model = model

  car = Car('Toyota', 'Corolla')
  # car.year = 2021  # AttributeError: 'Car' object has no attribute 'year'
  ```
- **说明**：`__slots__` 可以限制类的属性，阻止随意添加新属性，节省内存。

#### 3.2.10 `__doc__`
- **定义**：`__doc__` 存储类或函数的文档字符串。
- **使用**：
  ```python
  class Car:
      """A simple car class representing a vehicle."""
      def __init__(self, brand, model):
          self.brand = brand
          self.model = model

  print(Car.__doc__)  # 输出: A simple car class representing a vehicle.
  ```
- **说明**：`__doc__` 用于提供类、函数、模块等的文档字符串，有助于代码的可读性。

#### 3.2.11 `__call__`
- **定义**：`__call__` 允许一个类的实例像函数一样被调用。
- **使用**：
  ```python
  class Greet:
      def __call__(self, name):
          print(f"Hello, {name}!")

  greet = Greet()
  greet("Yuki")  # 输出: Hello, Yuki!
  ```
- **说明**：通过实现 `__call__` 方法，类的对象可以像函数一样被直接调用。
---


### 3.3 类变量

类变量是与类本身相关联的变量，而不是与某个特定对象相关联的变量。类变量对所有类的实例共享，通常用于存储所有实例之间共享的数据。

#### 3.3.1 类变量的定义
- **定义**：类变量是在类体内、方法之外定义的变量。
- **使用**：
  ```python
  class Toy:
      number_of_toys = 0  # 类变量，用于统计创建的玩具数量

      def __init__(self, toytype, price, colour):
          Toy.number_of_toys += 1  # 每创建一个玩具对象，数量加一
          self.toytype = toytype
          self.price = price
          self.colour = colour

      def price_increase(self, amount):
          self.price += amount
  
  toy1 = Toy('Car', 10, 'Red')
  toy2 = Toy('Doll', 15, 'Blue')
  print(Toy.number_of_toys)  # 输出: 2
  ```
- **说明**：在这个例子中，`number_of_toys` 是一个类变量，所有 `Toy` 类的实例共享它。每次创建一个新对象时，类变量的值都会增加。

#### 3.3.2 类变量的访问
- **定义和访问类变量**：类变量可以通过类名访问，也可以通过类的实例访问。
- **使用**：
  ```python
  print(Toy.number_of_toys)  # 通过类名访问类变量，输出: 2
  print(toy1.number_of_toys)  # 通过实例访问类变量，输出: 2
  ```
- **说明**：类变量通常通过类名来访问，以便清楚地表明这是一个类级别的属性。

---


### 3.4 私有类和方法变量（Private Class and Method Variables）

在 Python 中，私有变量和方法可以通过在名称前加下划线来实现。虽然 Python 没有真正的私有变量，但通过以下方式可以实现类似私有的行为。

#### 3.4.1 私有实例变量
- **定义**：使用单下划线 `_` 或双下划线 `__` 作为变量名前缀来定义私有变量。
- **使用**：
  ```python
  class Car:
      def __init__(self, brand, model):
          self.__brand = brand  # 双下划线表示私有变量
          self._model = model   # 单下划线表示建议为私有的变量

      def get_brand(self):
          return self.__brand

  car = Car('Toyota', 'Corolla')
  # print(car.__brand)  # AttributeError: 'Car' object has no attribute '__brand'
  print(car.get_brand())  # 输出: Toyota
  ```
- **说明**：双下划线会触发名称重整（name mangling），使变量名变为 `_ClassName__VariableName`，从而避免被外部直接访问。

#### 3.4.2 私有方法
- **定义**：使用双下划线 `__` 作为方法名前缀来定义私有方法。
- **使用**：
  ```python
  class Car:
      def __init__(self, brand, model):
          self.__brand = brand
          self.__model = model

      def __display_info(self):
          print(f"Brand: {self.__brand}, Model: {self.__model}")

      def show_info(self):
          self.__display_info()

  car = Car('Toyota', 'Corolla')
  # car.__display_info()  # AttributeError: 'Car' object has no attribute '__display_info'
  car.show_info()  # 输出: Brand: Toyota, Model: Corolla
  ```
- **说明**：私有方法只能在类的内部调用，不能被类的外部直接访问。

#### 3.4.3 单下划线 `_` 的约定
- **定义**：使用单下划线作为变量或方法的前缀表示这些属性或方法是内部使用的，虽然它们不是严格的私有属性，但不建议外部直接访问。
- **使用**：
  ```python
  class Car:
      def __init__(self, brand, model):
          self._brand = brand  # 单下划线表示内部使用
          self._model = model

      def _display_info(self):
          print(f"Brand: {self._brand}, Model: {self._model}")

  car = Car('Toyota', 'Corolla')
  car._display_info()  # 虽然可以访问，但不建议外部调用
  ```
- **说明**：单下划线的属性和方法在语法上是可以被外部访问的，但在约定上不建议这样做。

---



