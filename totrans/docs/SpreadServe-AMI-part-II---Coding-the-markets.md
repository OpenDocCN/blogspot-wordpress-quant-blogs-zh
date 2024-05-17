<!--yml
category: 未分类
date: 2024-05-12 19:30:13
-->

# SpreadServe AMI part II | Coding the markets

> 来源：[https://etrading.wordpress.com/2017/01/17/spreadserve-ami-part-ii/#0001-01-01](https://etrading.wordpress.com/2017/01/17/spreadserve-ami-part-ii/#0001-01-01)

## SpreadServe AMI part II

### January 17, 2017

The core component in a [SpreadServe](http://spreadserve.com) deployment is the SpreadServeEngine, a headless C++ server binary that implements the Excel compatible calculation engine. The engine discovers its hostname through the win32 API using [GetComputerNameExA](https://msdn.microsoft.com/en-us/library/windows/desktop/ms724301(v=vs.85).aspx)( ComputerNameDnsFullyQualified, …). On [AWS](https://aws.amazon.com/) this was giving me hostnames like WIN-THU4IQNRN6F, when what I wanted was the fully qualified domain name, like ec2-54-186-184-85.us-west-2.compute.amazonaws.com. [Harry Johnston](http://english.stackexchange.com/users/77895/harry-johnston) helpfully advised on StackExchange that, since the host is not joined to a domain, GetComputerNameExA will only return the FQDN if I explicitly set it via Control Panel. Naturally I want to avoid manual fixes on a SpreadServe AMI so I settled on using Amazon’s EC2 [instance metadata](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html). The FQDN hostname can be discovered with an HTTP GET on this URL from any EC2 host: http://169.254.169.254/latest/meta-data/public-hostname. I built a small helper server process to query instance metadata using Tornado’s [async HTTPClient](http://www.tornadoweb.org/en/stable/httpclient.html) and write it to the localFS, where SpreadServeEngine can read it. Result: any new SpreadServe AMI will automatically discover its public DNS.