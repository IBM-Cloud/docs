---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 配置外部日志主机
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} 会在内存中保留数量有限的日志信息。记录信息时，较新的信息会将旧的信息替换掉。要保留所有日志信息，可以将日志保存到外部日志主机，例如第三方日志管理服务或其他主机。
{:shortdesc}

要将应用程序和系统中的日志流式传输到外部日志主机，请完成以下步骤：

  1. 确定日志记录端点。

	 可以将日志发送到第三方日志聚集器，例如 Papertrail、Splunk 或 Sumologic。还可以将日志发送到 syslog 主机、使用 TLS（传输层安全性）加密的 syslog 主机或 HTTPS POST 端点。对于不同的日志主机，用于获取日志记录端点的方法有所不同。

  2. 创建用户提供的服务实例。

	 使用 `cf create-user-provided-service` 命令（或此命令的简短版本 `cups`）来创建用户提供的服务实例：
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 &lt;service_name&gt;
	 
	 用户提供的服务实例的名称。

	 &lt;logging_endpoint&gt;

	 {{site.data.keyword.Bluemix_notm}} 向其发送日志的日志记录端点。请参阅下表，以将 *logging_endpoint* 替换为您的值：

	 <table>
	 <caption>表 1. 日志记录端点值</caption>
     <thead>
     <tr>
     <th>日志记录端点</th>
     <th>命令</th>
	 <th>注释</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog 主机</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>例如，要允许将日志记录到 Papertrail，请输入 `cf cups my-logs -l syslog://<papertrail-url>`。将 `<papertrail-url>` 替换为 Papertrail 中您的日志记录端点的 URL。</td>
     </tr>
	 <tr>
     <td>syslog-tls 主机</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>证书必须受认证中心信任。不要使用自签名证书。</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>此端点必须位于公共因特网上，并可由 {{site.data.keyword.Bluemix_notm}} 进行访问</td>
     </tr>
     </tbody>
     </table>
  3. 将服务实例与应用程序绑定。

	 使用以下命令将服务实例绑定到应用程序：

	 ```
	 cf bind-service <appname> <service_name>
	 ```
	 &lt;appname&gt;
	 
	 应用程序的名称。

	 &lt;service_name&gt;

	 用户提供的服务实例的名称。

  4. 重新编译打包应用程序。键入 `cf restage appname` 以使更改生效。

