
# learning-git

*via [「ProGit」](http://git-scm.com/book/zh) *

## git 基础

Git 只关心文件数据的整体是否发生变化，而大多数其他系统则只关心文件内容的具体差异。

Git 更像是把变化的文件作快照后，记录在一个微型的文件系统中。

基本的 Git 工作流程如下：

1.在工作目录中修改某些文件。
2.对修改后的文件进行快照，然后保存到暂存区域。
3.提交更新，将保存在暂存区域的文件快照永久转储到 Git 目录中。

## 初次配置

`git config` 命令

### 配置文件

 - `/etc/gitconfig` 文件：系统中对所有用户都普遍适用的配置。若使用 `git config` 时用 `--system` 选项，读写的就是这个文件。
 - `~/.gitconfig` 文件：用户目录下的配置文件只适用于该用户。若使用 `git config` 时用 `--global` 选项，读写的就是这个文件。
 - 当前项目的 git 目录中的配置文件（也就是工作目录中的 `.git/config` 文件）：这里的配置仅仅针对当前项目有效。每一个级别的配置都会覆盖上层的相同配置，所以 `.git/config` 里的配置会覆盖 `/etc/gitconfig` 中的同名变量。
 
### 用户信息

用户名称和电子邮件地址。这两条配置很重要，每次 Git 提交时都会引用这两条信息，说明是谁提交了更新

    $ git config --global user.name "John Doe"
    $ git config --global user.email johndoe@example.com

### 查看配置信息

`git config -l`


## 获取帮助

`$ git help config`


## 取得 Git 仓库

### 初始化新仓库

    $ git init
    
添加文件：

    $ git add *.c
    $ git add README
    $ git commit -m 'initial project version'

### 克隆仓库

Git 收取的是项目历史的所有数据（每一个文件的每一个版本），服务器上有的数据克隆之后本地也都有了。

克隆仓库的命令格式为 `git clone [url]`

    $ git clone git://github.com/schacon/grit.git
    或
    $ git clone git://github.com/schacon/grit.git mygrit
    
支持协议
 - `git:// ` 协议
 - `http(s):// `
 - `user@server:/path.git`  表示的 SSH 传输协议
 
 
## 记录每次更新到仓库

请记住，工作目录下面的所有文件都不外乎这两种状态：已跟踪或未跟踪。

 - 已跟踪的文件是指本来就被纳入版本控制管理的文件，在上次快照中有它们的记录，工作一段时间后，它们的状态可能是未更新，已修改或者已放入暂存区。
 - 所有其他文件都属于未跟踪文件。它们既没有上次更新时的快照，也不在当前的暂存区域。

### 查看状态

用 `git status` 命令

### 跟踪新文件

用 `git add` 命令

### 暂存已修改文件

还是 `git add` 命令

### 忽略某些文件

可以创建一个名为 `.gitignore` 的文件，列出要忽略的文件模式。来看一个实际的例子：

    $ cat .gitignore
    *.[oa]     # 忽略所有以 .o 或 .a 结尾的文件
    *~          # 忽略所有以波浪符（~）结尾的文件（一些编辑器的副本文件）
    
文件 .gitignore 的格式规范如下：
 - 所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略。
 - 可以使用标准的 glob 模式匹配（指 shell 所使用的简化了的正则表达式）。
 - 匹配模式最后跟反斜杠（/）说明要忽略的是目录。
 - 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。

一个 .gitignore 文件的例子：

    # 此为注释 – 将被 Git 忽略
    # 忽略所有 .a 结尾的文件
    *.a
    # 但 lib.a 除外
    !lib.a
    # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
    /TODO
    # 忽略 build/ 目录下的所有文件
    build/
    # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
    doc/*.txt
    # ignore all .txt files in the doc/ directory
    doc/**/*.txt
    

### 查看已暂存和未暂存的更新

用 `git diff` 命令查看未暂存的更新
用 `git diff --cached` 命令或 `git diff --staged` 查看已经暂存起来的文件和上次提交时的快照之间的差异


### 提交更新

每次准备提交前，先用 `git status` 看下，是不是都已暂存起来了，然后再运行提交命令 `git commit`

    $ git commit

这种方式会启动文本编辑器以便输入本次提交的说明。

也可以用 -m 参数后跟提交说明的方式，在一行命令中提交更新：

    $ git commit -m "Story 182: Fix benchmarks for speed"

