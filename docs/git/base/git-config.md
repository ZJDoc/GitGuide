
# [git config]配置

## 命令行操作范围

使用命令`git config`进行配置，各级别设置需要加上可选参数

    # 系统级别
    git config --system ...
    # 全局级别
    git config --global ...
    # 仓库级别
    git config --local ...

### 打印配置信息

* 获取配置信息

```
$ git config --list
user.name=xxx
user.email=xxx@163.com
core.editor=code
http.postbuffer=1048576000
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
remote.origin.url=git@github.com:ZJDoc/GitGuide.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.master.remote=origin
branch.master.merge=refs/heads/master
```

* 获取全局配置信息

```
$ git config --global --list
user.name=xxx
user.email=xxx@163.com
core.editor=code
http.postbuffer=1048576000
```

* 获取本地配置信息

```
$ git config --local --list
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
remote.origin.url=git@github.com:ZJDoc/GitGuide.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.master.remote=origin
branch.master.merge=refs/heads/master
```

**注意：需要进入一个`Git`仓库才能获取本地信息**

## 常用设置

1. 设置用户信息
2. 设置文本编辑器
3. 移除变量

### 设置用户信息

每次提交时都需加上用户名和邮箱地址，可以设置成全局变量

    git config --global user.name user-name
    git config --global user.email email-address

*设置节点为`user`，设置属性为`name`和`email`*

也可以在仓库中设置本地用户名和用户邮箱：

```
$ git config --local user.name xxx
$ git config --local user.email xxx
```

### 设置文本编辑器

`git`使用系统默认的编辑器，可以设置指定编辑器

    # 未设置
    git config --global core.editor vim
    # 已设置，先删除再添加
    git config --global --unset core.editor
    git config --global core.editor vim

### 移除变量

    # 移除单个变量
    git config --global --unset 属性名
    # 移除所有变量
    git config --global --unset-all 属性名

## 配置文件地址

`git`有`3`个级别的配置文件：

1. `local`：本地文件存放在仓库中(`.git/config`)，只针对当前仓库
2. `global`：全局文件存放为`~/.gitconfig`或`~/.config/git/config`，作用于当前用户的所有仓库
3. `system`：系统文件存放为`/etc/gitconfig`，作用于系统的每个用户

其优先级为`local > global > system`

*`windows`环境下的全局配置文件存放为`C:\\User\\$USER\\.gitconfig`*

### 编写格式

所有配置文件的编写格式都一样，可参考仓库级别的`config`文件，按照*section和key*进行配置

    # 仓库级别
    $ cat config 
    [core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
    [remote "origin"]
        url = git@github.com:zjZSTU/linux-guide.git
        fetch = +refs/heads/*:refs/remotes/origin/*
    [branch "master"]
        remote = origin
        merge = refs/heads/master
    # 全局级别
    $ cat .gitconfig 
    [user]
        name = zxxx
        email = 50xxxxx.com