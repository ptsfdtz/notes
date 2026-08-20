# prometheus

Prometheus 按固定间隔抓取目标暴露的指标，并使用 PromQL 查询时序数据。

## 指标原则

- Counter 只增不减，适合请求总数和错误总数。
- Gauge 可升可降，适合队列长度和当前连接数。
- Histogram 适合记录延迟和响应大小分布。

示例查询：

```promql
sum(rate(http_requests_total[5m])) by (status)
histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le))
```

避免将用户 ID、请求 ID 等高基数字段设为标签。

## 配置抓取目标

```yaml
scrape_configs:
  - job_name: api
    metrics_path: /metrics
    static_configs:
      - targets: ["api:8080"]
```

## 常用查询

```promql
up
sum(rate(http_requests_total{status=~"5.."}[5m]))
max_over_time(process_resident_memory_bytes[1h])
```

## 经验总结

1. 每个服务都应暴露健康状态、请求量、错误量和延迟指标。
2. 告警表达式应保留一定持续时间，避免短暂抖动触发通知。
3. 指标名称应包含单位，例如 `_seconds`、`_bytes`、`_total`。
