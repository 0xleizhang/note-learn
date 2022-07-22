# with grpc


[rules 官方文档](https://docs.bazel.build/versions/main/be/java.html#rules)


和proto做集成的rules有多个

rules的作用：之前手动操作的步骤自动化，生成proto 结构体，生成client server hub类

1.  rules_java 自带的 [java_proto_library](https://github.com/bazelbuild/rules_java/blob/ca8f85f30491148dc86865e1e799d96410f31500/java/defs.bzl)
2. 官方的 bazelbuild/[rules_proto](https://github.com/bazelbuild/rules_proto)
3. gRPC 官方提供的 [java_grpc_library](https://grpc.io/docs/languages/java/generated-code/)
4. rules_go 提供的 [go_proto_library](https://github.com/bazelbuild/rules_go)
5.  pubref/[rules_protobuf](https://github.com/pubref/rules_protobuf/)  区分与官方提根更多特性 （停更）
6.  ✅ stackb/[rules_proto](https://github.com/stackb/rules_proto) pubref的新版本 基于bazel/gazelle
7.  rules-proto-grpc/[rules_proto_grpc](https://github.com/rules-proto-grpc/rules_proto_grpc)   另一个Bazel rules for building ProtoBuf and gRPC

 
 [对比文章](https://bazel-contrib.github.io/SIG-rules-authors/proto-grpc.html)
 多数社区的rules依赖官方rules_proto的proto_library,proto_library 主要用于构建proto文件依赖关系


gazelle的作用：生成BUILD.bazel 文件 see more:  [[Gazelle]] 


# buildtools

idea 提示缺少buildifier
可以通过 `go install github.com/bazelbuild/buildtools/buildifier@latest`  安装，并将 $GOPATH/bin 添加到PATH环境变量

buildifier is a tool for formatting bazel BUILD and .bzl files with a standard convention.

 
 