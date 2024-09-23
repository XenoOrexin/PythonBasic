
## 下载和安装 Cursor

Cursor 的安装依赖 vscode , 确保你的电脑已经安装并配置了 vscode

Cursor 需要账号, 可以使用 google 账户直接登录, 推荐直接使用 google 账号登录 Cursor 

Cursor 官网 : https://www.cursor.com/

![[Pasted image 20240923093709.png]]

下载后直接安装即可

## Cursor 配置

### 导入 vscode 的插件和配置

Cursor 完全基于 vscode, 可以直接从 vscode 导入对应的插件和配置

![[Pasted image 20240923094022.png]]

安装和登录完毕后在 Settings -> General -> VS Code Import 选项下点击 Import 即可

### 配置 Chat AI 返回语言为中文

 ![[Pasted image 20240923094240.png]]
在 Rules for AI 部分输入如下内容, Cursor 会默认将中文作为 chat 的返回语言

### 配置自定义模型 

![[Pasted image 20240923094415.png]]

Cursor 非会员能够使用的 chat 次数有限, 推荐配置自己的大模型 API key , 这里演示下如何配置 deepseek coder 和 claude 3.5 的 API key

#### deepseek

比较廉价的国内大模型 API key, 适合用于日常的编程推理工作, 配置流程如下:

1.  打开Cursor Setting -> Models 拖到 OpenAI API key

![[Pasted image 20240923094559.png]]

2. 在 Override OpenAI Base URL 部分输入下面的地址
```
https://api.deepseek.com/beta
```

3. 登录 deepseek 并创建自己的 API key

![[Pasted image 20240923094921.png]]

输入任意的 API key 名然后 create
![[Pasted image 20240923095007.png]]

copy 并保存下面的 API key 到本地文件中

![[Pasted image 20240923095108.png]]

在 Cursor 中配置 API key, 下图的红框部分输入你的 API key , 输入完毕后点击 Verify, 如果没有任何报错信息则配置成功
![[Pasted image 20240923095151.png]]
4. 关闭所有的其他模型并创建名为 `deepseek-coder` 的模型

![[Pasted image 20240923095357.png]]
5. 开启 deepseek-coder 模型
![[Pasted image 20240923095435.png]]

6. 通过 ctrl + shift + l 在侧边栏打开 chat 界面, 选择 deepseek-coder 模型, 并输入 hello 进行测试

![[Pasted image 20240923095613.png]]

7. 如果正常的返回则表示安装完成
![[Pasted image 20240923095734.png]]


## 如何使用

自己去看文档 : https://docs.cursor.com/get-started/migrate-from-vscode

## 一些问题汇总

### 关于 windows 使用拨号上网无法使用 google

#### 确保拨号连接名为英文
检查自己的宽带连接名是否是中文, 如果是则需要删除该连接然后创建一个新的宽带连接, 连接名使用英文. 我这里使用的是 `pppoe` 


#### 调整拨号连接的跃点


#### 手动为拨号连接设置代理


#### 手动为浏览器设置默认端口号


