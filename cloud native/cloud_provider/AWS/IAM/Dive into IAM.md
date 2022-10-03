
让你会用并且明白背后的原理

# 解决的问题及产品簇
1. https://docs.aws.amazon.com/zh_cn/organizations/?id=docs_gateway
2. https://docs.aws.amazon.com/zh_cn/singlesignon/?id=docs_gateway
3. https://docs.aws.amazon.com/zh_cn/iam/?id=docs_gateway


## 何为权限控制

本质控制的是对API及关联资源的访问

A公司 -> B 公司 
A 公司多个部门
A公司a部门#1员工


## 何为API的访问：
1. Endpoint https://docs.aws.amazon.com/zh_cn/general/latest/gr/rande.html
2. AWS网关 需要做什么？
3. IAM service需要做什么？
4. AWS后端service 需要什么？

---

## 何为资源

[ARN](https://docs.aws.amazon.com/zh_cn/general/latest/gr/aws-arns-and-namespaces.html) 

---

# 深入理解Role 

example：钦差大臣的故事
1. https://docs.aws.amazon.com/zh_cn/IAM/latest/UserGuide/id_roles_terms-and-concepts.html


---

## 何为服务关联角色

 [doc](https://docs.aws.amazon.com/zh_cn/IAM/latest/UserGuide/using-service-linked-roles.html)

 服务指AWS服务

---


## 何为STS


1. https://docs.aws.amazon.com/zh_cn/STS/latest/APIReference/API_AssumeRole.html

---



# 你的权限剖析

让我们从onelogin开始

---

# service pod 权限剖析

kiam解决的问题: https://github.com/uswitch/kiam

让我们来看deployment.yaml

---

# lambda 权限剖析

从serverless framework 看起
到lambda console 