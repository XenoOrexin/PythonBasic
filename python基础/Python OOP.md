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

## 多态 Polymorphism

### Python 中的多态

**多态**（Polymorphism）是面向对象编程的核心特性之一，指的是在不同类的对象上调用相同的方法时，表现出不同的行为。在 Python 中，多态的实现方式非常灵活，因为 Python 是动态类型语言，不依赖强类型约束，允许不同类型的对象共享同名的方法或运算符。

### Python 实现多态的方式
Python 的多态主要通过以下方式实现：

1. **方法重写（Overriding）**：子类重写父类的方法，实现不同的行为。
2. **鸭子类型（Duck Typing）**：如果某个对象具有与目标方法签名相同的方法，那么它就可以使用这个方法，而不关心其类型。
3. **内置多态操作**：运算符的多态（如 `+` 号可以用于字符串拼接和数值加法）。
4. **抽象类与接口**：使用 `abc` 模块定义抽象类，确保子类实现必要的方法。

### 1. **方法重写实现多态**
方法重写是多态最直接的实现方式。当子类继承了父类时，可以重写父类的方法，使得相同的方法在不同的类上表现出不同的行为。

#### 示例：

```python
class Animal:
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

def make_animal_speak(animal):
    print(animal.speak())

dog = Dog()
cat = Cat()

make_animal_speak(dog)  # 输出：Woof!
make_animal_speak(cat)  # 输出：Meow!
```

在这个例子中：
- `Dog` 和 `Cat` 类继承了 `Animal` 类，并重写了 `speak` 方法。
- `make_animal_speak` 函数接受一个 `Animal` 类型的参数，但由于多态的特性，可以传递任何继承自 `Animal` 的子类。
- 每个对象根据自身类型调用了适合的 `speak` 方法。

### 2. **鸭子类型（Duck Typing）**
Python 的鸭子类型是一种动态类型检查机制。在 Python 中，"如果它走起来像鸭子，叫起来像鸭子，那它就是鸭子"。这意味着我们只需要关心对象是否有某个方法，而不需要关心它的类型。

#### 示例：

```python
class Bird:
    def fly(self):
        return "Flying high"

class Airplane:
    def fly(self):
        return "Taking off"

def make_it_fly(flying_thing):
    print(flying_thing.fly())

bird = Bird()
plane = Airplane()

make_it_fly(bird)   # 输出：Flying high
make_it_fly(plane)  # 输出：Taking off
```

在这个例子中，`Bird` 和 `Airplane` 都有 `fly()` 方法，但它们不需要有任何继承关系。Python 不关心对象是什么类型，只要它有 `fly()` 方法，函数 `make_it_fly` 就能正常工作。

### 3. **运算符重载的多态**
Python 中的运算符可以通过方法重载表现出多态行为。例如，`+` 运算符在不同的数据类型中具有不同的作用。

#### 示例：

```python
print(3 + 4)         # 数字加法，输出：7
print("Hello" + " World")  # 字符串拼接，输出：Hello World
```

在这个例子中，`+` 运算符对整数执行加法操作，对字符串执行拼接操作。这是运算符多态的一个例子。

### 4. **抽象类与接口**
Python 使用 `abc` 模块来创建抽象类和抽象方法，以确保子类必须实现特定的方法。这种方式实现了多态，保证了不同的子类可以根据需求实现相同的接口。

#### 示例：

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

def make_animal_speak(animal):
    print(animal.speak())

dog = Dog()
cat = Cat()

make_animal_speak(dog)  # 输出：Woof!
make_animal_speak(cat)  # 输出：Meow!
```

在这个例子中：
- `Animal` 类是一个抽象类，它定义了抽象方法 `speak`。
- 子类 `Dog` 和 `Cat` 必须实现 `speak` 方法，否则会抛出 `TypeError`。
- 这确保了每个子类都遵循相同的接口，进一步实现多态。

### Python 多态相关的常用关键字和语法

1. **`class` 关键字**：用于定义类，在多态中用于定义父类和子类。

2. **`super()` 关键字**：用于调用父类的方法或属性，特别在子类重写方法时，仍然可以调用父类的逻辑。

3. **`@abstractmethod` 装饰器**：用于定义抽象方法，确保子类实现该方法。在多态中，用来定义不同类共享的方法接口。

4. **`isinstance()` 函数**：检查一个对象是否是某个类的实例。尽管多态的实现通常不需要检查类型，但 `isinstance()` 有时用于类型检查。

#### 示例：

```python
class Animal:
    def speak(self):
        return "Animal sound"

class Dog(Animal):
    def speak(self):
        return "Woof!"

def animal_sound(animal):
    if isinstance(animal, Animal):
        print(animal.speak())
    else:
        print("Not an animal!")

