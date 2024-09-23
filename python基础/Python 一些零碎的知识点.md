
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



## 真值测试
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

## Python 读取大文件的处理方式

对于超过机器内存限制的超大文件, 往往需要针对文件进行切分然后再进行处理, 下面是 Python 中主流的切分文件进行处理的形式

### 方法 1: 按行逐步读取
如果你的文件是文本文件，逐行读取是一个简单而有效的方式，避免将整个文件加载到内存中。

```python
def process_line(line):
    # 在这里处理每一行数据
    print(line.strip())

# 逐行读取文件并处理
with open('large_file.txt', 'r') as file:
    for line in file:
        process_line(line)
```

#### 优势和劣势
* 优势
代码逻辑非常简单且易于理解

* 不足
**按行读取文件**在默认情况下是**同步**的。在Python中，使用常见的文件读取操作（例如 `open()` 函数）按行读取文件时，操作是顺序执行的，意味着每次读取一行都会等待当前行读取和处理完成后，才会继续读取下一行。这种操作是同步的，单线程执行

### 方法 2: 按固定大小的块读取
对于二进制文件或者按字节处理的情况，可以按固定大小的块读取文件，这样能够更灵活地控制每次读取的数据量。

```python
def process_chunk(chunk):
    # 处理每个块数据
    print(chunk)

# 每次读取1MB的块数据
chunk_size = 1024 * 1024  # 1MB
with open('large_file.bin', 'rb') as file:
    while True:
        chunk = file.read(chunk_size)
        if not chunk:  # 读取完毕
            break
        process_chunk(chunk)
```

这种方法特别适合处理二进制文件或者你需要按块处理的情况。你可以根据可用内存或具体处理逻辑调整 `chunk_size`。

### 方法 3: 通过 `iter` 按块读取
Python 的 `iter` 函数允许通过自定义读取器进行逐步读取。例如，可以用来创建一个每次读取固定字节数的迭代器。

```python
def read_in_chunks(file_object, chunk_size=1024):
    """逐块读取文件，每次返回指定大小的数据"""
    while True:
        data = file_object.read(chunk_size)
        if not data:
            break
        yield data

with open('large_file.bin', 'rb') as file:
    for chunk in read_in_chunks(file):
        process_chunk(chunk)
```

通过这种方式，文件被分成大小可控的块并逐步处理。

### 方法 4: 使用 `mmap` 处理超大文件
`mmap` 是 Python 中的内存映射模块，它可以将文件的一部分映射到内存中，从而可以像操作内存一样操作文件内容。虽然底层仍是按块处理，但在用户层面，文件可以像是已经被整体加载到内存中一样访问。

```python
import mmap

def process_data(data):
    # 处理数据
    print(data)

with open('large_file.txt', 'r+b') as file:
    # 内存映射文件，访问模式为只读
    mmapped_file = mmap.mmap(file.fileno(), 0)
    
    # 逐行读取并处理
    for line in iter(mmapped_file.readline, b""):
        process_data(line)

    # 关闭内存映射
    mmapped_file.close()
```

`mmap` 适合在需要频繁访问文件中不同部分时使用，但在非常大文件的情况下，仍然要注意操作系统的内存限制。
### 方法 5: 文件切片 (Split)
对于一些场景，可能需要将大文件物理上切分成多个小文件。可以使用 Python 的文件处理代码或系统命令（如 `split`）来完成。

使用 Python 切分文件：

```python
def split_file(input_file, chunk_size):
    with open(input_file, 'rb') as file:
        chunk_count = 0
        while True:
            chunk = file.read(chunk_size)
            if not chunk:
                break
            chunk_filename = f'{input_file}_part_{chunk_count}'
            with open(chunk_filename, 'wb') as chunk_file:
                chunk_file.write(chunk)
            chunk_count += 1

split_file('large_file.bin', 1024 * 1024)  # 每次切分1MB
```

这种方法将大文件分成多个小文件，适合那些需要分布式处理或在不同系统中分割文件的情况。

## python 写文件的参数明细

