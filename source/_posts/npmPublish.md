---
title: 如何创建并发布自己的npm包
author: leonliu
category: npm
tags:
- npm
---

# 常用npm命令
## npm version
<!--more-->
### 语法
```
npm version [<newversion> | major | minor | patch | premajor | preminor | prepatch | prerelease [--preid=<prerelease-id>] | from-git]

'npm [-v | --version]' to print npm version
'npm view <pkg> version' to view a package's published version
'npm ls' to inspect current package/dependency versions
DESCRIPTION§
```

在命令行窗口输入npm version ?可以查看可以使用的命令:
```
major: 主版本号
premajor: 预备主版本
minor: 次版本号
preminor: 预备次版本
patch: 修订号
prepatch: 预备修订版
prerelease: 预发布版本
```

执行命令及版本提升示例：
```
假设初始版本为0.0.0
➜  xxx git:(master) npm version preminor
v0.1.0-0
➜  xxx git:(master) npm version minor
v0.1.0
➜  xxx git:(master) npm version prepatch
v0.1.1-0
➜  xxx git:(master) npm version patch   
v0.1.1
➜  xxx git:(master) npm version prerelease
v0.1.2-0
➜  xxx git:(master) npm version premajor
v1.0.0-0
➜  xxx git:(master) npm version major   
v1.0.0
```

## npm publish
```
npm publish [<tarball>|<folder>][--tag <tag>] [--access <public|restricted>][--otp otpcode] [--dry-run]
Publishes '.' if no argument supplied
Sets tag 'latest' if no --tag specified
```
- &lt;folder&gt;：包含 package.json 文件的文件夹
- &lt;tarball&gt;：压缩后的 tar 存档的 url 或文件路径，其中包含单个文件夹，其中包含 package.json 文件。
- [--tag &lt;tag&gt;] 使用给定标签注册发布的软件包，例如npm install @将安装此版本。默认情况下，npm publish更新和npm install安装latest标签。有关标签的详细信息，请参见npm-dist-tag。
- [--access &lt;public|restricted&gt;] 告诉注册表此软件包是应公开发行还是受限制发行。仅适用于作用域包，默认为 restricted。如果您没有付费帐户，则必须使用发布与 –access public 发布有范围的软件包。
- [--otp &lt;otpcode&gt;] 如果您在 auth-and-writes 模式下启用了双重身份验证，那么您可以为此提供来自身份验证器的代码。如果您不包括此文件，而您正在从 TTY 中运行，则会提示您。
- [--dry-run] 从开始 npm@6，除了实际发布到注册表外，所有发布都可以完成。报告将要发布的内容的详细信息。
- 如果指定的注册表中已经存在软件包名称和版本组合，则失败。

**一旦使用给定的名称和版本发布了软件包，即使使用 npm-unpublish 将其删除，该特定名称和版本组合也将永远无法再次使用。**

## npm adduser
```
npm adduser [--registry=url] [--scope=@orgname] [--always-auth] [--auth-type=legacy]
aliases: login, add-user
```
npm login是它的别名

## 发包过程
### 第一次发包
终端输入npm adduser,提示输入账号，密码和邮箱，然后将提示创建成功
### 非第一次发包
在终端输入npm login，然后输入你创建的账号和密码，和邮箱，登陆
### 发布
npm publish
### 撤销发布
npm unpublish
删除npm市场的包同名的24小时后才能重新发布

# 创建一个简单的模版管理工具(leon-cli)
```
Usage: leon cli [options]

Options:
  -v --version  output the version number
  -h, --help    output usage information

Commands:
  init|i        Create a new project by templates
  list|ls       Show template lists
  use|u         Switch template to use
  get|g         Get one custom template, if only use "leon get" show all templates
  set|s         Add or modify one custom template
  remove|rm     Delete one custom template

Usages:
  leon init <project-name>                   : Init a project by template
  leon list                                  : List all the templates
  leon get <key>?                            : Get one custom template
  leon set <key> <value>                     : Add or modify one custom template
  leon remove <key>                          : Delete one custom template
  leon use <template-name>                   : Switch template to use
```
[leon-cli详细代码](https://github.com/lord2416/leon-cli)