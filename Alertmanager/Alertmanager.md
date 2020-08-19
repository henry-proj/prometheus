# Alertmanager自身监控规则

## 配置重载错误
```yaml
- alert: Alertmanager配置重载
  expr: alertmanager_config_last_reload_successful != 1
  for: 5m
  labels:
    serverity: "warning"
    service: "kubernetes"
  annotations:
    summary: "Alertmanager配置重载错误"
    description: |
      实例: {{ $labels.instance }}
```
