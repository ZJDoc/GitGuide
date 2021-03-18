
# [standard-version]版本自动化及CHANGELOG生成

参考：

[conventional-changelog/standard-version](https://github.com/conventional-changelog/standard-version)

[Closing issues using keywords](https://help.github.com/en/articles/closing-issues-using-keywords)

[如何维护更新日志](https://keepachangelog.com/zh-CN/1.0.0/)

## conventioanl-changelog

参考：

[conventional-changelog-cli](https://www.cnblogs.com/zivxiaowei/p/10089201.html)

使用工具[conventional-changelog](https://www.npmjs.com/package/conventional-changelog)进行`CHANGELOG`文件的自动生成

### 安装

全局安装:

```
$ npm install -g conventional-changelog-cli
```

### 使用

基本使用命令如下：

```
$ conventional-changelog -p angular -i CHANGELOG.md -s
```

* 参数`-p`指定提交信息的规范，有以下选择：`angular, atom, codemirror, ember, eslint, express, jquery, jscs or jshint`
* 参数`-i`指定读取`CHANGELOG`内容的文件
* 参数`-s`表示将新生成的`CHANGELOG`输出到`-i`指定的文件中

上述命令将基于上次`tag`版本后的变更内容添加到`CHANGELOG.md`文件中，`CHANGELOG.md`之前的内容不会消失

如果想要重新生成所有版本完整的`CHANGELOG`内容，使用以下命令：

```
$ conventional-changelog -p angular -i CHANGELOG.md -s -r 0
```

* 参数`-r`默认为`1`，设为`0`将重新生成所有版本的变更信息

### 快捷方式

参考：[五、生成 Change log](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)

在工程`package.json`中加入以下脚本

```
    {
      "scripts": {
        "changelog": "conventional-changelog -p angular -i CHANGELOG.md -s -r 0"
      }
    }
```

运行如下命令即可生成`1CHANGELOG`

```
$ npm run changelog
```
