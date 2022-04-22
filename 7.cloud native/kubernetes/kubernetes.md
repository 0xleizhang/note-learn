OCI Open Container Initiative

这是一个关于容器格式和运行时的规范文件，其中包含了运行时标准（runtime-spec ）、容器镜像标准（image-spec）和镜像分发标准（distribution-spec，分发标准还未正式发布）

​

CRI “容器运行时接口”Container Runtime Interface，

​

CNI（Container Networking Interface）

​

CSI（Container Storage Interface）

​

​

​

​

​

runC 是 OCI Runtime

containerd

cri-containerd

docker-shim

cri-o

![image.png](1639039778688-0e940155-e940-4a50-ba58-e06115988337.png)

![image.png](1639040090674-eba64056-9621-4d0f-ba61-0fd5b591772a.png)

kubernetes 目前：

Kubernetes Master → kubelet → KubeGenericRuntimeManager → containerd → runC