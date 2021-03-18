
# [Commitizen]信息交互工具

[Commitizen](http://commitizen.github.io/cz-cli/)是一个提交日志工具，辅助开发者使用提交规则

## 预配置

需要安装`NodeJS`，参考：[nodeJS安装](https://hexo-guide.readthedocs.io/zh_CN/latest/node/nodeJS%E5%AE%89%E8%A3%85.html)

## 安装`Commitizen`

    # 全局安装
    $ npm install -g commitizen

## 安装`Adapter`

`Commitizen`支持多种不同的提交规范，可以安装和配置不同的适配器实现

以`Conventional Commit`规范为例

### 全局配置（推荐）

    # 安装
    $ npm install -g cz-conventional-changelog
    # 配置
    $ echo '{ "path": "cz-conventional-changelog" }' > ~/.czrc

### 本地配置

    # 安装
    commitizen init cz-conventional-changelog --save-dev --save-exact

安装完成后，查看是否在`package.json`中已加入`cz-conventional-changelog`信息：

```
...
...
  "devDependencies": {
    "cz-conventional-changelog": "^3.0.2"
  },
  "config": {
    "commitizen": {
      "path": "./node_modules/cz-conventional-changelog"
    }
  }
}
```

### 测试

安装完成后，使用`git-cz`替代`git commit`完成提交操作，

```
$ git cz
cz-cli@4.0.3, cz-conventional-changelog@3.0.2

? Select the type of change that you're committing: (Use arrow keys)
❯ feat:     A new feature 
  fix:      A bug fix 
  docs:     Documentation only changes 
  style:    Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc) 
  refactor: A code change that neither fixes a bug nor adds a feature 
  perf:     A code change that improves performance 
  test:     Adding missing tests or correcting existing tests 
(Move up and down to reveal more choices)
```

通过提示信息辅助你完成标准化的提交日志

**`git-cz`支持`git commit`所有的参数设置**

**正文换行使用`\n`操作，比如正文内容如下：`新增事项:\n1. 测试1\n2. 测试2\n3. 测试`**

    build(npm): 加入package.json
    
    新增事项:
    1. 测试1
    2. 测试2
    3. 测试

## 徽章

在`README`中添加`commitizen`友好徽章

[![](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)