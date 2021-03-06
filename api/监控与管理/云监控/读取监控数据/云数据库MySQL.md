## 1. 接口描述

云数据库MySQL（Cloud Database for MySQL）是腾讯云基于全球最受欢迎的开源数据库MySQL专业打造的高性能分布式数据存储服务。具体介绍请参考<a href="/doc/product/236/简介" title="简介">云数据库MySQL</a>页面。
查询云数据库（MySQL）产品监控数据，入参取值如下：
namespace: qce/cdb
维度名称取值：uInstanceId
dimensions.0.name=uInstanceId
dimensions.0.value为cdb实例id


## 2. 输入参数

以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见<a href="/doc/api/405/公共请求参数" title="公共请求参数">公共请求参数</a>页面。其中，此接口的Action字段为GetMonitorData。


<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>必选</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> namespace
<td> 是
<td> String
<td> 命名空间，参见第一小节
<tr>
<td> metricName
<td> 是
<td> String
<td> 指标名称，具体名称见第5小节
<tr>
<td> dimensions.n.name
<td> 是
<td> String
<td> 维度的名称，具体维度名称见第5小节各产品监控指标列表，与dimensions.n.value配合使用。
<tr>
<td> dimensions.n.value
<td> 是
<td> String
<td> 对应的维度的值，具体维度名称见第5小节各产品监控指标列表，与dimensions.n.name配合使用。
<tr>
<td> period
<td> 否
<td> Int
<td> 监控统计周期。默认为取值为300，单位为s。目前CVM支持60s、300s粒度，其他产品支持仅300s。后续将逐步支持更多产品。
<tr>
<td> startTime
<td> 否
<td> Datetime
<td> 起始时间，如”2016-01-01 10:25:00”。 默认时间为当天的”00:00:00”
<tr>
<td> endTime
<td> 否
<td> Datetime
<td> 结束时间，默认为当前时间。 endTime不能小于startTime
</tbody></table>



## 3. 输出参数

<table class="t"><tbody><tr>
<th><b>参数名称</b></th>
<th><b>类型</b></th>
<th><b>描述</b></th>
<tr>
<td> code
<td> Int
<td> 错误码, 0: 成功, 其他值表示失败
<tr>
<td> message
<td> String
<td> 返回信息
<tr>
<td> startTime
<td> Datetime
<td> 起始时间
<tr>
<td> endTime
<td> Datetime
<td> 结束时间
<tr>
<td> metricName
<td> String
<td> 指标名称
<tr>
<td> period
<td> Int
<td> 监控统计周期，单位为s
<tr>
<td> dataPoints
<td> Array
<td> 监控数据列表
</tbody></table>


## 4. 错误码表

| 错误代码 | 错误描述    | 英文描述                                 |
| ---- | ------- | ------------------------------------ |
| -502 | 资源不存在   | OperationDenied.SourceNotExists      |
| -503 | 请求参数有误  | InvalidParameter                     |
| -505 | 参数缺失    | InvalidParameter.MissingParameter    |
| -507 | 超出限制    | OperationDenied.ExceedLimit          |
| -509 | 错误的维度组合 | InvalidParameter.DimensionGroupError |
| -513 | DB操作失败  | InternalError.DBoperationFail        |


## 5. 指标列表
**metricName可选取值范围**

| 指标名称                  | 含义             | 单位     | 维度          |
| --------------------- | -------------- | ------ | ----------- |
| slow_queries          | 慢查询数           | 次/秒    | uInstanceId |
| select_scan           | 全表扫描数          | 次/秒    | uInstanceId |
| select_count          | 查询数            | 次/秒    | uInstanceId |
| com_update            | 更新数            | 次/秒    | uInstanceId |
| com_delete            | 删除数            | 次/秒    | uInstanceId |
| com_insert            | 插入数            | 次/秒    | uInstanceId |
| com_replace           | 覆盖数            | 次/秒    | uInstanceId |
| queries               | 总请求数           | 次/秒    | uInstanceId |
| threads_connected     | 当前打开连接数        | 个      | uInstanceId |
| real_capacity         | 磁盘使用空间         | MB     | uInstanceId |
| capacity              | 磁盘占用空间         | MB     | uInstanceId |
| bytes_sent            | 内网出流量          | Byte/秒 | uInstanceId |
| bytes_received        | 内网入流量          | Byte/秒 | uInstanceId |
| qcache_use_rate       | 缓存使用率          | %      | uInstanceId |
| qcache_hit_rate       | 缓存命中率          | %      | uInstanceId |
| table_locks_waited    | 等待表锁次数         | 次/秒    | uInstanceId |
| created_tmp_tables    | 临时表数量          | 次/秒    | uInstanceId |
| innodb_cache_use_rate | innodb缓存使用率    | %      | uInstanceId |
| innodb_cache_hit_rate | innodb缓存命中率    | %      | uInstanceId |
| innodb_os_file_reads  | innodb读磁盘数量    | 次/秒    | uInstanceId |
| innodb_os_file_writes | innodb写磁盘数量    | 次/秒    | uInstanceId |
| innodb_os_fsyncs      | innodb fsync数量 | 次/秒    | uInstanceId |
| key_cache_use_rate    | myisam缓存使用率    | %      | uInstanceId |
| key_cache_hit_rate    | myisam缓存命中率    | %      | uInstanceId |
| volume_rate           | 容量使用率          | %      | uInstanceId |
| query_rate            | 查询使用率          | %      | uInstanceId |
| qps                   | 每秒执行操作数        | 次/秒    | uInstanceId |
| tps                   | 每秒执行事务数        | 次/秒    | uInstanceId |\

## 6. 示例


**读取云数据库MySQL监控指标示例**

输入

<pre>
https://monitor.api.qcloud.com/v2/index.php?Action=GetMonitorData
&<<a href="https://www.qcloud.com/doc/api/229/6976">公共请求参数</a>>
&namespace=qce/cdb
&metricName=slow_queries
&dimensions.0.name=uInstanceId
&dimensions.0.value=ins-e242adzf
&startTime=2016-06-28 14:10:00
&endTime=2016-06-28 14:20:00
</pre>

输出

```
{
	"code": 0,
	"message": "",
	"metricName": "slow_queries",
	"startTime": "2016-06-28 14:10:00",
	"endTime": "2016-06-28 14:20:00",
	"period": 300,
	"dataPoints": [
		55,
		33
	]
}
```