dog = Dog()
animal_sound(dog)  # 输出：Woof!
```

5. **`issubclass()` 函数**：检查一个类是否是另一个类的子类，这在多态和继承结构中很有用。

#### 示例：

```python
class Animal:
    pass

class Dog(Animal):
    pass

print(issubclass(Dog, Animal))  # 输出：True
print(issubclass(Animal, Dog))  # 输出：False
```

### 总结

Python 中的多态主要通过以下机制实现：
- **方法重写**：子类重写父类的方法，表现出不同的行为。
- **鸭子类型**：不关心对象的类型，只要对象有相同的接口，就可以执行。
- **运算符重载的多态**：同一个运算符在不同的类型中表现出不同的行为。
- **抽象类和接口**：通过 `abc` 模块定义接口，确保子类实现特定的行为。

常用的关键字和语法包括 `class`、`super()`、`@abstractmethod`、`isinstance()` 和 `issubclass()`。通过这些工具，Python 提供了强大的多态支持，允许不同类的对象使用相同的接口，同时表现出不同的行为。


## 类属性

类属性定义了类级别的数据，与实例属性不同，类属性是共享的，所有实例都可以访问和共享类属性的值。下面的代码中对类属性的修改会影响所有该类的实例：

```Python
class Stu:  
    classroom = "202"  
    def __init__(self,name):  
        self.name = name  
  
stu1 = Stu("john")  
stu2 = Stu("lara")  
print(stu1.classroom)  # 输出的结果为202
print(stu2.classroom)  # 输出的结果为202
Stu.classroom = 205  # 修改类属性
print(stu1.classroom)  # 输出的结果为205
print(stu2.classroom)  # 输出的结果为205
```

### 类属性的核心知识点

1. **类属性的定义**: 类属性定义在类的主体中（不是在方法内部），它是类的一个特定属性，通常用于存储类级别的共享数据。
2. **类属性的访问**: 类属性可以通过类本身和实例来访问，具有全局共享的特性。

### 类属性的定义和使用
#### 1. 类属性的定义
类属性定义在类体内，并且不属于任何方法。

```python
class MyClass:
    class_variable = "This is a class attribute"
```

在上面的代码中，`class_variable` 是一个类属性。它存在于类的命名空间中，可以通过类名直接访问。

#### 2. 类属性的访问
- 通过类访问：`MyClass.class_variable`
- 通过实例访问：`my_instance.class_variable`

```python
class MyClass:
    class_variable = "This is a class attribute"

# 通过类访问
print(MyClass.class_variable)  # 输出: This is a class attribute

# 通过实例访问
obj = MyClass()
print(obj.class_variable)  # 输出: This is a class attribute
```

#### 3. 类属性的修改
类属性可以通过类名进行修改，但如果通过实例来修改，实际上是为该实例创建了一个新的实例属性，而不会影响原来的类属性。

```python
class MyClass:
    class_variable = "Class level"

# 修改类属性
MyClass.class_variable = "New class level"
print(MyClass.class_variable)  # 输出: New class level

# 通过实例修改类属性实际上创建了实例属性
obj = MyClass()
obj.class_variable = "Instance level"
print(obj.class_variable)  # 输出: Instance level
print(MyClass.class_variable)  # 输出: New class level
```

### 类属性与实例属性的区别
1. **作用范围**:
   - 类属性：定义在类中，属于整个类，所有实例共享。
   - 实例属性：定义在 `__init__` 等实例方法中，属于某个具体实例，每个实例有自己的属性副本。

2. **共享特性**:
   - 类属性：所有实例共享类属性的值，如果类属性发生改变，所有实例的值都会发生变化（前提是没有通过实例单独修改）。
   - 实例属性：每个实例有自己独立的值，修改某个实例的属性不会影响其他实例。

#### 示例：
```python
class MyClass:
    class_variable = "Shared across instances"
    
    def __init__(self, name):
        self.name = name  # 实例属性

# 创建实例
obj1 = MyClass("Object 1")
obj2 = MyClass("Object 2")

# 访问类属性和实例属性
print(obj1.class_variable)  # 输出: Shared across instances
print(obj2.class_variable)  # 输出: Shared across instances

# 修改类属性
MyClass.class_variable = "Updated class variable"
print(obj1.class_variable)  # 输出: Updated class variable
print(obj2.class_variable)  # 输出: Updated class variable

