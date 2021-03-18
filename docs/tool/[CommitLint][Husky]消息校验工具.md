
# [CommitLint][Husky]消息校验工具

参考：[commitlint](https://conventional-changelog.github.io/commitlint/#/)

使用`commitizen`可以规范化提交信息，同样的，可以设置工具来检查提交信息是否符合格式要求

* [commitlint](https://github.com/conventional-changelog/commitlint)：用于检查提交信息

* [husky](https://github.com/typicode/husky)是`hook`工具，作用于`git-commit`和`git-push`阶段

使用场景：

1. 本地信息检查
2. `CI`信息检查

## `commitlint`

### 全局安装

    $ npm install -g @commitlint/cli @commitlint/config-conventional

### 本地安装

    $ npm install --save-dev @commitlint/{cli,config-conventional}

### 配置规范

    # 使用conventional规范
    $ echo "module.exports = {extends: ['@commitlint/config-conventional']};" > commitlint.config.js

### 测试

需要全局安装才能在命令行使用`commitlint`

    # 错误示例，类型后跟一个冒号和一个空格
    $ echo "docs:添加新的文档" | commitlint

    ⧗   input: docs:添加新的文档
    ✖   subject may not be empty [subject-empty]
    ✖   type may not be empty [type-empty]
    ✖   found 2 problems, 0 warnings 
        (Need help? -> https://github.com/conventional-changelog/commitlint#what-is-commitlint )
    # 正确示例
    $ echo "docs: 添加新的文档" | commitlint

    ⧗   input: docs: 添加新的文档
    ✔   found 0 problems, 0 warnings 
        (Need help? -> https://github.com/conventional-changelog/commitlint#what-is-commitlint )
    # 或者
    $ commitlint "docs: asdf"

    ⧗   input: build(npm): 添加package.json
    ✔   found 0 problems, 0 warnings 
        (Need help? -> https://github.com/conventional-changelog/commitlint#what-is-commitlint )

## `husky`

### 安装

    # 本地
    $ npm install --save-dev husky

### 配置

在`package.json`中添加

    // package.json
    {
        "husky": {
            "hooks": {
                "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
            }  
        }
    }


当`git`提交信息提交`commitlint`检查，参数`-E`默认将`.git/COMMIT_EDITMSG`数据添加到`HUSKY_GIT_PARAMS`

### 测试

    # 错误提交提交
    $ git commit -m "忽略node_modules"
    husky > commit-msg (node v10.15.3)

    ⧗   input: 忽略node_modules
    ✖   subject may not be empty [subject-empty]
    ✖   type may not be empty [type-empty]
    ✖   found 2 problems, 0 warnings 
        (Need help? -> https://github.com/conventional-changelog/commitlint#what-is-commitlint )


    husky > commit-msg hook failed (add --no-verify to bypass)
    # 正确提交
    $ git commit -m "build(npm): 忽略node_modules"
    husky > commit-msg (node v10.15.3)

    ⧗   input: build(npm): 忽略node_modules
    ✔   found 0 problems, 0 warnings 
        (Need help? -> https://github.com/conventional-changelog/commitlint#what-is-commitlint )


    [master 8728336] build(npm): 忽略node_modules
    1 file changed, 1 insertion(+)
    create mode 100644 .gitignore

### 禁用`husky`

某一次提交想要禁用`husky`，可以添加参数`--no-verify`

    $ git commit --no-verify -m "xxx"

## `CI`设置

以`Travis CI`为例

在本地安装

    $ npm install --save-dev @commitlint/travis-cli

修改`travis.yml`

    language: node_js
    script:
        - commitlint-travis