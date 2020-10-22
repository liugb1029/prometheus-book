# 目录

* [Introduction](README.md)
* [作者](AUTHOR.md)
* [版本变更历史](CHANGELOGS.md)
* [第一章 天降奇兵](./chapter0/README.md)
  * [Prometheus是什么](./sources/what-is-prometheus.md)
  * [Prometheus的核心组件](./sources/prometheus-architecture-and-components.md)
        * Prometheus Server
        * Exporters
        * AlertManager
        * PushGateway
          * Pull Vs Push
  * Prometheus简介
        * 前世今生
        * 适用场景
        * 百里挑一
            * Prometheus Vs Graphite
            * Prometheus Vs InfluxDB
            * Prometheus Vs OpenTSDB
            * Prometheus Vs Nagios
  * [在Linux环境下安装Prometheus](./sources/install_prometheus_in_with_binary.md)
        * [安装Prometheus Server](./sources/install_prometheus_server_with_binary.md)
        * [安装NodeExporter采集主机信息](./sources/install_node_exporter_with_binary.md)
        * [配置Prometheus采集主机信息](./sources/config_prometheus_scarap_node_metrics.md)
        * [验证部署过程](./sources/verify_prometheus_service_install.md)
        * [启用Basic Auth认证](./sources/security_prometheus_enable_http_basic_auth.md)
  * [在Docker环境下安装Prometheus](./sources/install_prometheus_in_docker.md)
        * 使用Docker容器启动Prometheus
        * 使用Docker Compose启动Prometheus
  * [小结](./chapter0/SUMMARY.md)
* [第二章 探索PromQL](sources/exploration_of_promql.md)
  * 什么是Metrics和Lables
  * [Prometheus Query Language](./sources/prometheus-query-language.md)
  * Metrics类型
        * Counter
        * Gauges
        * Histograms
        * Summaries
  * 新的存储层
  * 最佳实践
  * 小结
* 第三章 Prometheus告警处理
  * AlertManaer简介
  * 部署AlertManager
        * 使用二进制包部署AlertManager
        * 使用容器部署AlertManager
  * 自定义Prometheus告警规则
  * 基于Label的动态告警处理
        * 通知对象Receivers
        * 告警路由规则Route
  * 抑制机制 inhibit
  * 告警模板
  * 第三方集成
        * 与邮件系统集成
        * 与Slack集成
        * 与Webhook集成
            * 示例：基于Webhook创建自定义扩展
    * 小结
* 第四章 可视化一切
  * Grafana简介
  * 安装Grafana
        * 使用二进制包安装Grafana
        * 使用容器安装Grafana
  * 使用Prometheus数据源
  * 创建监控Dashboard
        * 自定义Panel
        * 共享你的仪表盘
  * 基于Grafana的告警配置
  * 小结
* 第五章 扩展Prometheus
  * 常用Exporter
        * 使用NodeExporter采集主机数据
        * 使用MysqlExporter采集Mysql Server数据
        * 使用RabbitMQExporter采集RabbitMQ数据
        * 使用Cadvisor采集容器数据
  * [使用Java创建自定义Metrics](sources/custom_metrics_with_java_sdk.md)
  * 使用Golang创建自定义Metrics
  * 扩展Spring Boot应用支持应用指标采集
  * 小结
* 第六章 Prometheus服务发现
  * 基于文件的服务发现
        * 创建文件
        * 配置Prometheus使用基于文件的动态发现
        * 定义刷新时间
  * 基于Consul的服务发现
        * Consul介绍
        * Consul的安装和使用
        * 注册Exporter到Consul
        * 配置Prometheus使用Consul动态发现
  * 小结
* [第七章 运行和管理Prometheus](./chapter7/READMD.md)
  * 数据管理
        * 本地存储
        * 创建快照
  * 远程数据存储
        * 远程读
        * 远程写
  * [分片](./sources/scale-promethues-with-functional-sharding.md)
  * [联邦集群](./sources/scale-prometheus-with-federation.md)
  * 使用Prometheus Opertor管理Prometheus
  * 使用Promgen管理Prometheus
  * 从1.0迁移到2.0
  * [总结](./chapter4/SUMMARY.md)
* 第八章 Kubernetes监控实战
  * Kubernetes简介
  * 搭建Kubernetes本地测试环境
  * Prometheus Vs Heapster
  * 在Kubernetes下部署Prometheus
  * 采集Kubelet状态
  * [采集集群状态](./sources/expose-cluster-level-metrics-with-kube-state-metrics.md)
  * 采集应用资源用量
  * 采集集群节点状态指标
  * 使用Grafana创建可视化仪表盘
  * 基于Prometheus实现应用的弹性伸缩
  * 总结
* [参考资料](./REFERENCES.md)