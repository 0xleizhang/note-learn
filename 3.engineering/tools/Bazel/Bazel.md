brew install bazel

brew install bazel@3.4.1

# 文件
[https://zhuanlan.zhihu.com/p/95998597](https://zhuanlan.zhihu.com/p/95998597)

WORKSPACE(.bazel)

1. 定义项目根目录和项目名。
1. 加载 Bazel 工具和 rules 集。
1. 管理项目外部依赖库。

BUILD.(bazel)

定义依赖解析，构建目标

*.bzl

自定义函数供WORKSPACE和BUILD文件调用

.bazelrc

配置命令运行时的参数

Gazelle

generator 可以自动生成BUILD.bazel （自动维护依赖）

# 概念
## WORKSPACE

存在WORKSPACE.bazel的根目录

package 存在BUILD.bazel的目录

targets = files rules 指令

labels = target唯一表示（指令名称）

rules

A rule specifies the relationship between inputs and outputs, and the steps to build the outputs

# rules

## go-rules

nogo是什么

nogo代码检查=eslint

go_library

定义源文件及依赖

go_binary

打包可执行文件

## rules_docker
不同语言是不同的target

*_image 构建镜像

container_push 推送
```
load("@io_bazel_rules_docker//go:image.bzl", "go_image")

go_image(
 name = "go_image",
 srcs = ["main.go"],
 importpath = "github.com/your/path/here",
)

```



# java 

[java rules ](https://docs.bazel.build/versions/main/be/java.html#java_library)

java_binary 通过_deploy.jar 后缀打包fat-jar [原文](https://docs.bazel.build/versions/main/tutorial/java.html#package-a-java-target-for-deployment)

[rules-jvm-external](https://blog.bazel.build/2019/03/31/rules-jvm-external-maven.html)

更多 [[Bazel-java]]

# bazelisk

本地安装的bazel版本可能和.bazelversion要求的版本不一样，运行不了

bazelisk是bazel的封装，自动下载对应的版本，再调用对应的版本

把bazelisk link成bazel 一样的使用体验

# 构建
go build [target表达式]


# toolchains
抽象的概述：根据platforms自动选择不同的rules 
理解toolchian就能理解经常出现的错误：
`Error:(48, 19) in cc_toolchain_suite rule @local_config_cc//:toolchain: cc_toolchain_suite '@local_config_cc//:toolchain' does not contain a toolchain for cpu 'darwin'`
因为bazel要编译到不同的target， 先不考虑有runner
没有toolchains之前不同的平台
要么是不同的rules
比如
bar_binary_win
bar_binary_linux 
要么通过参数传递进去，参加官方的例子
![[Pasted image 20220325195925.png]]

有了toolchians之后能够根据不同的platforms选择不同的toolchians（也就是编译套件）
见这个例子截图：cc_toolchain_suite 根据不同的arch对应不同的实际toolchian

![[Pasted image 20220325200110.png]]

这个报错就是系统识别我们的arch 在tool_suit里没找到对应的具体tool_chain

这样就有两种解决方式，一个是通过 platforms alias 比如 aarch64和arm64就是一个东西只是在不同社区Linux和GUN不同叫法，[参加](https://stackoverflow.com/questions/31851611/differences-between-arm64-and-aarch64)。
另一个结局办法就是让bazel正确识别或者符合期望的识别，比如他这里期望darwin_arm64但是识别成了darwin，这是一个思路，但是具体怎么搞还有待探索。
