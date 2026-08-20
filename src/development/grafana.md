# grafana

Grafana 用于展示 Prometheus、Loki 等数据源中的指标与日志。

创建仪表盘时，优先围绕服务目标组织面板：吞吐量、错误率、延迟和资源饱和度。告警应给出明确阈值、持续时间、负责人和排查链接，避免针对瞬时波动频繁通知。

## 配置数据源

1. 登录 Grafana，进入 `Connections` -> `Data sources`。
2. 选择 Prometheus，填写地址，例如 `http://prometheus:9090`。
3. 点击 `Save & test`，确认连接成功。

## 面板例子

```promql
sum(rate(http_requests_total[5m])) by (job)
```

时间序列面板适合观察趋势；Stat 面板适合显示当前值；Table 面板适合列出实例和标签。面板标题应写清指标含义和单位。

## 经验总结

1. 仪表盘变量可按环境、服务和实例筛选，减少复制面板。
2. 使用 provisioning 或导出 JSON 管理重要仪表盘，避免只保存在单个账号中。
3. 告警通知附上仪表盘链接和 runbook，方便接收人快速定位。
