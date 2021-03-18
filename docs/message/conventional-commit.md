
# Conventional提交规范

[Conventional Commits](https://www.conventionalcommits.org)(约定式提交)脱胎于`Angular`提交信息准则，提供了更加通用、简洁和灵活的提交规范

提交格式如下：

    <类型>[可选的作用域]: <描述>
    # 空一行
    [可选的正文]
    # 空一行
    [可选的脚注]

## 页眉设置

强制支持的类型名是`fix`和`feat`，同样支持`Angular`准则中推荐的其他类型

常规提交规范还推荐使用类型`improvement`，表示在不添加新功能或修复`bug`的情况下改进当前的实现

## 页尾设置

强制支持在页脚使用`BREAKING CHANGES`

## 提交规范

结合[RFC2019](https://www.ietf.org/rfc/rfc2119.txt)，在下面规范中使用关键字来指示需求级别

* `MUST`（必须）
* `MUST NOT`（禁止）
* `REQUIRED`（需要）
* `SHALL`（应当）
* `SHALL NOT`（不应当）
* `SHOULD`（应该）
* `SHOULD NOT`（不应该）
* `RECOMMENDED`（推荐）
* `MAY`（可以）
* `OPTIONAL`（可选）

1. 每次提交**必须**添加类型名为前缀。类型名是一个名词，比如`feat、fix`，后跟冒号和一个空格
2. 类型`feat`**必须**在提交新特征时使用
3. 类型`fix`**必须**用于修复`bug`的提交
4. 类型后面**可以**添加一个可选的作用域。作用域名是一个短语，表示代码库中的一个小节，比如`fix(parser)`
5. 在类型/作用域前缀后面**必须**跟上一个简短描述，关于本次提交的代码修改，比如`fix: 字符串中包含多个空格时的数组分析问题`
6. **可以**在描述后面添加一个长的正文，用于提供额外的上下文信息。正文内容**必须**在短描述后空一行开始
7. **可以**在正文后空一行开始页脚，页脚**应该**包含这次代码修改的相关问题，比如`Fixes #13`
8. 不兼容修改(`breaking change`)**必须**放置在提交的页脚或正文部分的最开始处，**必须**使用大写文本`BREAKING CHANGE`作为前缀，后跟冒号和一个空格
9. 在`BREAKING CHANGE:`后面**必须**提供一个描述，关于`API`的修改，比如`BREAKING CHANGE: 环境变量目前优先于配置文件`
10. 页脚**必须**包含不兼容修改、额外链接、问题引用和其他元信息
11. 除了`feat`和`fix`以外的类型**可以**在提交信息中使用

## 徽章

使用了常规提交规范可以添加徽章在`README`

    [![Conventional Commits](https://img.shields.io/badge/Conventional%20Commits-1.0.0-yellow.svg)](https://conventionalcommits.org)

## 实现示例

只有页眉和页尾

    feat: allow provided config object to extend other configs

    BREAKING CHANGE: `extends` key in config file is now used for extending other config files

只有页眉

    docs: correct spelling of CHANGELOG

使用了作用域

    feat(lang): added polish language

修复了`bug`

    fix: minor typos in code

    see the issue for details on the typos fixed

    fixes issue #12

## `FAQ`

问：在最初开发阶段如何处理提交信息？

建议像已发布产品一样处理。即使是你的软件开发伙伴在使用软件过程中，也想知道那些被修复了，那些是不兼容修改。

问：提交头的类型名是大写还是小写？

无所谓，不过最好保持一致（一直大写或一直小写）

**问：如果提交内容适用于多个类型怎么办？**

尽可能返回并进行多次提交。常规提交准则的优势在于它有能力驱动我们进行更加组织化的提交和`PR`

问：这是否是不鼓励快速开发和快速迭代？

它不鼓励以无序的方式快速开发。它帮助你在有多个开发者的多个项目中进行长期开发

**问：常规提交准则是否会限制提交的类型?**

常规提交准则鼓励开发者使用更多有确切含义的类型。除此以外，准则的灵活性允许开发组提出更多适用于自己的类型，并随着时间的推移更改这些类型

问：这个准则和[SemVer](https://semver.org/lang/zh-CN/)的联系？

`fix`类型应该翻译成`PATCH`版本。`feat`类型应该翻译成`MINOR`版本。如果提交信息中包含`不兼容修改`，不管哪种类型，都应该翻译成`MAJOR`版本

问：如何将扩展版本转换为常规提交规范?

我们建议使用`SemVer`发布您自己对本规范的扩展（并鼓励您进行这些扩展！）

**问：如果我不小心使用了错误的提交类型，该怎么办？**

1. 使用了规范中的类型但是没有使用正确的类型，比如使用`fix`替代了`feat`

在合并或者发布这个错误之前，推荐使用`git rebase -i`进行提交历史编辑。发布之后，依据使用的工具或流程进行清理

2. 当使用了规范外的类型，比如使用了`feet`替代了`feat`

如果提交不符合常规提交规范，它只是意味着基于规范的工具将错过这次提交

**问：是否我的所有贡献者都需要使用常规提交规范?**

如果使用基于`squash`的`Git`工作流，主管维护者可以在合并时清理提交信息——这不会对普通提交者产生额外的负担。常见的工作流程是让`git`系统自动从`pull request`中`squash`出提交，并向主维护者提供一份表单，用以在合并时输入适合的`git`提交信息。