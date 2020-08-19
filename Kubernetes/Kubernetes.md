# Kubernetes资源对象监控规则

## Node

## Container
### 容器LimitsCPU使用率
```yaml
- alert: 容器 Limits CPU
  expr: (sum(rate(container_cpu_usage_seconds_total{container_name != ""}[3m])) by (pod_name,container_name,instance,namespace) * 100) > 90
  for: 2m
  labels:
    serverity: "warning"
    service: "kubernetes"
  annotations:
    summary: '容器Limits CPU使用率大于90%,当前值是{{ printf "%.2f" $value }}'
    description: |
      命名空间: {{ $labels.namespace }}
      Pod名称: {{ $labels.pod_name }}
      容器名称: {{ $labels.container_name }}
      实例: {{ $labels.instance }}
```
### 容器Limits内存使用率
```yaml
- alert: 容器 Limits 内存
  expr: sum(container_memory_rss{image!=""}) by(pod_name, namespace, container_name) / sum(container_spec_memory_limit_bytes{image!=""}) by(pod_name, namespace,container_name) * 100 != +inf > 90
  for: 2m
  labels:
    serverity: "warning"
    service: "kubernetes"
  annotations:
    summary: '容器Limits内存使用率大于90%,当前值是{{ printf "%.2f" $value }}'
    description: |
      命名空间: {{ $labels.namespace }}
      Pod名称: {{ $labels.pod_name }}
      容器名称: {{ $labels.container_name }}
```

