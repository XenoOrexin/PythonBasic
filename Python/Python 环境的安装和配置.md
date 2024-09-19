
## TODO 基本安装

python 安装包下载地址 : https://www.python.org/downloads/


### 在 windows 上安装 Python 环境

从官方网站的下载默认的版本 : 

![[Pasted image 20240919161419.png]]

如果需要下载特定版本号的 python 安装包, 可以从下面 sperific release 部分选择自己需要的版本 :  

![[Pasted image 20240919161544.png]]


### TODO 在 Mac 上安装 Python 环境



### 在 linux 上安装 Python 环境 (以 Wsl2 为例)

由于目前服务器的操作系统主流是 Linux ，本地使用 Linux，可以保证本地开发环境与服务器环境一致，减少环境差异导致的问题。而且相比 Windows, Linux 提供了更加丰富的包管理工具  (APT YUM ) 和命令行工具 (ZSH) . 目前 Windows 已经在内部集成 WSL（Windows Subsystem for Linux，Windows 的 Linux 子系统）, 目前用户可以直接在 Windows 上运行 Linux 上的原生命令行和应用程序, 而无需安装虚拟机或者启动双系统.

#### 安装和配置 WSL2 以 Windows11 为例

安装 WSL 需要你的系统至少是 Windows10 的2004 或者更高的版本 (Build 19041 and higher) 或者是 Windows11 操作系统.

##### 启动 Windows 功能

1 在开始菜单的搜索页面中输入控制面板或者 `control panel` 进入控制面板

![[Pasted image 20240919164110.png]]

2 在搜索框中检索程序和功能:

![[Pasted image 20240919164230.png]]

3 进入启用或关闭 windows 功能

![[Pasted image 20240919164328.png]]

4 启用**适用于 Linux 的 Windows 子系统**和 **Virtual Machine Platform** (部分系统可能显示为 **虚拟机平台**) , 在勾选功能后安装服务并按照提示重新启动电脑


![[Pasted image 20240919164557.png]]

5 重启完毕后如果在文件管理系统中出现 Linux 的图标, 表示 WSL 功能已经正常启动

![[Pasted image 20240919164937.png]]


##### TODO 配置wsl

##### 安装 Ubuntu 

在 windows 应用商店搜索 Ubuntu , 选择自己需要的版本进行安装即可, 我这里选择的是 Ubuntu 22.04 这个版本进行安装

![[Pasted image 20240919165616.png]]

安装完成后打开 Ubuntu , 会要求设置一个用户名和密码, 用户名不可为`root`因为默认已存在`root`用户, 密码需要输入两次, 第二次为确认密码

然后配置对应的 root 密码 : 

```sh
sudo passwd root
```

系统会要求输入三次密码, 第一次为当前用户的密码, 第二次和第三次为 root 用户的密码. 完成密码的配置后可以关闭 Ubuntu.

##### 迁移 Ubuntu 至其他盘 (可选)

考虑到 Windows 的传统使用习惯我们会对硬盘进行分盘, 给 C 盘的预留空间往往有限. 而我们在子系统中进行的环境配置操作或让子系统所占用的硬盘空间会不断膨胀, 所以为了减少 C 盘的压力可以考虑把 Ubuntu 子系统迁移到其他的盘符.

1. 在迁移 Ubuntu 前需要确保子系统已经处于关闭的状态 : 

```sh
wsl -l -v
```

![[Pasted image 20240919170750.png]]

如果 Ubuntu-22.04 的状态目前处于 Running , 使用下面的命令关闭 Ubuntu 子系统, 确保子系统处于`Stopped` 状态 :

```sh
wsl --shutdown
```

![[Pasted image 20240919171017.png]]

2. 导出镜像文件

	需要注意:
	转移子系统之前需要先在目标的盘符创建对应的目录 我的目录是 D:\wsl\images

```sh
wsl --export Ubuntu-22.04 D:\wsl\images\Ubuntu-22.04.tar
```

- `--export` 为导出选项
- `Ubuntu-22.04` 为子系统名称，对应 `wsl -l -v` 查询出的子系统名称, 需要填写正确
- `D:\wsl\images\Ubuntu-22.04.tar` 为导出路径，文件名随意

3. 注销当前的子系统

```sh
wsl --unregister Ubuntu-22.04
```

4. 导入 Ubuntu-22.04 镜像并挂载存储系统至 D 盘：  

名字还是为：Ubuntu-22.04

```sh
wsl --import Ubuntu-22.04 D:\wsl\Ubuntu-22.04 D:\wsl\images\Ubuntu-22.04.tar
```

5. 设置默认的用户

在移动盘符后默认的用户会变成 root , 需要重新设置默认用户为创建 wsl 子系统时创建的用户.

```sh
ubuntu2204.exe config --default-user 用户名
```

以上操作完成后就可以在 `D:\wsl\Ubuntu-22.04` 中看到存储系统已经被挂载到了该路径下。

![[Pasted image 20240919172043.png]]

以后在该子系统下所有的文件操作都不会影响 C 盘的存储空间了，并且该操作还可以当作快照来保存你的子系统状态，方便以后还原。




#### 在 WSL2 ubuntu 子系统上安装开发环境









## conda 环境的安装和配置




