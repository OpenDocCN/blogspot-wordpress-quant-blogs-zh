<!--yml

分类：未分类

日期：2024-05-12 19:30:13

-->

# SpreadServe AMI 第二部分 | 编码市场

> 来源：[`etrading.wordpress.com/2017/01/17/spreadserve-ami-part-ii/#0001-01-01`](https://etrading.wordpress.com/2017/01/17/spreadserve-ami-part-ii/#0001-01-01)

## SpreadServe AMI part II

### 2017 年 1 月 17 日

在[SpreadServe](http://spreadserve.com)部署中的核心组件是 SpreadServeEngine，这是一个实现了与 Excel 兼容的计算引擎的无头 C++服务器二进制文件。该引擎通过使用[GetComputerNameExA](https://msdn.microsoft.com/en-us/library/windows/desktop/ms724301(v=vs.85).aspx)( ComputerNameDnsFullyQualified, …) win32 API 发现其主机名。在[AWS](https://aws.amazon.com/)上，这给我的主机名是 WIN-THU4IQNRN6F，而我想要的是完全合格域名，如 ec2-54-186-184-85.us-west-2.compute.amazonaws.com。StackExchange 上的[Harry Johnston](http://english.stackexchange.com/users/77895/harry-johnston)热心建议，由于主机没有加入域，只有通过控制面板明确设置，GetComputerNameExA 才会返回 FQDN。自然地，我想要避免在 SpreadServe AMI 上进行手动修复，所以我决定使用 Amazon 的 EC2[实例元数据](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)。可以通过任何 EC2 主机的 HTTP GET 请求从这个 URL 获取完全合格的主机名：http://169.254.169.254/latest/meta-data/public-hostname。我建立了一个小型助手服务器进程，使用 Tornado 的[异步 HTTP 客户端](http://www.tornadoweb.org/en/stable/httpclient.html)查询实例元数据，并将其写入本地文件系统，SpreadServeEngine 可以从本地文件系统中读取它。结果：任何新的 SpreadServe AMI 都可以自动发现其公共 DNS。
