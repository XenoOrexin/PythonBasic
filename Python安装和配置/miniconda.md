## 为什么使用 miniconda

1. 版本和环境管理

实际开发过程中我们往往需要用到不同版本的 python 环境. 

	比如项目A 需要用到 python3.9 而项目 B 需要使用 python 3.7, 
	而作为开发者为了熟悉新特性我们往往需要在开发电脑上再配置一个最新版本的 python
	
每个环境不仅 python 的版本不同, 内部所用到的包可能也不尽相同. 使用 miniconda 允许我们为每个项目创建独立的 python 环境, 这些环境是完全隔离的, 而且可以在不同的版本之间快速切换. 这样可以避免因为版本不一致导致依赖冲突. 

此外 miniconda 有者自己的包管理器 conda, 他可以自动的处理复杂的依赖关系, 确保安装的包之间相互兼容, 减少手动调试包的版本的时间.

2. 跨平台兼容性

miniconda 在不同的操作系统上可以提供一直的开发体验, 实际开发工作中经常会出现需要在多个操作系统上来回切换的情况, 这时候可以使用 conda 提供较为一致的开发环境体验.

## conda 基础命令操作

在 miniconda 安装完毕后我们可以在命令行中输入:
```sh
conda env list
```

可以得到以下输出, 这是 conda 默认的环境, 但是根据官方文档,不推荐使用默认的环境作为工作的环境, 该环境仅仅用于安装 anaconda conda 和相关的包依赖 
```
# conda environments:
#
base                  *  /opt/miniconda3
```

### 环境管理

#### 创建新的 conda 环境

使用以下的命令创建一个全新的 conda 环境 :

```sh
conda create -n py39 python=3.9
```

`-n` 参数用于指定创建环境的名字, `python=` 则指定该环境使用的 python 的版本, 在执行该命令后, conda 会创建一个基于 python3.9 的新环境.\

继续使用下面的命令查看所有的环境信息:

```
conda env list
```

```
# conda environments:
#
base                  *  /opt/miniconda3
py39                     /opt/miniconda3/envs/py39
```

可以看到 py39 环境已经被创建出来, 路径位于 `/opt/miniconda3/envs/py39` , 我们还可以发现 base 环境对应的路径前有一个 * 符号, 该符号表示这是目前被激活的环境. 

创建环境的时候还可以指定包的版本 :

```sh
conda create -n myenv python=3.11 beautifulsoup4 docutils jinja2=3.1.4 wheel
```

使用 conda 创建环境的语法总结如下:

其中 `python=<VERSION> `  和 `<PACKAGE>=<VERSION>` 都是可选的

```
conda create -n <ENV_NAME> python=<VERSION> <PACKAGE>=<VERSION>
```

#### 激活和停止环境

在完成 py39 环境的创建后, 使用下面的命令激活:
```
conda activate py39
```

下面的命令也可以查看 conda 的环境列表:

```
conda info --envs
```

```
# conda environments:
#
base                     /opt/miniconda3
myenv                    /opt/miniconda3/envs/myenv
py39                  *  /opt/miniconda3/envs/py39
```

此时显示 py39 环境已经被激活.

推荐在当前的环境中完成工作后关闭这个环境, 使用 deactivate 来完成这个任务:

```
conda deactivate
```

```
# conda environments:
#
base                  *  /opt/miniconda3
myenv                    /opt/miniconda3/envs/myenv
py39                     /opt/miniconda3/envs/py39
```

可以看到激活的环境又回到了最初的 base 环境.


## IDE 中使用 conda 作为python 环境



