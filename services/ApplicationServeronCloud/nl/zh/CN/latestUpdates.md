---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 最新更新
{: #latest_updates}

服务的最新更新的列表。

## 2016 年 11 月 8 日：更新了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 已添加客户机为 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} VM 请求[公共 IP](networkEnvironment.html#networkEnvironment) 地址的功能 
* 解决了影响 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 的[若干安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21993842){: new_window}，包括：
  * IBM WebSphere Application Server 中可能允许远程黑客使用不可信源的序列化对象执行任意 Java 代码的漏洞。
  * TS_OBJ_print_bio 函数不限制读取导致的拒绝服务漏洞。远程黑客可能使用特别创建的时间戳记文件利用此漏洞导致应用程序崩溃。
  * OpenSSL 中可能允许远程黑客获取敏感信息的潜在漏洞，该漏洞由用作 SSL/TLS 协议一部分的 64 位块密码上的三重 DES 中错误引起的。通过捕获 SSL/TLS 服务器和客户机之间的大量加密流量，能够进行中间人攻击的远程黑客可能利用此漏洞恢复纯文本数据与获取敏感信息。此漏洞称为“SWEET32 生日”攻击。
  * OpenSSL 中拒绝服务漏洞。远程认证黑客通过重复请求重谈，可能发送过量的 OCSP 状态请求扩展，以使用所有可用内存资源。
  * OpenSSL 中拒绝服务漏洞，这是由 MDC2_Update 函数中整数溢出导致的。远程黑客使用未知的攻击矢量，利用此漏洞发出无限制写入，导致应用程序崩溃。
  * OpenSSL 中允许远程黑客获取敏感信息的潜在漏洞，这是由于 DSA 实施中允许特定操作的非常量时间代码路径追踪错误引起的。黑客使用高速缓存时序攻击利用此漏洞，来恢复私有 DSA 密钥。
  * OpenSSL 中拒绝服务漏洞，这是由解析证书时没有进行消息长度检查导致的。远程认证黑客可利用此漏洞发出无限制读取，并导致拒绝服务。

## 2016 年 9 月 19 日：更新了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 升级了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 二进制文件，以便 WebSphere Application Server Liberty（核心和 ND 套餐）的新实例将安装 FP16.0.0.3。
* 解决了影响 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 的[若干安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21990236){: new_window}，包括：
  *  IBM WebSphere Application Server Liberty 中允许远程黑客进行钓鱼攻击的漏洞。
  * IBM WebSphere Application Server Liberty 中跨站点在 OpenID Connect 客户机进行脚本编制的漏洞。
  * IBM WebSphere Application Server Liberty 中允许远程黑客获取敏感信息的潜在漏洞，这是由于缺省错误页面不存在时不正当地处理异常导致的。
  * Apache Tomcat 中拒绝服务漏洞，由 Apache Commons FileUpload 组件中的错误导致。
  * IBM WebSphere Application Server 和 IBM WebSphere Application Server Liberty 中的漏洞，该漏洞可能允许远程黑客获取敏感信息，由特定条件下对响应的不当处理导致的。
  * 与无机密性影响、低完整性影响和无可用性的 Networking 组件相关的未指定漏洞。

## 2016 年 8 月 17 日：更新了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 将 WebSphere Application Server for Bluemix 二进制从 8.5.5.9 升级到 8.5.5.10
* 解决了影响 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 的[若干安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window}，包括：
  * 对 WebSphere Application Server 和 WebSphere Application Server Hypervisor Edition 管理控制台有影响的 Apache Struts 漏洞。
  * 使用 SIP 服务时 IBM WebSphere Application Server 中潜在的拒绝服务漏洞。
  * 对 WebSphere Application Server 使用的 IBM HTTP Server 可能有影响的若干漏洞。
  * 可重定向 CGI 应用程序的 HTTP 流量的漏洞，其可能会影响 IBM HTTP Server (IHS)。此漏洞称为“HTTPOXY”。
  * IBM WebSphere Application Server 中的信息披露漏洞。
  * IBM WebSphere Application Server 中潜在的绕过安全限制漏洞（只有启用了 Web 容器定制属性 HttpSessionIdReuse 的环境才会出现该漏洞）。


## 2016 年 6 月 24 日：更新了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 为客户新增了在创建新的*传统 ND* 或*传统 WebSphere* 实例时，可以选择 V8.5 或 V9.0 的能力。
* 升级了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 二进制文件，以便 WebSphere Application Server Liberty（核心和 ND 套餐）的新实例安装 FP16.0.0.2。16.0.0.2 是 8.5.5.9 之后的下一个修订包。从 16.0.0.2 开始，缺省情况下将安装这些套餐支持的所有授权 Liberty 可选功能部件。
* 解决了影响 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 的[若干安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window}，包括：
  * Apache Standard Taglibs 中的 XML 外部实体注入 (XXE) 漏洞，该漏洞会影响到 IBM WebSphere Application Server。
  * 使用 WebSphere Application Server Liberty 概要文件 API 发现功能部件和 Swagger 文档时，可能会导致降低预期安全性的漏洞。
  * IBM WebSphere Application Server Liberty 管理中心内的潜在信息披露漏洞。
  * IBM WebSphere Application Server 中的潜在 HTTP 响应分割漏洞。
  * 2016 年 5 月 3 日由 OpenSSL Project 披露的 OpenSSL 漏洞。

## 2016 年 6 月 13 日：更新了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 添加了新功能，使客户可以通过创建使用了 WebSphere Application Server for Bluemix RESTful API 的应用程序或脚本来构建、供应、管理和删除虚拟机实例。
* 添加了新功能，使客户的固定“已停止”实例数控制为 10 个 IP 地址或 64 GB 内存以内。现在，对于“已停止”状态的累计实例，我们向客户减免 5%。

## 2016 年 4 月 26 日：更新了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 解决了关于 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 在启用 FIPS 140-2 时 Samba 中出现多个漏洞（包括 Badlock 漏洞）的[潜在安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window}问题。
* 集成了其他服务维护。

## 2016 年 4 月 15 日：更新了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* 已将 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 二进制从 8.5.5.8 升级到 8.5.5.9
* 解决了 IBM {{site.data.keyword.Bluemix_notm}} 的 Liberty for Java 中影响客户使用 OpenID Connect (OIDC) 客户机的[跨站点脚本编制](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window}漏洞。
* 集成了其他服务维护。

## 2016 年 2 月 19 日：更新了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* 为应用程序占用大量内存的客户添加了一个选项，以便使用更大型的虚拟机来合理调整其环境的大小。客户可选择具有特定资源大小且最多包含 32 GB RAM 虚拟机的给定 WebSphere Application Server 组件或单个系统。
* 将 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 二进制从 8.5.5.7 升级到 8.5.5.8
* 解决了 IBM SDK Java Technology Edition 中影响 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 运行的多个漏洞，通常将其称为 [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}。
* 解决了影响客户使用 OAuth 提供程序输出的[跨站点脚本编制](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window}漏洞。
* 集成了其他服务维护。

## 2015 年 12 月 11 日：更新了 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* 将正式的产品名称从 IBM Application Server on Cloud for {{site.data.keyword.Bluemix_notm}} 更改为 IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* 向 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment 计划添加了新功能。该计划包含带有两个或更多虚拟机的 WebSphere Application Server Network Deployment 单元环境。这些新功能允许用户设置集群环境，以用于高可用性、故障转移和可扩展性。
* 向 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core 计划添加了新功能。该计划包含使用 Liberty 集合，作为 Liberty 概要文件（服务器）组的管理域，该集合由两个或更多虚拟机组成
* 将 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 二进制从 8.5.5.6 升级到 8.5.5.7
* 解决了用于处理 Java 对象编组的 [Apache Commons Collection 漏洞](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window}。
* 解决了可能允许 [HTTP 响应分割攻击](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}的漏洞。
* 集成了其他服务维护。

## 2015 年 10 月 15 日：更新了 Application Server on Cloud
* 新增了以下两个新计划：
  * [WebSphere Application Server 传统 V9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* 其他服务维护