# 修改实例属性
obj1.class_variable = "Instance-specific variable"
print(obj1.class_variable)  # 输出: Instance-specific variable
print(obj2.class_variable)  # 输出: Updated class variable
```

### 何时使用类属性？
- **共享数据**：当某些数据需要在类的所有实例之间共享时（例如，计数器、常量等）。
- **类级别操作**：当某些属性与类相关，而不是与某个具体实例相关时，类属性是合适的选择。

### 相关的 OOP 知识点
1. **封装（Encapsulation）**: 类属性是一种封装数据的方式，数据只与类相关，可以通过类或实例访问，但无法直接从外部修改，除非显式指定。
   
2. **继承（Inheritance）**: 在继承中，类属性的继承是常见的情况，子类可以访问父类的类属性，但也可以覆盖或重新定义类属性。
   
3. **多态（Polymorphism）**: 类属性并不直接涉及多态，但它为类级别提供了一种一致的数据存取方式，可以用于实现多态行为时统一处理类级别的数据。

### 类属性 vs 静态属性
- **类属性**: 属于类并可以通过类或实例访问，属于所有实例共享。
- **静态属性**: 静态方法不依赖于类或实例的属性，它是类中的一个普通函数，但通常与类相关联，可以通过类名调用。

```python
class MyClass:
    class_variable = "I am a class variable"
    
    @staticmethod
    def static_method():
        print("I am a static method")

MyClass.static_method()  # 直接通过类调用静态方法
```


## 类方法

类方法是 Python 中一种特殊的方法，它与普通的实例方法不同，类方法操作的是类本身，而不是类的某个实例。类方法通过类而不是实例来调用，并且通常用于处理与类级别相关的逻辑。了解类方法的作用和用法是 Python 面向对象编程的一个重要知识点，特别是当涉及到类的设计、类级别的操作以及如何使用类和实例之间的关系时。


### 相关知识点：
1. **类的定义**: 如何定义类、类的属性、类的行为。
2. **实例方法 vs 类方法 vs 静态方法**:
   - **实例方法**: 通过实例调用，能够访问实例的属性和方法。
   - **类方法**: 通过类或实例调用，操作类本身，而不是具体的实例。
   - **静态方法**: 通过类或实例调用，但与类和实例无关，仅仅是类中的一个普通函数。

### 类方法的定义和使用：

#### 1. 类方法的定义：
类方法使用 `@classmethod` 装饰器来定义，其第一个参数是 `cls`，代表类本身，而不是实例。类方法通常用于访问或修改类级别的属性。

```python
class MyClass:
    class_variable = "I am a class variable"
    
    @classmethod
    def class_method(cls):
        print(f"Class variable: {cls.class_variable}")

# 调用类方法
MyClass.class_method()  # 输出: Class variable: I am a class variable
```

#### 2. 类方法的调用：
- **通过类调用**: `MyClass.class_method()`
- **通过实例调用**: `my_instance.class_method()`

即使通过实例调用类方法，`cls` 仍然是类本身，而不是实例。

### 3. 实例方法 vs 类方法：
- **实例方法**:
  - 定义：默认传入 `self` 参数，表示当前实例。
  - 操作：可以访问实例的属性和方法。
  
  ```python
  class MyClass:
      def instance_method(self):
          print(f"Instance method called by {self}")
  ```

- **类方法**:
  - 定义：使用 `@classmethod` 装饰器，默认传入 `cls` 参数，表示当前类。
  - 操作：可以访问类的属性和方法，不能访问实例属性。

  ```python
  class MyClass:
      class_variable = "Class variable"
      
      @classmethod
      def class_method(cls):
          print(f"Class method called by {cls}")
  ```

### 4. 何时使用类方法？

- 当需要访问或修改类级别的属性时。
- 当你需要一种与类相关的操作，而不依赖于具体的实例。例如，工厂方法通常是类方法，用来创建类的实例。

### 类方法在面向对象编程中的位置：
- **封装**: 类方法可以作为对类级别数据的封装，避免外部直接操作类属性。

- **代码结构的优化**: 类方法提供了一种明确的方式去区分类相关的逻辑和实例相关的逻辑，使代码更加结构化。

### 示例：类方法在工厂模式中的使用
类方法经常被用来实现**工厂模式**，它允许通过类方法来创建类的实例。

```python
class Pizza:
    def __init__(self, ingredients):
        self.ingredients = ingredients
    
    @classmethod
    def margherita(cls):
        return cls(['mozzarella', 'tomatoes'])
    
    @classmethod
    def pepperoni(cls):
        return cls(['mozzarella', 'tomatoes', 'pepperoni'])

# 使用类方法创建实例
pizza1 = Pizza.margherita()
pizza2 = Pizza.pepperoni()

print(pizza1.ingredients)  # 输出: ['mozzarella', 'tomatoes']
print(pizza2.ingredients)  # 输出: ['mozzarella', 'tomatoes', 'pepperoni']
```



