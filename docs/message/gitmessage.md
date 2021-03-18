
# [gitmessage]提交模板

## 默认模板

在提交时打开编译器，默认会出现一段模板信息，提示你编辑提交信息，同时会提示当前修改的文件

    $ git commit

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    # On branch master
    # Your branch is ahead of 'origin/master' by 1 commit.
    #   (use "git push" to publish your local commits)
    #
    # Changes to be committed:
    #	modified:   ...
    #   deleted:    ...
    #

## 自定义模板

可以自己编辑一个模板文件，比如新建`~/.gitmessage`，编辑一段关于提交规范的注释

    $ vim ~/.gitmessage

    # head: <type>(<scope>): <subject>
    # - type: feat, fix, docs, style, refactor, test, chore
    # - scope: can be empty (eg. if the change is a global or difficult to assign to a single component)
    # - subject: start with verb (such as 'change'), 50-character line
    #
    # body: 72-character wrapped. This should answer:
    # * Why was this change necessary?
    # * How does it address the problem?
    # * Are there any side effects?
    #
    # footer: 
    # - Include a link to the ticket, if any.
    # - BREAKING CHANGE
    #

修改全局配置文件`~/.gitconfig`，添加

    [commit]
        template = ~/.gitmessage

再次提交时显示的模板如下

    # head: <type>(<scope>): <subject>
    # - type: feat, fix, docs, style, refactor, test, chore
    # - scope: can be empty (eg. if the change is a global or difficult to assign to a single component)
    # - subject: start with verb (such as 'change'), 50-character line
    #
    # body: 72-character wrapped. This should answer:
    # * Why was this change necessary?
    # * How does it address the problem?
    # * Are there any side effects?
    #
    # footer: 
    # - Include a link to the ticket, if any.
    # - BREAKING CHANGE
    #

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    # On branch master
    # Your branch is ahead of 'all/master' by 2 commits.
    #   (use "git push" to publish your local commits)
    #
    # Changes to be committed:
    #       new file:   .gitignore
    #
    # Untracked files:
    #       package.json
    #

## 文件解析

在仓库内的`.git/COMMIT_EDITMSG`文件中保存了最近一次提交的日志（包括模板信息）

## 相关阅读

* [优雅的提交你的 Git Commit Message](https://zhuanlan.zhihu.com/p/34223150)