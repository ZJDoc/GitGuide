
# README生成器

[RichardLitt/generator-standard-readme](https://github.com/RichardLitt/generator-standard-readme)提供了一个`npm`命令行工具，用于生成`README`文件

## 安装

```
npm install --global yo generator-standard-readme
```

## 使用

命令行输入

```
$ yo standard-readme
```

接下来会提出很多问题，然后生成一个README文件。所有问题如下：

```
What do you want to name your module?
What is the description of this module?
Do have a banner image?
    Where is the banner image? Ex: 'img/banner.png'
Do you want a TODO dropped where your badges should be?
Do you want a TODO dropped where your long description should be?
Do you need a prioritized security section?
Do you need a background section?
Do you need an API section?
What is the GitHub handle of the main maintainer?
Do you have a CONTRIBUTING.md file?
Are PRs accepted?
Is an MIT license OK?
    What is your license?
Who is the License holder (probably your name)?
Use the current year?
    What years would you like to specify?
```

## 示例

```
$ yo standard-readme
? ==========================================================================
We're constantly looking for ways to make yo better! 
May we anonymously report usage statistics to improve the tool over time? 
More info: https://github.com/yeoman/insight & http://yeoman.io
========================================================================== Yes
? What is the name of your module? zj
? What is the description of this module? yo使用示例
? Do have a banner image? No
? Do you want a standard-readme compliant badge? Yes
? Do you want a TODO dropped where more badges should be? Yes
? Do you want a TODO dropped where your long description should be? Yes
? Do you need a prioritized security section? No
? Do you need a background section? Yes
? Do you need an API section? No
? What is the GitHub handle of the main maintainer? zjZSTU
? Do you have a CONTRIBUTING.md file? No
? Are PRs accepted? Yes
? Is an MIT license OK? Yes
? Who is the License holder (probably your name)? zjZSTU
? Use the current year? Yes
   create README.md
```

生成文件如下：

    # zj                                       // 标题

    [![standard-readme compliant](https://img.shields.io/badge/standard--readme-OK-green.svg?style=flat-square)](https://github.com/RichardLitt/standard-readme)    // 徽章
    TODO: Put more badges here.                // 可以添加更多徽章

    > yo使用示例                                // 简短说明

    TODO: Fill out this long description.      // 详细说明

    ## Table of Contents                       // 下面的章节列表，每个章节都可以点击跳转

    - [Background](#background)
    - [Install](#install)
    - [Usage](#usage)
    - [Maintainers](#maintainers)
    - [Contributing](#contributing)
    - [License](#license)

    ## Background                               // 背景

    ## Install                                  // 安装

    ```
    ```

    ## Usage                                    // 用法

    ```
    ```

    ## Maintainers                              // 主要维护人员

    [@zjZSTU](https://github.com/zjZSTU)

    ## Contributing                             // 参与贡献方式

    PRs accepted.

    Small note: If editing the README, please conform to the [standard-readme](https://github.com/RichardLitt/standard-readme) specification.

    ## License                                  // 许可证

    MIT © 2019 zjZSTU