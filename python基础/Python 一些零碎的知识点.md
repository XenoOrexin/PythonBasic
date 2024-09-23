
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

