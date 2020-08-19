[TOC]

# Prometheus自身监控规则

## Prometheus配置重载错误
```yaml
- name: Prometheus-rules
  rules:
  - alert: Prometheus配置重载
    expr: prometheus_config_last_reload_successful != 1
    for: 5m
    labels:
      serverity: "warning"
      service: "kubernetes"
    annotations:
      summary: "Prometheus配置重载错误"
      description: |
        实例: {{ $labels.instance }}
```
