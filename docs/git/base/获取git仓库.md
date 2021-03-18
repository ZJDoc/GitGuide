
# 获取git仓库

## 本地新建

在工程目录中输入如下命令

    git init

生成一个`.git`文件夹

## 远程拉取

从远程服务器`(github/gitee`等)获取地址后拉取到本地

    git clone <repo> [<dir>]

`<repo>`表示输入地址

    git clone https://github.com/zjZSTU/git-guide.git

也可制定路径

    git clone https://github.com/zjZSTU/git-guide.git ../git-repo/

或文件夹

    git clone https://github.com/zjZSTU/git-guide.git guide

下载并绑定指定分支
    
    git clone --branch [标签名/分支名] [git地址]