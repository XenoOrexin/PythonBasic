
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

