service-account cluster内部访问

role 配置策略 RoleBinding 角色绑定到账号 ns范围内授权
\`\`\`
kind: ServiceAccount
apiVersion: v1
metadata:
 name: crier
 namespace: prow
\-\-\-
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
 namespace: prow
 name: crier
rules:
\- apiGroups:
 \- "prow.k8s.io"
 resources:
 \- "prowjobs"
 verbs:
 \- "get"
 \- "watch"
 \- "list"
 \- "patch"
\-\-\-
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
 name: crier
 namespace: prow
roleRef:
 apiGroup: rbac.authorization.k8s.io
 kind: Role
 name: crier
subjects:
\- kind: ServiceAccount
 name: crier
 namespace: prow
\`\`\`

clusterRole clusterRoleBinding集群范围内授权

pod <- spec.serviceAccountName -> service-account <-RoleBinding -> Role

通过模版spec.serviceAccountName 指定service account