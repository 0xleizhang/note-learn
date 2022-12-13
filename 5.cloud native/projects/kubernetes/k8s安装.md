export https\_proxy=http://127.0.0.1:7890 http\_proxy=http://127.0.0.1:7890 all\_proxy=socks5://127.0.0.1:7891

brew install hyperkit

minikube start --driver=hyperkit --image-mirror-country=cn  --image-repository=registry.cn-hangzhou.aliyuncs.com/google\_containers --iso-url=https://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/iso/minikube-v1.13.0.iso

kubeadm

minikube .minikube

kubectl .kube/config \_\`kubectl\` 在 $HOME/.kube 目录中寻找一个名为 config 的文件 \_

\_kubectl client工具通过config文件找到服务端\_
\`\`\`
apiVersion: v1
clusters:
\- cluster:
 certificate-authority: /Users/seven/.minikube/ca.crt
 server: https://192.168.64.2:8443
 name: minikube
contexts:
\- context:
 cluster: minikube
 user: minikube
 name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
\- name: minikube
 user:
 client-certificate: /Users/seven/.minikube/profiles/minikube/client.crt
 client-key: /Users/seven/.minikube/profiles/minikube/client.key
\`\`\`

\`\`\`
kubectl create deployment hello-minikube --image=registry.cn-hangzhou.aliyuncs.com/google\_containers/echoserver:1.10
kubectl expose deployment hello-minikube --type=NodePort --port=8080
minikube service hello-minikube --url
\`\`\`
[redis-master-service.yml](https://www.yuque.com/attachments/yuque/0/2020/yml/290656/1599325519184-4cf43241-7530-48a8-bafd-8eaced1dad74.yml?\_lake\_card=%7B%22uid%22%3A%221599325518981-0%22%2C%22src%22%3A%22https%3A%2F%2Fwww.yuque.com%2Fattachments%2Fyuque%2F0%2F2020%2Fyml%2F290656%2F1599325519184-4cf43241-7530-48a8-bafd-8eaced1dad74.yml%22%2C%22name%22%3A%22redis-master-service.yml%22%2C%22size%22%3A233%2C%22type%22%3A%22application%2Fx-yaml%22%2C%22ext%22%3A%22yml%22%2C%22progress%22%3A%7B%22percent%22%3A99%7D%2C%22status%22%3A%22done%22%2C%22percent%22%3A0%2C%22id%22%3A%22qsRSe%22%2C%22card%22%3A%22file%22%7D)[redis-master-deployment.yml](https://www.yuque.com/attachments/yuque/0/2020/yml/290656/1599325519364-4dfd9ae5-b1c4-417e-9a1c-1dc5e037061a.yml?\_lake\_card=%7B%22uid%22%3A%221599325518981-1%22%2C%22src%22%3A%22https%3A%2F%2Fwww.yuque.com%2Fattachments%2Fyuque%2F0%2F2020%2Fyml%2F290656%2F1599325519364-4dfd9ae5-b1c4-417e-9a1c-1dc5e037061a.yml%22%2C%22name%22%3A%22redis-master-deployment.yml%22%2C%22size%22%3A571%2C%22type%22%3A%22application%2Fx-yaml%22%2C%22ext%22%3A%22yml%22%2C%22progress%22%3A%7B%22percent%22%3A99%7D%2C%22status%22%3A%22done%22%2C%22percent%22%3A0%2C%22id%22%3A%22fwXA5%22%2C%22card%22%3A%22file%22%7D)

善用 --help