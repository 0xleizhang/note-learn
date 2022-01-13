brew install bazel

brew install bazel@3.4.1

\# 文件
[https://zhuanlan.zhihu.com/p/95998597](https://zhuanlan.zhihu.com/p/95998597)

WORKSPACE(.bazel)

1\. 定义项目根目录和项目名。
1\. 加载 Bazel 工具和 rules 集。
1\. 管理项目外部依赖库。

BUILD.(bazel)

定义依赖解析，构建目标

\*.bzl

自定义函数供WORKSPACE和BUILD文件调用

.bazelrc

配置命令运行时的参数

Gazelle

generator 可以自动生成BUILD.bazel （自动维护依赖）

\# 概念
WORKSPACE

存在WORKSPACE.bazel的根目录

package 存在BUILD.bazel的目录

targets = files rules 指令

labels = target唯一表示（指令名称）

rules

A rule specifies the relationship between inputs and outputs, and the steps to build the outputs

\# rules

\## go-rules

nogo是什么

nogo代码检查=eslint

go\_library

定义源文件及依赖

go\_binary

打包可执行文件

\## rules\_docker
不同语言是不同的target

\*\_image 构建镜像

container\_push 推送
\`\`\`
load("@io\_bazel\_rules\_docker//go:image.bzl", "go\_image")

go\_image(
 name = "go\_image",
 srcs = ["main.go"],
 importpath = "github.com/your/path/here",
)
\`\`\`

\# bazelisk

本地安装的bazel版本可能和.bazelversion要求的版本不一样，运行不了

bazelisk是bazel的封装，自动下载对应的版本，再调用对应的版本

把bazelisk link成bazel 一样的使用体验

\# 构建
go build [target表达式]