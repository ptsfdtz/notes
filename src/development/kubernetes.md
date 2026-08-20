# kubernetes

Kubernetes 使用声明式资源管理容器化工作负载。常用对象包括 Deployment、Service、ConfigMap、Secret 和 Ingress。

```bash
kubectl get pods -A
kubectl apply -f deployment.yaml
kubectl rollout status deployment/api
kubectl logs deployment/api -f
kubectl rollout undo deployment/api
```

工作负载应配置资源请求与限制、存活/就绪探针和滚动更新策略。Secret 只适合传递敏感配置，不等同于加密的长期密钥库。

## Deployment 例子

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api
spec:
  replicas: 2
  selector:
    matchLabels:
      app: api
  template:
    metadata:
      labels:
        app: api
    spec:
      containers:
        - name: api
          image: example/api:1.0.0
          ports:
            - containerPort: 8080
          readinessProbe:
            httpGet: { path: /health, port: 8080 }
```

## 常用排查

```bash
kubectl describe pod <pod-name>
kubectl get events --sort-by=.lastTimestamp
kubectl exec -it <pod-name> -- sh
kubectl port-forward service/api 8080:80
```

## 经验总结

1. 镜像使用明确版本或提交 SHA，不使用不确定的 `latest`。
2. readiness probe 失败时不会接收流量，适合保护尚未启动完成的服务。
3. 使用 namespace 区分环境，并在执行命令前确认当前 context。
