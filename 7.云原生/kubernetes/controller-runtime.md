封装关系

kubebuilder -> controller-runtime -> client-go

\# usage

1 创建manager
\`\`\`
manager, err := ctrl.NewManager(
 ctrl.GetConfigOrDie(),
 ctrl.Options{
 LeaseDuration: &leaseDuration,
 RenewDeadline: &renewDeadline,
 RetryPeriod: &retryPeriod,
 })
\`\`\`
2 创建controller

Complete controller实现Reconcile方法

Reconcile方法调用client对pod信息进行CRUD
\`\`\`
err = ctrl.
 NewControllerManagedBy(manager). // Create the Controller
 For(&appsv1.ReplicaSet{}). // ReplicaSet is the Application API
 Owns(&corev1.Pod{}). // ReplicaSet owns Pods created by it
 Complete(&ReplicaSetReconciler{Client: manager.GetClient()})
\`\`\`
3 start
\`\`\`
if err := manager.Start(ctrl.SetupSignalHandler()); err != nil {
 log.Error(err, "could not start manager")
 os.Exit(1)
 }
\`\`\`