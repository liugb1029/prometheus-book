# 使用Recoding Rules优化性能

通过PromQL可以实时对Prometheus中采集到的样本数据进行查询，聚合以及其它各种运算操作。而在某些PromQL较为复杂且计算量较大时，直接使用PromQL可能会导致Prometheus响应超时的情况。这时需要一种能够类似于后台批处理的机制能够在后台完成这些复杂运算的计算，对于使用者而言只需要查询这些运算结果即可。Prometheus通过Recoding Rule规则支持这种后台计算的方式，可以实现对复杂查询的性能优化，提高查询效率。

## 定义Recoding rules

在Prometheus配置文件中，通过rule_files定义recoding rule规则文件的访问路径。

```
rule_files:
  [ - <filepath_glob> ... ]
```

每一个规则文件通过以下格式进行定义：

```
groups:
  [ - <rule_group> ]
```

一个简单的规则文件可能是这个样子的：

```
groups:
  - name: example
    rules:
    - record: job:http_inprogress_requests:sum
      expr: sum(http_inprogress_requests) by (job)
```

rule_group的具体配置项如下所示：

```
# The name of the group. Must be unique within a file.
name: <string>

# How often rules in the group are evaluated.
[ interval: <duration> | default = global.evaluation_interval ]

rules:
  [ - <rule> ... ]
```

与告警规则一致，一个group下可以包含多条规则rule。

```
# The name of the time series to output to. Must be a valid metric name.
record: <string>

# The PromQL expression to evaluate. Every evaluation cycle this is
# evaluated at the current time, and the result recorded as a new set of
# time series with the metric name as given by 'record'.
expr: <string>

# Labels to add or overwrite before storing the result.
labels:
  [ <labelname>: <labelvalue> ]
```

在配置的时候，除却 record: <string> 需要注意，其他的基本上是一样的，一个 groups 下可以包含多条规则 rules ，记录和警报规则保存在规则组内，组中的规则以规则的配置时间间隔顺序运算，也就是全局中的 evaluation_interval 设置。

配置范例：
```yaml
groups:
- name: http_requests_total
  rules:
  - record: job:http_requests_total:rate10m
    expr: sum by (job)(rate(http_requests_total[10m]))
    lables:
      team: operations
  - record: job:http_requests_total:rate30m
    expr: sum by (job)(rate(http_requests_total[30m]))
    lables:
      team: operations  
```           
上面的规则其实就是根据record规则中的定义，Prometheus 会在后台完成 expr 中定义的 PromQL 表达式计算过去的指标，以job为维度使用sum聚合运算符计算 http_requests_total 10m内的请求量，并且将计算结果保存到新的时间序列`job:http_requests_total:rate10m`中， 同时还可以通过`labels`为样本数据添加额外的自定义标签。

根据规则中的定义，Prometheus会在后台完成expr中定义的PromQL表达式计算，并且将计算结果保存到新的时间序列`record`中。同时还可以通过labels为这些样本添加额外的标签。

这些规则文件的计算频率与告警规则计算频率一致，都通过global.evaluation_interval定义:

```
global:
  [ evaluation_interval: <duration> | default = 1m ]
```


