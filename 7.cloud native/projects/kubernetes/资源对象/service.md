演进过程

service->ingress -> [gatewayAPI](https://kubernetes.io/blog/2021/04/22/evolving-kubernetes-networking-with-the-gateway-api/)

\> \`Type\` 的取值以及行为如下：
\> \- \`ClusterIP\`：通过集群的内部 IP 暴露服务，选择该值时服务只能够在集群内部访问。 这也是默认的 \`ServiceType\`。

\> \- [\`NodePort\`](https://kubernetes.io/zh/docs/concepts/services-networking/service/#nodeport)：通过每个节点上的 IP 和静态端口（\`NodePort\`）暴露服务。 \`NodePort\` 服务会路由到自动创建的 \`ClusterIP\` 服务。 通过请求 \`<节点 IP>:<节点端口>\`，你可以从集群的外部访问一个 \`NodePort\` 服务。

\> \- [\`LoadBalancer\`](https://kubernetes.io/zh/docs/concepts/services-networking/service/#loadbalancer)：使用云提供商的负载均衡器向外部暴露服务。 外部负载均衡器可以将流量路由到自动创建的 \`NodePort\` 服务和 \`ClusterIP\` 服务上。

\> \- [\`ExternalName\`](https://kubernetes.io/zh/docs/concepts/services-networking/service/#externalname)：通过返回 \`CNAME\` 和对应值，可以将服务映射到 \`externalName\` 字段的内容（例如，\`foo.bar.example.com\`）。 无需创建任何类型代理。

clusterIP 内部虚拟IP

NodePort每个节点用一样的静态端口暴露同一个服务

多个service通过clusterIP暴露服务，再通过ingress暴露