在 Python 中，使用内置的 `open()` 函数来打开文件时，你可以指定多个参数来控制文件的读取和写入方式。以下是 `open()` 函数常见的参数，尤其是与**写文件**相关的参数：

### 1. `file`（文件名）
   - **作用**：要打开的文件的路径或文件名。
   - **类型**：`str` 或 `pathlib.Path`
   - **示例**：`open('example.txt', 'w')`

### 2. `mode`（模式）
   - **作用**：定义文件的打开模式，决定文件是以只读、写入、追加等方式打开。
   - **类型**：`str`
   - **常见的模式**：
     - `'w'`：写入模式。如果文件已存在，则清空文件。如果文件不存在，则创建新文件。
     - `'a'`：追加模式。如果文件已存在，则在文件末尾追加内容；如果文件不存在，则创建新文件。
     - `'x'`：创建新文件并写入。如果文件已存在，则引发 `FileExistsError`。
     - `'b'`：以二进制模式打开文件。通常与写入模式（如 `'wb'`）组合使用。
     - `'t'`：以文本模式打开文件（默认）。通常与写入模式（如 `'wt'`）组合使用。
     - `'+'`：更新模式。允许同时进行读写操作。可与 `'r+'`、`'w+'` 或 `'a+'` 组合使用。
   
   - **示例**：
     - `open('example.txt', 'w')`：以文本模式打开文件，进行写入操作（如果文件存在则覆盖）。
     - `open('example.txt', 'wb')`：以二进制模式打开文件，进行写入操作。
     - `open('example.txt', 'a')`：以文本模式打开文件，进行追加操作。

### 3. `buffering`（缓冲区大小）
   - **作用**：设置文件的缓冲模式。
   - **类型**：`int`
   - **默认值**：默认使用全缓冲（文本文件缓冲大小为系统默认值；二进制文件根据块大小自动确定）。
   - **选项**：
     - `0`：不使用缓冲（仅适用于二进制模式）。
     - `1`：使用行缓冲（仅适用于文本模式）。
     - 大于 `1` 的整数：指定固定大小的缓冲区（单位是字节）。
   
   - **示例**：
     - `open('example.txt', 'w', buffering=1)`：启用行缓冲。
     - `open('example.bin', 'wb', buffering=0)`：无缓冲写入二进制文件。

### 4. `encoding`（编码）
   - **作用**：指定文本文件的字符编码。该参数只适用于文本模式。
   - **类型**：`str`
   - **默认值**：`None`（使用系统默认编码）。
   - **常见的编码**：
     - `'utf-8'`：常用的 UTF-8 编码（推荐用于文本文件）。
     - `'ascii'`：ASCII 编码。
     - `'latin-1'`：Latin-1 编码（ISO-8859-1）。

   - **示例**：
     - `open('example.txt', 'w', encoding='utf-8')`

### 5. `errors`（编码错误处理）
   - **作用**：指定在编码或解码过程中遇到错误时如何处理。
   - **类型**：`str`
   - **选项**：
     - `'strict'`：默认行为，遇到错误时引发 `ValueError`。
     - `'ignore'`：忽略编码错误。
     - `'replace'`：用替代字符（通常是 `'?'`）替换无法编码的字符。
     - `'backslashreplace'`：将非法字符替换为 Unicode 转义序列。
   
   - **示例**：
     - `open('example.txt', 'w', encoding='utf-8', errors='ignore')`

### 6. `newline`（换行符处理）
   - **作用**：控制换行符的处理方式，适用于文本模式。
   - **类型**：`str` 或 `None`
   - **选项**：
     - `None`（默认）：不同操作系统的默认换行符行为。
     - `''`：不进行任何自动换行处理（即只使用 `\n`）。
     - `'\n'`：指定使用 Unix 换行符（换行符为 `\n`）。
     - `'\r\n'`：指定使用 Windows 换行符（换行符为 `\r\n`）。

   - **示例**：
     - `open('example.txt', 'w', newline='\n')`：指定使用 Unix 风格的换行符。

