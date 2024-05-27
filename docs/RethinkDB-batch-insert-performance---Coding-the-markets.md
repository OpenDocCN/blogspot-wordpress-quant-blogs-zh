<!--yml

category: 未分类

date: 2024-05-12 19:30:29

-->

# RethinkDB batch insert performance | Coding the markets

> 来源：[`etrading.wordpress.com/2016/11/21/rethinkdb-batch-insert-performance/#0001-01-01`](https://etrading.wordpress.com/2016/11/21/rethinkdb-batch-insert-performance/#0001-01-01)

## RethinkDB 批量插入性能

### 2016 年 11 月 21 日

即将推出的 SpreadServe 的云版本使用基于 Tornado 的服务器来持久化所有在 SpreadServe 中加载的电子表格中使用的公式的分解。对于复杂的表格，我发现许多公式在公式表中的插入可能会耗时。在一个测试场景中，多公式插入花了 5 分钟。所以我去查看了 RethinkDB 的[故障排除页面](https://www.rethinkdb.com/docs/troubleshooting/)，那里有一些有用的性能提示。使用建议的批量大小 200 进行批量插入，将插入时间从 5 分钟降低到 21 秒。进一步的改进来自于使用软持久性和 noreply，将插入时间降低到约 3.5 秒。然而，我发现当插入协程在循环插入批次时，我的 Tornado 服务器无法响应传入的 HTTP GET 请求。我推测 noreply 意味着循环中的 yield 会立即继续，而不等待数据库的回复 IO。去掉 noreply 允许单线程服务器在插入过程中处理 HTTP GET 请求。如果将来需要改进性能，将 Tornado 服务器分成两个进程可能是可行的，但对于当前的测试场景，性能是可以接受的。
