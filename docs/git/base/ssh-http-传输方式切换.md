
# [ssh][http]传输方式切换

通过修改本地文件，切换代码传输方式

## 命令修改

查看当前使用`SSH`还是`HTTP`

    $ git remote -v
    origin	git@gitee.com:zjZSTU/zjzstu.gitee.io.git (fetch)
    origin	git@gitee.com:zjZSTU/zjzstu.gitee.io.git (push)

当前使用`SSH`协议进行代码拉取和推送

方式一：仅修改拉取协议为`HTTP`

    $ git remote set-url --push origin https://gitee.com/zjZSTU/zjzstu.gitee.io.git
    $ git remote -v
    origin	git@gitee.com:zjZSTU/zjzstu.gitee.io.git (fetch)
    origin	https://gitee.com/zjZSTU/zjzstu.gitee.io.git (push)

方式二：同时修改拉取和推送协议为`HTTP`

    # 先增加HTTP
    $ git remote set-url --add origin https://gitee.com/zjZSTU/zjzstu.gitee.io.git
    $ git remote -v
    origin	git@gitee.com:zjZSTU/zjzstu.gitee.io.git (fetch)
    origin	https://gitee.com/zjZSTU/zjzstu.gitee.io.git (push)
    # 再删除SSH
    $ git remote set-url --delete origin git@gitee.com:zjZSTU/zjzstu.gitee.io.git
    $ git remote -v
    origin	https://gitee.com/zjZSTU/zjzstu.gitee.io.git (fetch)
    origin	https://gitee.com/zjZSTU/zjzstu.gitee.io.git (push)

## 文件修改

修改文件`.git/config`的`remote`小节

    [core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
    [remote "origin"]
        fetch = +refs/heads/*:refs/remotes/origin/*
        url = git@gitee.com:zjZSTU/zjzstu.gitee.io.git
    [branch "master"]
        remote = origin
        merge = refs/heads/master
    [branch "dev"]
        remote = origin
        merge = refs/heads/dev

方式一：仅修改拉取协议为`HTTP`

添加`pushurl = ...`到`remote`小节

    ...
    [remote "origin"]
        fetch = +refs/heads/*:refs/remotes/origin/*
        url = git@gitee.com:zjZSTU/zjzstu.gitee.io.git
        pushurl = https://gitee.com/zjZSTU/zjzstu.gitee.io.git
    [branch "master"]
    ...

方式二：同时修改拉取和推送协议为`HTTP`

修改`url`为`HTTP`即可

    ...
    [remote "origin"]
        fetch = +refs/heads/*:refs/remotes/origin/*
        url = https://gitee.com/zjZSTU/zjzstu.gitee.io.git
    ...