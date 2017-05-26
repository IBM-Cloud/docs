---

copyright:
  years: 2015, 2016
lastupdated: "2017-04-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 最新更新
{: #latest_updates}

服务的最新更新的列表。

## 2017 年 3 月 15 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 集成了其他服务维护。
* 升级了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 二进制文件，以便 FP8.5.5.11 或 9.0.0.3 随传统 WebSphere Application Server 的新实例一起安装。
* 解决了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 中的[若干安全漏洞](https://www-01.ibm.com/support/docview.wss?uid=swg22000587){: new_window}，包括：
  * 与库组件相关的未指定漏洞，此漏洞没有机密性和可用性影响，但有高完整性影响。
  * 与库组件相关的未指定漏洞，此漏洞可允许远程黑客使用未知攻击矢量获取敏感信息，导致高机密性影响。
  * 与库组件相关的未指定漏洞，此漏洞可允许远程黑客使用未知攻击矢量生成拒绝服务，导致低可用性影响。
  * OpenSSL 中可能允许远程黑客获取敏感信息的漏洞，此漏洞是由用作 SSL/TLS 协议一部分的 DES/3DES 密码中的错误引起的。
  * 允许用户在 Web UI 中嵌入任意 JavaScript 代码来改变目标功能的漏洞，此漏洞可能会导致在可信会话中泄露凭证。
  * Apache HTTPD 中会受到 HTTP 响应分割攻击的漏洞，此漏洞是由对用户提供的输入不正确验证引起的。
  * Samba 中允许远程已认证黑客获取对系统的提升特权的漏洞，此漏洞是由处理 PAC 校验和失败引起的。
  * Samba 中允许远程已认证黑客获取对系统的提升特权的漏洞，此漏洞是使用 Kerberos 认证将凭单授权凭单 (TGT) 转发给其他服务引起的。
  * Samba 中会导致基于堆的缓冲区溢出的漏洞，此漏洞是由 ndr_pull_dnsp_name() 函数中的整数包装缺陷引起的。


## 2017 年 2 月 10 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 集成了其他服务维护。
* 升级了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 二进制文件，以便 FP8.5.5.11 或 9.0.0.2 随传统 WebSphere Application Server 的新实例一起安装。
* 升级了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 二进制文件，以便 FP16.0.0.4 随 WebSphere Application Server Liberty（核心和 ND 套餐）的新实例一起安装。
* 解决了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 中的[若干安全漏洞](https://www-01.ibm.com/support/docview.wss?uid=swg21997657){: new_window}，包括：
  * 会导致拒绝服务的漏洞，此漏洞是由允许运行来自不可信源的序列化对象引起的，会造成资源耗用。
  * 使用格式不正确的 SOAP 请求，这会允许远程黑客获取敏感信息。


## 2016 年 12 月 16 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 集成了其他服务维护。
* 解决了 IBM SDK Java Technology Edition 中影响 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 的[若干安全漏洞](https://www-01.ibm.com/support/docview.wss?uid=swg21995995){: new_window}，包括：
  * Oracle Java SE 和 Java SE Embedded 中与热点组件相关的未指定漏洞，此漏洞具有高机密性影响、高完整性影响和高可用性影响。
  * Oracle Java SE 和 Java SE Embedded 中与联网组件相关的未指定漏洞，此漏洞可允许远程黑客使用未知攻击矢量获取敏感信息，导致高机密性影响。
  *  IBM WebSphere Application Server 中的跨站点脚本编制漏洞，此漏洞允许用户在 Web UI 中嵌入任意 JavaScript 代码来潜在改变目标功能，从而导致在可信会话中泄露凭证。


## 2016 年 11 月 8 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 已添加客户机为 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} VM 请求[公共 IP](networkEnvironment.html#networkEnvironment) 地址的功能 
* 解决了影响 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 的[若干安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21993842){: new_window}，包括：
  * IBM WebSphere Application Server 中可能允许远程黑客使用不可信源的序列化对象执行任意 Java 代码的漏洞。
  * TS_OBJ_print_bio 函数不限制读取导致的拒绝服务漏洞。远程黑客可能使用特别创建的时间戳记文件利用此漏洞导致应用程序崩溃。
  * OpenSSL 中可能允许远程黑客获取敏感信息的潜在漏洞，该漏洞由用作 SSL/TLS 协议一部分的 64 位块密码上的三重 DES 中错误引起的。通过捕获 SSL/TLS 服务器和客户机之间的大量加密流量，能够进行中间人攻击的远程黑客可能利用此漏洞恢复纯文本数据与获取敏感信息。此漏洞称为“SWEET32 生日”攻击。
  * OpenSSL 中拒绝服务漏洞。远程认证黑客通过重复请求重谈，可能发送过量的 OCSP 状态请求扩展，以使用所有可用内存资源。
  * OpenSSL 中拒绝服务漏洞，这是由 MDC2_Update 函数中整数溢出导致的。远程黑客使用未知的攻击矢量，利用此漏洞发出无限制写入，导致应用程序崩溃。
  * OpenSSL 中允许远程黑客获取敏感信息的潜在漏洞，这是由于 DSA 实施中允许特定操作的非常量时间代码路径追踪错误引起的。黑客使用高速缓存时序攻击利用此漏洞，来恢复私有 DSA 密钥。
  * OpenSSL 中拒绝服务漏洞，这是由解析证书时没有进行消息长度检查导致的。远程认证黑客可利用此漏洞发出无限制读取，并导致拒绝服务。

## 2016 年 9 月 19 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 升级了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 二进制文件，以便 WebSphere Application Server Liberty（核心和 ND 套餐）的新实例安装 FP16.0.0.3。
* 解决了影响 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 的[若干安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21990236){: new_window}，包括：
  *  IBM WebSphere Application Server Liberty 中允许远程黑客进行钓鱼攻击的漏洞。
  * IBM WebSphere Application Server Liberty 中跨站点在 OpenID Connect 客户机进行脚本编制的漏洞。
  * IBM WebSphere Application Server Liberty 中允许远程黑客获取敏感信息的潜在漏洞，这是由于缺省错误页面不存在时不正当地处理异常导致的。
  * Apache Tomcat 中拒绝服务漏洞，由 Apache Commons FileUpload 组件中的错误导致。
  * IBM WebSphere Application Server 和 IBM WebSphere Application Server Liberty 中的漏洞，该漏洞可能允许远程黑客获取敏感信息，由特定条件下对响应的不当处理导致的。
  * 与无机密性影响、低完整性影响和无可用性的联网组件相关的未指定漏洞。

## 2016 年 8 月 17 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 已将 WebSphere Application Server in Bluemix 二进制文件从 8.5.5.9 升级到 8.5.5.10
* 解决了影响 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 的[若干安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window}，包括：
  * 对 WebSphere Application Server 和 WebSphere Application Server Hypervisor Edition 管理控制台有影响的 Apache Struts 漏洞。
  * 使用 SIP 服务时 IBM WebSphere Application Server 中潜在的拒绝服务漏洞。
  * 对 WebSphere Application Server 使用的 IBM HTTP Server 可能有影响的若干漏洞。
  * 可重定向 CGI 应用程序的 HTTP 流量的漏洞，其可能会影响 IBM HTTP Server (IHS)。此漏洞称为“HTTPOXY”。
  * IBM WebSphere Application Server 中的信息披露漏洞。
  * IBM WebSphere Application Server 中潜在的绕过安全限制漏洞（只有启用了 Web 容器定制属性 HttpSessionIdReuse 的环境才会出现该漏洞）。


## 2016 年 6 月 24 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 为客户新增了在创建新的*传统 ND* 或*传统 WebSphere* 实例时，可以选择 V8.5 或 V9.0 的能力。
* 升级了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 二进制文件，以便 WebSphere Application Server Liberty（核心和 ND 套餐）的新实例安装 FP16.0.0.2。16.0.0.2 是 8.5.5.9 之后的下一个修订包。从 16.0.0.2 开始，缺省情况下将安装这些套餐支持的所有授权 Liberty 可选功能部件。
* 解决了影响 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 的[若干安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window}，包括：
  * Apache Standard Taglibs 中的 XML 外部实体注入 (XXE) 漏洞，该漏洞会影响到 IBM WebSphere Application Server。
  * 使用 WebSphere Application Server Liberty 概要文件 API 发现功能部件和 Swagger 文档时，可能会导致降低预期安全性的漏洞。
  * IBM WebSphere Application Server Liberty 管理中心内的潜在信息披露漏洞。
  * IBM WebSphere Application Server 中的潜在 HTTP 响应分割漏洞。
  * 2016 年 5 月 3 日由 OpenSSL Project 披露的 OpenSSL 漏洞。

## 2016 年 6 月 13 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 添加了新功能，使客户可以通过创建使用了 WebSphere Application Server in Bluemix RESTful API 的应用程序或脚本来构建、供应、管理和删除虚拟机实例。
* 添加了新功能，使客户的固定“已停止”实例数控制为 10 个 IP 地址或 64 GB 内存以内。现在，对于“已停止”状态的累计实例，我们向客户减免 5%。

## 2016 年 4 月 26 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 解决了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 中在启用 FIPS 140-2 时的[潜在安全漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window}以及 Samba 中的多个漏洞（包括 Badlock 漏洞）。
* 集成了其他服务维护。

## 2016 年 4 月 15 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}

* 已将 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 二进制文件从 8.5.5.8 升级到 8.5.5.9
* 解决了 IBM {{site.data.keyword.Bluemix_notm}} 的 Liberty for Java 中影响客户使用 OpenID Connect (OIDC) 客户机的[跨站点脚本编制](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window}漏洞。
* 集成了其他服务维护。

## 2016 年 2 月 19 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
* 为应用程序占用大量内存的客户添加了一个选项，以便使用更大型的虚拟机来合理调整其环境的大小。客户可选择具有特定资源大小且最多包含 32 GB RAM 虚拟机的给定 WebSphere Application Server 组件或单个系统。
* 已将 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 二进制文件从 8.5.5.7 升级到 8.5.5.8
* 解决了 IBM SDK Java Technology Edition 中影响 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 的多个漏洞，通常这些漏洞称为 [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}。
* 解决了影响客户使用 OAuth 提供程序输出的[跨站点脚本编制](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window}漏洞。
* 集成了其他服务维护。

## 2015 年 12 月 11 日：更新了 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
* 将正式的产品名称从 IBM Application Server on Cloud in {{site.data.keyword.Bluemix_notm}} 更改为 IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
* 向 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Network Deployment 套餐添加了新功能。该计划包含带有两个或更多虚拟机的 WebSphere Application Server Network Deployment 单元环境。这些新功能允许用户设置集群环境，以用于高可用性、故障转移和可扩展性。
* 向 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Liberty Core 套餐添加了新功能。该计划包含使用 Liberty 集合，作为 Liberty 概要文件（服务器）组的管理域，该集合由两个或更多虚拟机组成
* 已将 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 二进制文件从 8.5.5.6 升级到 8.5.5.7
* 解决了用于处理 Java 对象编组的 [Apache Commons Collection 漏洞](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window}。
* 解决了可能允许 [HTTP 响应分割攻击](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}的漏洞。
* 集成了其他服务维护。

## 2015 年 10 月 15 日：更新了 Application Server on Cloud
* 新增了以下两个新计划：
  * [WebSphere Application Server 传统 V9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* 其他服务维护
