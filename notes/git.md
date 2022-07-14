---
attachments: [Clipboard_2022-07-13-09-17-46.png, Clipboard_2022-07-13-09-24-09.png]
title: git
created: '2022-07-13T01:17:40.568Z'
modified: '2022-07-13T02:21:24.565Z'
---

# git

![](@attachment/Clipboard_2022-07-13-09-17-46.png)

- 图中左侧为工作区，右侧为版本库。在版本库中标记为 "index" 的区域是暂存区（stage/index），标记为 "master" 的是 master 分支所代表的目录树。

- 图中我们可以看出此时 "HEAD" 实际是指向 master 分支的一个"游标"。所以图示的命令中出现 HEAD 的地方可以用 master 来替换。

- 图中的 objects 标识的区域为 Git 的对象库，实际位于 ".git/objects" 目录下，里面包含了创建的各种对象及内容。

- 当对工作区修改（或新增）的文件执行 git add 命令时，暂存区的目录树被更新，同时工作区修改（或新增）的文件内容被写入到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。

- 当执行提交操作（git commit）时，暂存区的目录树写到版本库（对象库）中，master 分支会做相应的更新。即 master 指向的目录树就是提交时暂存区的目录树。

- 当执行 git reset HEAD 命令时，暂存区的目录树会被重写，被 master 分支指向的目录树所替换，但是工作区不受影响。

- 当执行 git rm --cached <file> 命令时，会直接从暂存区删除文件，工作区则不做出改变。

- 当执行 git checkout . 或者 git checkout -- <file> 命令时，会用暂存区全部或指定的文件替换工作区的文件。这个操作很危险，会清除工作区中未添加到暂存区中的改动。

- 当执行 git checkout HEAD . 或者 git checkout HEAD <file> 命令时，会用 HEAD 指向的 master 分支中的全部或者部分文件替换暂存区和以及工作区中的文件。这个命令也是极具危险性的，因为不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动。

## 命令


![](@attachment/Clipboard_2022-07-13-09-24-09.png)
`git init`	初始化仓库
`git clone`	拷贝一份远程仓库，也就是下载一个项目。

[`git add`](#git-add)	添加文件到暂存区
[`git status`](#git-status)	查看仓库当前的状态，显示有变更的文件。
[`git diff`](#git-diff)	比较文件的不同，即暂存区和工作区的差异。
[`git commit`](#git-commit)	提交暂存区到本地仓库。
[`git reset`](#git-reset)	回退版本。
[`git rm`](#git-rm)	将文件从暂存区和工作区中删除。
[`git mv`](#git-mv)	移动或重命名工作区文件。
[`git remote`](#git-remove)	远程仓库操作
[`git fetch`](#git-fetch)	从远程获取代码库
[`git pull`](#git-pull)	下载远程代码并合并
[`git push`](#git-push)	上传远程代码并合并

### git add
添加一个或多个文件到暂存区：

`git add [file1] [file2]`
`git add [dir]`

### git status

git status 命令用于查看在你上次提交之后是否有对文件进行再次修改。

### git diff

git diff 命令比较文件的不同，即比较文件在暂存区和工作区的差异。

git diff 命令显示已写入暂存区和已经被修改但尚未写入暂存区文件的区别。

git diff 有两个主要的应用场景。

尚未缓存的改动：git diff
查看已缓存的改动： git diff --cached
查看已缓存的与未缓存的所有改动：git diff HEAD
显示摘要而非整个 diff：git diff --stat

显示暂存区和工作区的差异:
`git diff [file]`

显示暂存区和上一次提交(commit)的差异:
`git diff --cached [file]`
`git diff --staged [file]`

显示两次提交之间的差异:

`git diff [first-branch]...[second-branch]`

### git commit 

提交暂存区到本地仓库中:

`git commit -m [message]`

### git reset
`git reset [--soft | --mixed | --hard] [HEAD]`

--mixed 为默认，可以不用带该参数，用于重置暂存区的文件与上一次的提交(commit)保持一致，工作区文件内容保持不变。

```shell
git reset HEAD^            # 回退所有内容到上一个版本  
git reset HEAD^ hello.php  # 回退 hello.php 文件的版本到上一个版本  
git reset  052e           # 回退到指定版本
```

--soft 参数用于回退到某个版本：

```shell
git reset --soft HEAD~n # 回退到n个版本前
```

--hard 参数撤销工作区中所有未提交的修改内容，将暂存区与工作区都回到上一次版本，并删除之前的所有信息提交：
```shell
git reset --hard HEAD
```

HEAD 说明：

- HEAD 表示当前版本

- HEAD^ 上一个版本

- HEAD^^ 上上一个版本

- HEAD^^^ 上上上一个版本

可以使用 ～数字表示
- HEAD~0 表示当前版本

- HEAD~1 上一个版本

- HEAD~2 上上一个版本

- HEAD~3 上上上一个版本

简而言之，执行 git reset HEAD 以取消之前 git add 添加，但不希望包含在下一提交快照中的缓存。

### git rm
将文件从暂存区和工作区中删除：
```shell
git rm <file>
```
如果想把文件从暂存区域移除，但仍然希望保留在当前工作目录中，换句话说，仅是从跟踪清单中删除，使用 --cached 选项即可：

```sh
git rm --cached <file>
```

### git mv
`git mv` 命令用于移动或重命名一个文件、目录或软连接。

```sh
git mv [file] [newfile]
```

### git remote

显示所有远程仓库：

```sh
git remote -v
```
显示某个远程仓库的信息：

```sh
git remote show [remote]
```
添加远程版本库：

```shell
git remote add [shortname] [url]
git remote rm name  # 删除远程仓库
git remote rename old_name new_name  # 修改仓库名
```

### git fetch

git fetch 命令用于从远程获取代码库。该命令执行完后需要执行 git merge 远程分支到你所在的分支。从远端仓库提取数据并尝试合并到当前分支：

```shell
git fetch
git merge
```

### git pull
git pull 命令用于从远程获取代码并合并本地的版本。

git pull 其实就是 git fetch 和 git merge FETCH_HEAD 的简写。

```sh
git pull <远程主机名> <远程分支名>:<本地分支名>
```

### git push
```sh
git push 命令用于从将本地的分支版本上传到远程并合并。
```
命令格式如下：
```shell
git push <远程主机名> <本地分支名>:<远程分支名>
# 如果本地分支名与远程分支名相同，则可以省略冒号：
git push <远程主机名> <本地分支名>
```
