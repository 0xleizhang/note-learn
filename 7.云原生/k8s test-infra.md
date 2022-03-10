# architecture
[architecture](https://docs.google.com/presentation/d/1HOQ2df_AT-vIuz-JNaJol2oiGq84m50h9T49_5WgEaI/edit#slide=id.g4a3c5dc660_1_359) ppt

[https://raw.githubusercontent.com/kubernetes/test-infra/master/docs/architecture.svg](https://raw.githubusercontent.com/kubernetes/test-infra/master/docs/architecture.svg)



![[assert/architecture.svg]]


将组件分成四类

​

prow核心组件

prow可选组件

prow cli工具组件

绑定Google cloud的组件，prow相关及无关

​

# 工具包

## interrupts
和cockroachdb 的stopper有得一拼 都属于协成管理

​

​

# 模式
Interfacing a Subset of Client

​

> This client has a lot of functions listed in the interfaces of client.go. Further, these interfaces may change at any time. To avoid having to extend the entire interface, we recommend writing a local interface that uses the functionality you need.

# 知识点
operator controller rutime 开发

GitHub API

prometheus & gateway

# prow core

## CRD
code: config/prow/cluster/legacy/prowjob-schemaless_customresourcedefinition.yaml

​

Prowjob定义

三种类型

periodics 周期性执行

postsubmits(Postsubmits are run when a push event happens on a repo) push远程代码仓库

presubmits 根据配置判断是否执行 `always_run` `run_if_changed` .. 根据comments指令/test all 等

​

prowJob定义是如何转化成CRD的？

plugins trigger调用

​

## plank 🌟
​

prowjob CRD自定义资源 controller

[为什么k8s prow plank能使用OSS(阿里云)或QingStor(青云)](https://www.yuque.com/seven4x/kb/gu66p6?view=doc_embed)

### clonerefs

### initupload

### entrypoint

### sidercar

### gcsupload

## hook 🌟
code:prow/cmd/hook

综述；

入口

持有很多系统client，通过plugin处理消息

其中trigger plugin构建prowjob（k8s资源）

​

​

​

配置通过 volumeMounts configMap & secret 到容器目录

通过启动参数制定配置路径（多数有默认值）

flagset解析

​

利用config-bootstrapper 初始化 job-config configMap.

​

### clients

 prowjob CRD client generator by [code-generator](https://github.com/kubernetes/code-generator)

### plugins

#### trigger 创建prowjob

## tide 🌟
直译：趋势，潮流；潮汐

合并PR & PR测试状态报告

 一个定时任务 2m拉去 approve标签的PR 进行合并 调用github merge

也是一个controller通过 [statuses](https://blog.travis-ci.com/2018-09-27-deprecating-github-commit-status-api-for-github-apps-managed-repositories) API 报告PR测试状态

​

合并通过exec调用git命令进行。

​

## crier
英文直译：法庭传唤官

一个controller watch，

通过watch订阅了prowJob状态 报告状态到github slack,gcs,pub/sub(Google消息队列云服务）等

##
​

​

##
​

## ghproxy 🌟
代码路径：/ghproxy

github-api正向代理

ghcache可以根据配置利用redis作为cache实现

##

## sinker 🌟
钓鱼下降铅锤

清除任务，通过controller-runtime管理k8s资源
> controller-runtime是kubebuilder的子项目，kubebuilder是CRD的sdk与之相同的是coreOS的operatorSDK
> controller-runtime是核心抽象，做的本质的事情是对pod及pod属性的CRUD
> controller-runtime底层通过调用client-go实现pod的CRUD



[[controller-runtime]] 使用的是实现Start方法的 controller 而不是 Reconcile ，他们之间的关系，
controller是reconcile的模版代码，controller回调用reconcile
代码参见：`sigs.k8s.io/controller-runtime/pkg/internal/controller/controller.go`


[相关watch原理](https://www.likakuli.com/posts/kubernetes-apiserver-watch/#%E7%AC%AC%E4%BA%8C%E9%83%A8%E5%88%86kube-apiserver%E7%9A%84watch-restful-api)

apiserver 对 etcd的watch
conttroller 对 apiserver的[watch  http chunked 实现](https://mp.weixin.qq.com/s/FOVjzOtwgeSOnuC_HsQF_w)

​

## horologium 时空座
用来创建周期性的prowJob

​

​

​

​

## deck
甲板露台

前端

​

​

## exporter
prometheus-exporter gateway

暴露prowjob metric,这些metric和其他组件不直接相关，无法通过其他组件暴露

# optional components by prow 可选组件

## jenkins-operator
任务运行在jenkins中

## tot
发号器

Tot vends (rations) incrementing numbers for use in builds.

 https://en.wikipedia.org/wiki/Rum_ration

​

## status-reconciler
 ensures changes to blocking presubmits in Prow configuration does not cause in-flight GitHub PRs to get stuck

​

## sub
listen to Cloud Pub/Sub notification to trigger Prow Jobs.

​

​

## gerrit
gerrit 适配

​

​

## branch protector
configures [github branch protection](https://help.github.com/articles/about-protected-branches/) according to a specified policy

​

​

## admission

​

​

---

# cli tools project by prow

## config-bootstrapper
导入Prowjob配置

## tackle
部署prow到K8s集群

​

## phony
模拟github webhook 测试用。

​

## phaino
本地允许prowjob

​

## perbolos
 manages GitHub org, team and membership settings according to a config file. Used by kubernetes/org

​

## mkpod
creates Pods from ProwJobs

​

## mkpj
 creates ProwJobs using Prow configuration.

​

## invitations-accepter
approves all pending GitHub repository invitations

​

​

## hmac
更新密钥



## checkconfig
检查配置

## grandmatriach

## generic-autobumper

## cm2ks
废弃

​

​

---

# infra on GCP
​

## Spyglass 小望远镜
 a pluggable artifact viewer framework for Prow.

通过在deck --spyglass启用

​

## greenhouse
是bazel build的remote cache
> 这个和bazel有个，bazel有增量构建的特性，有输入输出目录，对于大型项目而言这个cache很有必要。

## boskos
资源管理

## triage
 前端可视化

​

​

## testgrid

## gubenator

##

## pipeline

## gcsweb

## gencred

## gopherage
 is a tool for manipulating Go coverage files.

## kettle

## kubetest2

## label_sync

##

##

​

# 部署 prow
bazel build

▼

build push image

▼

[文档](https://github.com/kubernetes/test-infra/blob/master/prow/getting_started_deploy.md) manual deployment

准备github token

配置文件 config/prow/cluster/starter-gcs.yaml 需要<< >> 占位内容进行修改

kubectl apply 部署集群

配置github webhook

▼

配置任务 两种方式

1 静态的 postsubmits,presubmits 配置在configMap config.yml

2 保存在in repo config 源码根目录.prow.yaml，需要开启特性

▼

配置storage 保存日志

▼

开启tide特性 自动合并

# Glossary 词汇表
 gcs = google::cloud::storage = oss

 gce = goole compute engine = ecs

# 学习资料
[Building, Managing and Automating Clusters at Scale With Prow - Michael Splain, Sonos, Inc.](https://www.youtube.com/watch?v=DFJqUMtCuEo)

[KubeCon Seattle 2018 - SIG Testing Intro](https://docs.google.com/presentation/d/1HOQ2df_AT-vIuz-JNaJol2oiGq84m50h9T49_5WgEaI/edit#slide=id.g49782f2733_2_71)

[https://kubernetes.io/zh/blog/2018/08/29/the-machines-can-do-the-work-a-story-of-kubernetes-testing-ci-and-automating-the-contributor-experience/](https://kubernetes.io/zh/blog/2018/08/29/the-machines-can-do-the-work-a-story-of-kubernetes-testing-ci-and-automating-the-contributor-experience/)