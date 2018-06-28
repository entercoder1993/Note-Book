# Pro Git学习笔记

[Git简介](## Git简介)
[安装Git](## G安装Git)
[初次运行Git前的配置](## 初次运行Git前的配置)
[Git基础](## Git基础)
[Git分支](## Git分支)
## Git简介

1. 直接记录快照，而非差异比较
2. 近乎所有操作都是本地执行
3. Git保证完整性
4. Git一般只添加数据
5. 三种状态
    * **以提交** -- 已提交表示数据已经安全的保存在本地数据库中
    2. **已修改** -- 修改了文件，但还没保存到数据库中
    3. **已暂存** -- 对一个已修改的文件的当前版本做了标记，使之包含在下次提交的快照中。
6. 工作区域
    * **Git仓库** -- 用来保存项目的元数据和对象数据库的地方，从其他计算基金克隆仓库时，拷贝的就是这里的数据
    2. **工作目录** -- 对项目的某个版本独立提取出来的内容。这些从 Git 仓库的压缩数据库中提取出来的文件，放在磁盘 上供你使用或修改。
    3. **暂存区域** -- 暂存区域是一个文件，保存了下次将提交的文件列表信息，一般在 Git 仓库目录中。 有时候也被称作`‘索 引’'，不过一般说法还是叫暂存区域。![](https://ws1.sinaimg.cn/large/0079wTXjgy1fsmpcjuov0j30jz0b1taa)




      
## 安装Git
* Linux上安装

```
$ sudo yum install git
    
$ sudo apt-get install git
```

* Mac上安装
安装Xcode Command Line Tools

* Windows上安装
[Git官网](git-scm.com/download/win)

* 源代码安装
从源码安装Git，需要安装Git以来的库：curl、zlib、openssl、expat和libiconv

```
$ sudo yum install curl-devel expat-devel gettext-devel \ openssl-devel zlib-devel 
$ sudo apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \ libz-dev libssl-dev
```
为了能够添加更多格式的文档（如 doc, html, info），你需要安装以下的依赖包：

```
$ sudo yum install asciidoc xmlto docbook2x 
$ sudo apt-get install asciidoc xmlto docbook2x
```
[下载Git的tar包](https://www.kernel.org/pub/software/scm/git)

```
$ tar -zxf git-2.0.0.tar.gz 
$ cd git-2.0.0 $ make configure $ ./configure --prefix=/usr 
$ make all doc info 
$ sudo make install install-doc install-html install-info
```
使用Git来获取Git的升级

```
git clone git://git.kernel.org/pub/scm/git/git.git
```

## 初次运行Git前的配置
### 三个配置变量
每一个级别覆盖上一级别的配置
1. `/etc/gitconfig` 文件: 包含系统上每一个用户及他们仓库的通用配置。 如果使用带有 --system 选项的 git config 时，它会从此文件读写配置变量。
2. `~/.gitconfig` 或 ~/.config/git/config 文件：只针对当前用户。 可以传递 --global 选项让 Git 读写此文件。
3. `.git/config` 当前使用仓库的 Git 目录中的 config 文件（就是 .git/config）：针对该仓库。

> 在Windows 系统中，Git 会查找 $HOME 目录下（一般情况下是 C:\Users\$USER）的 .gitconfig 文件。 Git 同样也会寻找 /etc/gitconfig 文件，但只限于 MSys 的根目录下，即安装 Git 时所选的目标位置。

### 用户信息和文本编辑器
设置用户名称和邮件地址，因为每一个Git的提交都会使用这些信息，并且会写入到你的每一次提交中，不可更改：

```
$ git config --gloabl user.name "username"
$ git config --global user.email "user email"
$ git config --global core.editor emacs
//default vim
```
> 如果使用了 --global 选项，那么该命令只需要运行一次，因为之后无论你在该系统上做任何事 情， Git 都会使用那些信息。 
> 当你想针对特定项目使用不同的用户名称与邮件地址时，可以在那个项目目录下运 行没有 --global 选项的命令来配置。

检查配置信息

```
git config --list
//check someone
git config <key>
```

### 获取帮助
Git命令使用手册

```
$ git help <verb>
$ git  <verb> --help
$ man git-<verb>
```
config命令手册

```
git help config
```

## Git基础

### 获取Git仓库

* 在现有目录中初始化仓库
```
$ git init
```
* 克隆现有的仓库
```
git clone [url]
```
### 记录每次更新到仓库
![](https://ws1.sinaimg.cn/large/0079wTXjgy1fsns4c405fj30n509rwfp)

* 检查当前文件状态

    ```
    $ git status
    ```

* 跟踪新文件

    ```
    $ git add [file]
    ```

* 暂存已修改文件

    ```
    $ git add [file]
    ```
    
* 状态简览

    ```
    $ git status -s/--short
    ```

* 忽略文件

    创建一个名为`.gitignore`的文件，列出药忽略的文件模式。
    
    ```
    $ cat .gitignore 
    *.[oa] //忽略所有以.o或.a结尾的文件
    *~     //忽略所有以~结尾的文件
    ```
    
    > .gitignore的格式规范如下：
    • 所有空行或者以 ＃ 开头的行都会被 Git 忽略。
    • 可以使用标准的 glob 模式匹配。
    • 匹配模式可以以（/）开头防止递归。
    • 匹配模式可以以（/）结尾指定目录。
    • 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。
    
    glob 模式是指 shell 所使用的简化了的正则表达式。 星号（\*）匹配零个或多个任意字符；[abc] 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；问号（? ）只匹配一个任意字符；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配 （比如 [0-9] 表示匹配所有 0 到 9 的数字）。 使用两个星号（\*) 表示匹配任意中间目录，比如\`a/**/z\` 可以匹 配 a/z, a/b/z 或 \`a/b/c/z\`等。
    
    > [.gitignore文件列表](https://github.com/github/gitignore)
    
* 查看已暂存和未暂存的修改

    ```
    $ git diff
    ```

## Git分支

### 分支简介

* 创建分支

    ```
    $ git branch bran-name
    ```
    
* 切换分支

    ```
    $ git checkout bran-name
    ```
    
* 查看分叉历史

    ```
    $ git log
    $ git log --oneline --decorete --graph --all
    ```
    
### 分支的新建与合并

工作流：
1. 开发某个网站
2. 为实现某个需求，创建一个分支
3. 在这个分支上展开工作
有Bug需紧急处理：
1. 切换到你的线上分支
2. 为紧急任务创建一个新的分支，并修复它
3. 测试通过后，切换回线上分支，合并这个修补分支，最后将改动推动到线上分支
4. 切换回最初工作的分支，继续工作

* 新建并切换分支

    ```
    $ git branch bran-name
    $ git checkout bran-name
    //简写
    $ git checkout -b bran-name
    ```
    > 切换分支之前，保持干净的状态(提交还未被提交的修改)。也可以保存进度(stashing)和修补提交(commit amending)

* 分支的合并

    ```
    $ git checkout master
    Switched to branch 'master'
    $ git merge bran-name
    ```
    
* 分支的删除

    ```
    $ git branch -d bran-name
    ```
    
* 遇到冲突时的分支合并








