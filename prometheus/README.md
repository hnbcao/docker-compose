### Prometheus配置说明

```yaml
# prometheus.yml
# 全局配置
global:
  # scrape_interval: 数据收集频率，默认1分钟（1m）
  scrape_interval: 1m
  # scrape_timeout: 数据收集请求超时时间，默认10秒（10s）
  scrape_timeout: 10s
  # evaluation_interval: 告警规则触发频率，默认1分钟（1m），与altermanager关联。
  evaluation_interval: 10s
  # external_labels: 与外部系统通信时添加到任何时间序列或警报的标签，比如有一个altermanager同时接收多个Prometheus的告警信息，我们可以通过在消息数据中附加external_labels来区分告警消息来自于那个服务。
  external_labels: 
    monitor: prometheus
  # PromQL查询日志文件
  query_log_file: 
# 规则文件指定了一个globs列表,从所有匹配的文件中读取规则和警报.
rule_files:
  - /etc/config/recording_rules.yml
  - /etc/config/alerting_rules.yml
  - /etc/config/rules
  - /etc/config/alerts
# 指标抓取配置列表.
scrape_configs:
  - job_name: 
    scrape_interval: 
    scrape_timeout: 
    metrics_path: /metrics
    # 标签冲突
    honor_labels: false
    # 时间戳，
    honor_timestamps: true
    scheme: http
    # 请求参数
    params: 
    # 认证信息
    basic_auth:
    authorization:
    oauth2:
    follow_redirects: true
    tls_config:

# 警报指定与Alertmanager相关的设置.
alerting:
  alert_relabel_configs:
    [ - <relabel_config> ... ]
  alertmanagers:
    [ - <alertmanager_config> ... ]

# 与远程写入功能相关的设置.
remote_write:
  [ - <remote_write> ... ]

# 与远程读取功能相关的设置.
remote_read:
  [ - <remote_read> ... ]

```