## 基本数据类型
## 字符串格式化输出
Python 中有多种字符串格式化输出的方式，以下是几种常见的方法：

### 1. **百分号 (`%`) 格式化**
这是 Python 中比较早期的字符串格式化方式，类似于 C 语言的 `printf` 风格。

#### 示例：
```python
name = "Alice"
age = 30
formatted_string = "My name is %s and I am %d years old." % (name, age)
print(formatted_string)
```
**输出**：
```
My name is Alice and I am 30 years old.
```

#### 常用格式化符号：
- `%s`：字符串
- `%d`：整数
- `%f`：浮点数（可指定精度，如 `%.2f` 表示保留 2 位小数）
- `%x`：十六进制整数

### 2. **`str.format()` 方法**
`str.format()` 是 Python 3 推出的格式化方法，功能更加灵活强大。

#### 示例：
```python
name = "Bob"
age = 25
formatted_string = "My name is {} and I am {} years old.".format(name, age)
print(formatted_string)
```
**输出**：
```
My name is Bob and I am 25 years old.
```

#### 位置参数和关键字参数：
- 可以通过位置参数或关键字参数来指定格式化内容：
```python
# 位置参数
formatted_string = "My name is {0} and I am {1} years old.".format(name, age)
# 关键字参数
formatted_string = "My name is {name} and I am {age} years old.".format(name="Charlie", age=35)
```

#### 指定格式：
```python
pi = 3.14159
formatted_string = "Pi is approximately {:.2f}".format(pi)
print(formatted_string)
```
**输出**：
```
Pi is approximately 3.14
```

### 3. **`f-string` (格式化字符串字面量)**
`f-string` 是 Python 3.6 引入的一种格式化方式，性能更高，且更为简洁。它允许直接在字符串前添加 `f` 或 `F`，并在字符串中使用 `{}` 插入变量。

#### 示例：
```python
name = "Dave"
age = 40
formatted_string = f"My name is {name} and I am {age} years old."
print(formatted_string)
```
**输出**：
```
My name is Dave and I am 40 years old.
```

#### 表达式支持：
`f-string` 可以在 `{}` 内部放入任意的表达式：
```python
formatted_string = f"In 5 years, I will be {age + 5} years old."
print(formatted_string)
```
**输出**：
```
In 5 years, I will be 45 years old.
```

#### 指定格式：
```python
pi = 3.14159
formatted_string = f"Pi is approximately {pi:.2f}"
print(formatted_string)
```
**输出**：
```
Pi is approximately 3.14
```

### 4. **`Template` 模板字符串**
`Template` 是 Python `string` 模块中的类，允许通过占位符 `$` 来进行字符串替换，适用于对安全性有要求的场景（比如用户输入内容不应该执行表达式）。

#### 使用方法：
```python
from string import Template

template = Template("My name is $name and I am $age years old.")
formatted_string = template.substitute(name="Eve", age=28)
print(formatted_string)
```
**输出**：
```
My name is Eve and I am 28 years old.
```

#### 安全性：
`Template` 字符串不会执行表达式，因此适合在处理外部输入时使用。

### 5. **手动拼接字符串**
虽然不推荐，但通过手动拼接也是一种方式，通常使用 `+` 运算符。

#### 示例：
```python
name = "Frank"
age = 22
formatted_string = "My name is " + name + " and I am " + str(age) + " years old."
print(formatted_string)
```
**输出**：
```
My name is Frank and I am 22 years old.
```

### **总结**
不同的字符串格式化方式在不同的场景中适用：

- **`%` 格式化**：简单快速，但灵活性较差，适合老式代码。
- **`str.format()`**：功能强大，适用于需要复杂格式化的场景。
- **`f-string`**：最推荐的方式，简洁高效，适用于 Python 3.6 及以上。
- **`Template`**：适用于对安全性要求较高的场景，不支持表达式插值。

### **推荐使用：`f-string`**
在 Python 3.6 及以上的版本中，`f-string` 是最简洁且高效的格式化方式，尤其适合日常开发。

## 函数

### 一些零碎知识点
#### Python 真值测试 (truthy 和 falsy)

```

def get_formatted_name_type1(first_name, last_name, middle_name=''):

if middle_name:

full_name = f"{first_name} {middle_name} {last_name}"

else:

full_name = f"{first_name} {last_name}"

return full_name.title()

```

上面的代码中, 形参 `middle_name` 的默认值是一个空字符串, 但是仍可以用于下面的 if 语句的条件判断, 这对于习惯使用强类型语言的开发者可能造成一些困扰

##### 为什么 `if middle_name:` 可以用于条件判断？

1. **Falsy 值**： 在 Python 中，某些值在布尔上下文中会被视为 `False`，即“falsy”。这些值包括：
    
    - `None`
    - 空字符串 `''`
    - 数字 `0`
    - 空的容器类型（如空列表 `[]`、空元组 `()`、空字典 `{}` 等）
    
    所以，在上面的代码中，`middle_name` 默认为空字符串 `''`，空字符串在 Python 中属于“falsy”值，因此在 `if middle_name:` 这个条件判断中，空字符串会被视为 `False`。
    
2. **Truthy 值**： 与“falsy”相反，非空的字符串、非零的数字、非空的容器等都被视为“truthy”，即在条件判断中会被视为 `True`。例如，如果 `middle_name` 是非空字符串（如 `"John"`），则 `if middle_name:` 会返回 `True`。

所以上面的代码实际上是不会报错的, 在 Python 中，条件判断语句 `if middle_name:` 的行为是基于 Python 对“**真值测试**”（truthy 和 falsy）的处理方式。尽管 `middle_name` 不是一个布尔值，但 Python 会自动将它转换为布尔值来进行条件判断。