### 7. `closefd`（文件描述符关闭）
   - **作用**：控制在文件关闭时是否关闭底层的文件描述符（仅当 `file` 是文件描述符时有效）。
   - **类型**：`bool`
   - **默认值**：`True`（关闭文件时关闭文件描述符）。
   - **示例**：
     - `open('example.txt', 'w', closefd=False)`

### 8. `opener`（自定义打开器）
   - **作用**：允许指定自定义的文件打开器。可以传递一个函数，该函数必须返回一个打开的文件描述符。
   - **类型**：`callable`
   - **示例**：
     - `open('example.txt', 'w', opener=my_custom_opener)`

---

### 总结示例：
```python
# 按 UTF-8 编码写入文件，并忽略编码错误
with open('example.txt', 'w', encoding='utf-8', errors='ignore') as f:
    f.write('This is an example.\n')

# 以二进制模式写入文件
with open('example.bin', 'wb') as f:
    f.write(b'\x00\x01\x02\x03')
```

## python 魔法方法

## 操作列表

在 Python 中，操作 `list`（列表）有很多常见的方法和技巧。以下是一些常用的列表操作方式，涵盖创建、修改、访问、遍历等多方面操作：

### 1. **创建列表**

```python
# 创建空列表
my_list = []

# 创建包含元素的列表
my_list = [1, 2, 3, 4, 5]
```

### 2. **访问列表元素**

- **通过索引访问**（索引从 `0` 开始）

```python
# 访问第一个元素
first_item = my_list[0]

# 访问最后一个元素
last_item = my_list[-1]
```

- **切片**（从列表中提取一个子列表）

```python
# 访问索引 1 到 3 的元素 (不包括 3)
sub_list = my_list[1:3]

# 访问从索引 2 开始的所有元素
sub_list = my_list[2:]

# 访问前 3 个元素
sub_list = my_list[:3]
```

### 3. **修改列表**

- **通过索引修改元素**

```python
my_list[0] = 10  # 修改第一个元素为 10
```

- **通过切片赋值**

```python
my_list[1:3] = [20, 30]  # 修改索引 1 到 2 的元素
```

### 4. **添加元素**

- **`append()`**：在列表末尾添加单个元素

```python
my_list.append(6)
```

- **`insert()`**：在指定位置插入元素

```python
my_list.insert(2, 15)  # 在索引 2 处插入 15
```

- **`extend()`**：将另一个列表的元素添加到当前列表末尾

```python
my_list.extend([7, 8, 9])
```

### 5. **删除元素**

- **`remove()`**：删除指定值的第一个匹配项

```python
my_list.remove(3)  # 删除值为 3 的第一个元素
```

- **`pop()`**：删除并返回指定索引处的元素（默认删除最后一个元素）

```python
last_item = my_list.pop()  # 删除并返回最后一个元素
item_at_index_2 = my_list.pop(2)  # 删除索引 2 处的元素
```

- **`del`**：通过索引删除元素或切片

```python
del my_list[0]  # 删除第一个元素
del my_list[1:3]  # 删除索引 1 到 2 的元素
```

- **`clear()`**：清空列表

```python
my_list.clear()
```

### 6. **查找元素**

- **`index()`**：查找某个元素的索引

```python
index_of_5 = my_list.index(5)  # 找到 5 的索引
```

- **`in`**：检查元素是否在列表中

```python
is_in_list = 5 in my_list  # 检查 5 是否在列表中
```

### 7. **遍历列表**

- **`for` 循环**

```python
for item in my_list:
    print(item)
```

- **`enumerate()`**：获取索引和值

```python
for index, item in enumerate(my_list):
    print(index, item)
```

### 8. **列表排序**

- **`sort()`**：原地排序列表

```python
my_list.sort()  # 升序
my_list.sort(reverse=True)  # 降序
```

- **`sorted()`**：返回排序后的新列表，不改变原列表

```python
sorted_list = sorted(my_list)
```

### 9. **列表反转**

- **`reverse()`**：原地反转列表

```python
my_list.reverse()
```

- **`reversed()`**：返回反转后的新迭代器，不改变原列表

```python
reversed_list = list(reversed(my_list))
```

### 10. **列表推导式**

- **列表推导式**：通过表达式创建列表

