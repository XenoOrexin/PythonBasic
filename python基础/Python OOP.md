## 类和对象

## 封装

## 继承

在 Python 中，继承（**Inheritance**）是面向对象编程的核心特性之一。通过继承，一个类（子类）可以从另一个类（父类或基类）继承属性和方法，从而实现代码的重用和扩展。Python 的继承机制支持**单继承**和**多重继承**，并且提供了一些与继承相关的关键字和语法。

### 1. **继承的基本实现**

继承是通过类定义中的括号 `()` 来实现的，子类在定义时可以指定它要继承的父类。

#### 示例：

```python
# 定义父类
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        print(f"{self.name} makes a sound")

# 定义子类，继承自 Animal
class Dog(Animal):
    def speak(self):
        print(f"{self.name} barks")

# 创建对象
dog = Dog("Buddy")
dog.speak()  # 输出：Buddy barks
```

在这个例子中：
- `Dog` 类继承了 `Animal` 类，它获得了 `Animal` 类的所有属性和方法。
- 子类 `Dog` 通过重写（override）`speak` 方法，自定义了父类的行为。

### 2. **关键字 `super()`**

`super()` 是 Python 中的一个内置函数，用于调用**父类的方法**。通常在子类中覆盖父类的方法时，仍然需要调用父类的初始化方法或者其他逻辑，这时可以通过 `super()` 来实现。

#### 示例：

```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def speak(self):
        print(f"{self.name} makes a sound")

class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)  # 调用父类的 __init__ 方法
        self.breed = breed
    
    def speak(self):
        super().speak()  # 调用父类的 speak 方法
        print(f"{self.name} barks")

dog = Dog("Buddy", "Labrador")
dog.speak()
```

输出：
```
Buddy makes a sound
Buddy barks
```

在这个例子中：
- `super().__init__(name)` 调用了父类 `Animal` 的构造函数，确保 `name` 属性被正确初始化。
- `super().speak()` 在子类的方法中调用了父类的 `speak` 方法。

### 3. **方法重写（Override）**

当子类定义了与父类同名的方法时，子类会覆盖父类的方法。这就是方法重写（Override）。

#### 示例：

```python
class Animal:
    def speak(self):
        print("Animal makes a sound")

class Cat(Animal):
    def speak(self):
        print("Cat meows")

cat = Cat()
cat.speak()  # 输出：Cat meows
```

在这个例子中，`Cat` 类重写了 `Animal` 类的 `speak` 方法，调用 `cat.speak()` 时执行的是子类的方法。

### 4. **多重继承**

Python 支持**多重继承**，即一个类可以从多个父类继承属性和方法。多重继承的实现方式是让子类继承多个父类，以逗号分隔。

#### 示例：

```python
class Animal:
    def move(self):
        print("Animal moves")

class Swimmer:
    def swim(self):
        print("Swimmer swims")

class Fish(Animal, Swimmer):
    pass

fish = Fish()
fish.move()  # 从 Animal 继承
fish.swim()  # 从 Swimmer 继承
```

在这个例子中，`Fish` 类同时继承了 `Animal` 和 `Swimmer` 类，因此它可以调用这两个父类的方法。

### 5. **MRO (Method Resolution Order)**

在多重继承中，当子类调用方法时，Python 需要知道按照什么顺序去查找方法的定义。MRO（方法解析顺序）决定了这个查找顺序。

Python 使用一种叫做**C3 线性化算法**来确定方法的解析顺序。你可以通过 `ClassName.mro()` 或 `ClassName.__mro__` 查看某个类的 MRO。

#### 示例：

```python
class A:
    def method(self):
        print("A method")

class B(A):
    def method(self):
        print("B method")

class C(A):
    def method(self):
        print("C method")

class D(B, C):
    pass

d = D()
d.method()  # 输出：B method
print(D.mro())  # 打印方法解析顺序
```

输出：
```
B method
[<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
```

在这个例子中，`D` 类继承自 `B` 和 `C`，而 `B` 和 `C` 又都继承自 `A`。当调用 `d.method()` 时，Python 会按照 MRO 查找，首先找到 `B` 类的方法并执行。

### 6. **`isinstance()` 和 `issubclass()`**

- **`isinstance()`** 用于检查某个对象是否是某个类或其子类的实例。
- **`issubclass()`** 用于检查某个类是否是另一个类的子类。

#### 示例：

```python
class Animal:
    pass

class Dog(Animal):
    pass

dog = Dog()

print(isinstance(dog, Dog))  # 输出：True
print(isinstance(dog, Animal))  # 输出：True
print(issubclass(Dog, Animal))  # 输出：True
print(issubclass(Animal, Dog))  # 输出：False
```

### 7. **`__init_subclass__()` 方法**

`__init_subclass__()` 是一个特殊的钩子方法，当类被继承时，这个方法会被调用。它可以用于在类继承时自定义行为。

#### 示例：

```python
class Base:
    def __init_subclass__(cls, **kwargs):
        super().__init_subclass__(**kwargs)
        print(f"Class {cls.__name__} is being subclassed")

class SubClass(Base):
    pass

# 当 SubClass 继承 Base 时，__init_subclass__ 会被调用，输出信息
```

### 8. **抽象类与继承**

Python 提供了 `abc` 模块来定义抽象类和抽象方法。抽象类不能被实例化，但可以作为其他类的父类。子类必须实现抽象类中的抽象方法。

#### 示例：

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        print("Dog barks")

dog = Dog()  # 如果子类没有实现抽象方法，实例化会报错
dog.speak()
```

### 总结：
- **继承**：通过 `class SubClass(ParentClass)` 实现，子类可以继承父类的属性和方法。
- **`super()`**：用于调用父类的方法或属性。
- **方法重写**：子类可以通过定义与父类同名的方法来覆盖父类的方法。
- **多重继承**：一个类可以从多个父类继承属性和方法，方法的解析顺序由 MRO 决定。
- **`isinstance()` 和 `issubclass()`**：检查对象是否属于某个类或其子类。
- **`__init_subclass__()`**：钩子方法，用于类被继承时触发。
- **抽象类**：使用 `abc` 模块创建，强制子类实现某些方法。

## 多态