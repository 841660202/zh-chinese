# 面向合约的 Solidity 编程语言

[![Matrix Chat](https://img.shields.io/badge/Matrix%20-chat-brightgreen?style=plastic&logo=matrix)](https://matrix.to/#/#ethereum_solidity:gitter.im)
[![Gitter Chat](https://img.shields.io/badge/Gitter%20-chat-brightgreen?style=plastic&logo=gitter)](https://gitter.im/ethereum/solidity)
[![Solidity Forum](https://img.shields.io/badge/Solidity_Forum%20-discuss-brightgreen?style=plastic&logo=discourse)](https://forum.soliditylang.org/)
[![Twitter Follow](https://img.shields.io/twitter/follow/solidity_lang?style=plastic&logo=twitter)](https://twitter.com/solidity_lang)
[![Mastodon Follow](https://img.shields.io/mastodon/follow/000335908?domain=https%3A%2F%2Ffosstodon.org%2F&logo=mastodon&style=plastic)](https://fosstodon.org/@solidity)

您可以在 Gitter 和 Matrix 上与我们交谈，在 Twitter 上向我们发推特，或者在 Solidity 论坛上创建一个新的主题。
我们欢迎一切问题，反馈和建议。

Solidity 是一种静态类型的，面向合约的高级语言，用于在 Ethereum 平台上实现智能合约。

为了获得一个好的概述和起点，请查看官方的 [Solidity 语言门户](https://soliditylang.org)。

## 目录

- [面向合约的 Solidity 编程语言](#面向合约的-solidity-编程语言)
  - [目录](#目录)
  - [背景介绍](#背景介绍)
  - [构建和安装](#构建和安装)
  - [示例](#示例)
  - [文档](#文档)
  - [发展](#发展)
  - [维护者](#维护者)
  - [许可](#许可)
  - [安全](#安全)
  - [run](#run)
  - [](#)
  - [sphinx-autobuild -h](#sphinx-autobuild--h)
  - [rst 语法](#rst-语法)
  - [扩展 rst 语法](#扩展-rst-语法)

## 背景介绍

Solidity 是一种静态类型的大括号编程语言，用于开发在以太坊虚拟机上运行的智能合约。
智能合约是在点对点网络内执行的程序，没有人对执行有特别的权限，
因此它们允许实现价值代币，所有权，投票和其他种类的逻辑。

当部署合约时，您应该使用最新发布的 Solidity 版本。
这是因为重大的变化，以及新的功能和错误修复都是定期引入的。
我们目前使用 0.x 版本号 [以表示这种快速变化的节奏](https://semver.org/#spec-item-4)。

## 构建和安装

关于如何构建和安装 Solidity 编译器的说明可以在
[Solidity 文档](https://docs.soliditylang.org/en/latest/installing-solidity.html#building-from-source)
中找到。

## 示例

在 Solidity 中的 “Hello World” 程序比其他语言更没有用处，但此处仍然以此来展示：

```solidity
// SPDX-License-Identifier: MIT
pragma solidity >=0.6.0 <0.9.0;

contract HelloWorld {
    function helloWorld() external pure returns (string memory) {
        return "Hello, World!";
    }
}
```

要开始使用 Solidity，您可以使用 [Remix](https://remix.ethereum.org/)，
它是一个基于浏览器的 IDE。这里有一些合约的例子：

1. [投票合约](https://docs.soliditylang.org/en/latest/solidity-by-example.html#voting)
2. [盲拍合约](https://docs.soliditylang.org/en/latest/solidity-by-example.html#blind-auction)
3. [安全的远程购买合约](https://docs.soliditylang.org/en/latest/solidity-by-example.html#safe-remote-purchase)
4. [微支付通道合约](https://docs.soliditylang.org/en/latest/solidity-by-example.html#micropayment-channel)

## 文档

Solidity 文档托管在 [阅读文档](https://docs.soliditylang.org) 。

## 发展

Solidity 仍在开发中。我们随时欢迎您的贡献!
如果您想提供帮助，请遵循 [开发者指南](https://docs.soliditylang.org/en/latest/contributing.html)。

您可以在 [项目管理](https://github.com/ethereum/solidity/projects)
中找到我们目前对即将发布的版本的功能和错误的优先级。

## 维护者

- [@axic](https://github.com/axic)
- [@chriseth](https://github.com/chriseth)

## 许可

Solidity 有 [GNU 通用公共许可证 v3.0](LICENSE.txt) 的许可。

一些第三方代码有其 [自己的许可条款](cmake/templates/license.h.in)。

## 安全

安全政策可以 [在这里找到](SECURITY.md)。

## run

```sh
cd docs && ./docs.sh
```

https://www.sphinx-doc.org/en/master/man/sphinx-build.html

##

如果你希望 Sphinx 在源文件发生变化时自动重新生成 HTML 文档，你可以使用 sphinx-autobuild 工具。这是一个独立的工具，它会监听你的源文件的变化，并在文件发生变化时自动运行 sphinx-build。

首先，你需要安装 sphinx-autobuild。你可以使用 pip 来安装：

`pip install sphinx-autobuild`

然后，你可以运行 sphinx-autobuild，并指定你的源文件目录和输出目录：

`sphinx-autobuild sourcedir builddir`

这个命令将启动一个 web 服务器，并在源文件发生变化时自动重新生成 HTML 文档。你可以在你的 web 浏览器中访问 http://localhost:8000 来查看你的文档。

注意：sphinx-autobuild 默认监听 8000 端口，如果这个端口已经被其他服务使用，你可以使用-p 选项来指定一个不同的端口，例如：`sphinx-autobuild -p 8080 sourcedir builddir`。

## sphinx-autobuild -h

```
➜  ~/Desktop/docs/zh-chinese sphinx-autobuild -h
usage: sphinx-autobuild [-h] [--port PORT] [--host HOST] [--re-ignore RE_IGNORE] [--ignore IGNORE] [--no-initial] [--open-browser] [--delay DELAY]
                        [--watch DIR] [--pre-build COMMAND] [--version]
                        sourcedir outdir [filenames ...]

positional arguments:
  sourcedir             source directory
  outdir                output directory for built documentation
  filenames             specific files to rebuild on each run (default: None)

options:
  -h, --help            show this help message and exit
  --port PORT           port to serve documentation on. 0 means find and use a free port (default: 8000)
  --host HOST           hostname to serve documentation on (default: 127.0.0.1)
  --re-ignore RE_IGNORE
                        regular expression for files to ignore, when watching for changes (default: [])
  --ignore IGNORE       glob expression for files to ignore, when watching for changes (default: [])
  --no-initial          skip the initial build (default: False)
  --open-browser        open the browser after building documentation (default: False)
  --delay DELAY         how long to wait before opening the browser (default: 5)
  --watch DIR           additional directories to watch (default: [])
  --pre-build COMMAND   additional command(s) to run prior to building the documentation (default: [])
  --version             show program's version number and exit

sphinx's arguments:
  The following arguments are forwarded as-is to Sphinx. Please look at `sphinx --help` for more information.
    -b=builder, -a, -E, -d=path, -j=N, -c=path, -C, -D=setting=value, -t=tag, -A=name=value, -n, -v, -q, -Q, -w=file, -W, -T, -N, -P

```

## rst 语法

https://sublime-and-sphinx-guide.readthedocs.io/en/latest/lists.html

## 扩展 rst 语法

在 RestructuredText (reST) 中，没有直接的方式来为文本添加颜色。reST 语法主要关注内容和结构，而不是样式。样式通常在生成文档的过程中由 CSS 或其他样式语言处理。

然而，你可以通过定义自定义的角色或指令来实现这个功能。例如，你可以在 Sphinx 的 `conf.py` 文件中定义一个新的角色：

```py
from docutils import nodes
from docutils.parsers.rst import roles

# 上述两个插件写入到文件中后，需要执行 /zh-chinese/docs 文件夹下的 ./docs.sh, 来安装依赖


def color_role(role, rawtext, text, lineno, inliner, options={}, content=[]):
  return [nodes.inline(rawtext, text, classes=[role])], []

roles.register_local_role('red', color_role)
roles.register_local_role('green', color_role)
# 这里写完了需要重新执行 ./dev.sh
```

然后在 CSS 文件中定义这些角色的样式：

```css
.red {
  color: red;
}
.green {
  color: green;
}
```

最后，在 reST 文档中使用这些角色：

```rst
This is :red:`red` and this is :green:`green`.
```

请注意，这种方法需要你有一些 Python 和 CSS 的知识，并且可能不适用于所有的 reST 渲染器。
