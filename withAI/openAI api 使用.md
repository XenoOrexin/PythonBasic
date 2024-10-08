
调用 ChatGPT API 的常见参数主要用于指定模型的行为、对话内容以及其他相关设置。以下是一些常见的参数：

1. **model**：指定要使用的模型。例如：`"gpt-4"`, `"gpt-3.5-turbo"`等。

2. **messages**：必选参数，表示对话的内容。这个参数包含一个消息列表，每条消息是一个字典，格式为：
   ```json
   {
     "role": "system" | "user" | "assistant",
     "content": "message content here"
   }
   ```
   - `"role"`：消息的角色，包括：
     - `"system"`：用于提供模型的一些初始指令或设定场景。
     - `"user"`：用户输入的消息。
     - `"assistant"`：模型的回复。
   - `"content"`：消息的具体内容。

3. **max_tokens**：指定生成回复的最大 token 数。较大的 `max_tokens` 值会生成更长的回复，但也会消耗更多的资源。

4. **temperature**：控制生成文本的随机性。值的范围是 0 到 2，值越高生成的文本越随机。常见值为：
   - `0`：确定性的回答，生成的文本会更一致。
   - `1`：生成较有创意的回答。
   - `2`：生成更随机的回答。

5. **top_p**：另一种控制生成文本多样性的方式，称为“核采样”。`top_p` 的值越小，生成的文本越保守。

6. **n**：指定生成多少条回复。默认生成 1 条回复。

7. **stop**：设置一个或多个停止生成的条件。例如，当模型生成到某个特定字符串时停止生成。

8. **logprobs**：返回每个生成的 token 对应的概率，值为 `0` 到 `5`，表示返回生成文本中前 `n` 个 token 的概率。

9. **stream**：如果设置为 `true`，API 将通过流的方式返回结果，这样可以实时获取模型生成的回复。

10. **presence_penalty**：控制模型生成与之前内容不相关的新内容。范围是 -2.0 到 2.0，较高的值鼓励生成新内容。

11. **frequency_penalty**：控制模型减少生成重复内容的概率，范围是 -2.0 到 2.0。

12. **user**：可选参数，用户标识符，用于区分多个用户的请求。

示例调用：
```json
{
  "model": "gpt-4",
  "messages": [
    { "role": "system", "content": "You are a helpful assistant." },
    { "role": "user", "content": "Tell me a joke." }
  ],
  "max_tokens": 50,
  "temperature": 0.7
}
```

这些参数可以根据实际需求调整，以实现更符合特定应用场景的对话。

## 调用 API 的一些实践

### 执行翻译任务

#### 日常翻译




#### 学术文档翻译

prompt 样例： 

下面是一个基本的用于翻译学术文件的请求

```python
response = client.chat.completions.create(
    model="gpt-4",
    messages=[
        {
            "role": "system",
            "content": "You are a highly skilled translation engine with expertise in academic paper translation. Your function is to translate academic texts into the {{to}}, ensuring the accurate translation of complex concepts and specialized terminology without altering the original academic tone or adding explanations."
        },
        {
            "role": "user",
            "content": "<source text>"  # Pass the source text dynamically here
        }
    ],
    max_tokens=1500,  # Keep max_tokens as high as necessary for longer translations
    temperature=0.7,  # Lower temperature for more controlled, formal translations
    stream=False  
)

# Optionally, add error handling for API failures
try:
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[
            {
                "role": "system",
                "content": "You are a highly skilled translation engine..."
            },
            {
                "role": "user",
                "content": source_text  # Make source_text a variable
            }
        ],
        max_tokens=1500,
        temperature=0.7,
        stream=False
    )
except Exception as e:
    print(f"Error occurred: {e}")

```

在上面请求的基础上， 可以依据 co-star 元组对上面的内容进一步优化：
```python
messages = [
    {
        "role": "system",
        "content": (
            "You are a translation engine specialized in academic papers. "
            "Your task is to translate the provided academic text into {{chinese}} "
            "with high accuracy. You must retain the original academic tone, "
            "use specialized terminology precisely, and ensure no alterations to the meaning. "
            "Do not add explanations, interpretations, or summarize content. "
            "Focus on delivering a faithful, contextually accurate translation."
        )
    },
    {
        "role": "user",
        "content": source_text  # Source text as a variable
    }
]

```

CoSTAR解释：
清晰：明确指出引擎正在翻译学术文本。
客观：任务明确——将文本翻译为目标语言（{{to}}）。
具体：模型被指示保持语调和准确性，不添加或省略信息。
任务导向：专注于翻译文本，避免额外任务如总结。
可操作：给出了具体不做的事情（如，不改变意义或语调）。
结果导向：结果是精确、忠实的学术翻译。