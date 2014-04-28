
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