```python
squares = [x**2 for x in range(10)]  # 创建包含 0 到 9 的平方的列表
```

### 11. **统计和计数**

- **`count()`**：统计某个元素在列表中出现的次数

```python
count_of_5 = my_list.count(5)
```

- **`len()`**：获取列表的长度

```python
length = len(my_list)
```

### 12. **复制列表**

- **浅复制**：使用 `copy()` 或切片 `[:]`

```python
new_list = my_list.copy()
new_list = my_list[:]
```

- **深复制**：使用 `copy` 模块中的 `deepcopy()`

```python
import copy
new_list = copy.deepcopy(my_list)
```

### 13. **合并列表**

- **通过 `+` 操作符**

```python
merged_list = my_list + another_list
```

- **通过 `extend()`**

```python
my_list.extend(another_list)
```

### 14. **转置列表**

- **通过 `zip()` 转置二维列表**

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
transposed_matrix = list(zip(*matrix))  # 转置矩阵
```

### 总结

Python 提供了丰富的操作列表的方法，包括基本的添加、删除、排序、查找、切片、遍历等操作。通过列表推导式、排序和查找等高级操作，你可以灵活处理各种数据分析或处理任务。

## set 集合存储元素

自定义对象可以放入 Python 的 `set` 中，前提是该对象是**可哈希的**。Python 使用哈希值来判断集合元素的唯一性，因此任何放入集合的对象必须能够生成一个稳定的哈希值，并且对象应该支持相等性比较（即实现 `__hash__()` 和 `__eq__()` 方法）。

### 默认情况下的对象
默认情况下，Python 中的自定义类的实例是可哈希的，除非你明确覆盖了哈希行为。默认哈希值基于对象的内存地址。因此，如果你创建一个自定义类，而不修改其默认行为，该类的对象可以直接放入集合中。

例如：

```python
class MyClass:
    def __init__(self, value):
        self.value = value

# 创建对象
obj1 = MyClass(10)
obj2 = MyClass(20)
obj3 = MyClass(10)

# 创建一个集合并添加对象
s = {obj1, obj2, obj3}

# 打印集合中对象的数量
print(len(s))  # 输出 3，因为它们有不同的内存地址
```

在这个例子中，`obj1` 和 `obj3` 尽管 `value` 相同，但它们被视为不同的对象，因为它们的内存地址不同，哈希值也是不同的。

### 自定义哈希和相等性比较
如果希望基于对象的属性来判断它们是否相等（即对象的相等性是基于内容而不是内存地址），你需要为类实现 `__hash__()` 和 `__eq__()` 方法。这样你就可以将基于属性相等的对象放入集合中。

例如：

```python
class MyClass:
    def __init__(self, value):
        self.value = value

    def __hash__(self):
        # 基于对象的 'value' 属性生成哈希值
        return hash(self.value)

    def __eq__(self, other):
        # 两个对象如果 'value' 属性相同，则认为它们相等
        return isinstance(other, MyClass) and self.value == other.value

# 创建对象
obj1 = MyClass(10)
obj2 = MyClass(20)
obj3 = MyClass(10)

# 创建一个集合并添加对象
s = {obj1, obj2, obj3}

# 打印集合中对象的数量
print(len(s))  # 输出 2，因为 obj1 和 obj3 被认为是相等的
```

在这个例子中，`obj1` 和 `obj3` 被认为是相等的（因为它们的 `value` 属性相同），因此只会将其中一个放入集合中。

### 重要提示：
- `__hash__()` 方法的返回值应该始终是一个整数，并且在对象的生命周期中应该保持不变。
- `__eq__()` 方法应该实现逻辑上的相等性比较，决定两个对象是否被视为相同。
- 如果你重写了 `__eq__()` 方法，通常你也需要重写 `__hash__()`，以确保相等的对象具有相同的哈希值。

### 总结：
- **对象可以放入集合中**，前提是它们是**可哈希的**。
- 如果你希望基于对象的内容（属性）判断是否相等，而不是基于内存地址，则需要实现 `__hash__()` 和 `__eq__()` 方法。