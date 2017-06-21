---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 网络环境
{: #networkEnvironment}

供应 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 服务实例之后，您可以采取几种方式访问 VM。您可以通过安全 VPN 进行连接，以获取 SSH、传统 WebSphere 管理控制台以及应用程序对 VM 的访问权。您还可以使用公共 IP 地址将 VM 连接到互联网。

下图显示这些网络路径：

图 1. 使用公共 IP 的多租户联网的客户机视图

![图 1. 使用公共 IP 的多租户联网的客户机视图](images/wasaas_multi_tenantPublicIP.gif)

## VPN 访问
{: #vpnAccess}

从 {{site.data.keyword.Bluemix_notm}} UI 的服务仪表板供应 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 服务实例之后，您可以下载 VPN 凭证并建立 OpenVPN 连接。然后，您可以通过 SSH 访问 VM。您还可以访问 Liberty 管理中心、传统 WebSphere 管理控制台和应用程序。

## 公共互联网访问
{: #publicInternetAccess}

您可以选择为 WebSphere 服务器 VM 请求公共 IP 地址，方法是在 {{site.data.keyword.Bluemix_notm}} UI 的服务仪表板上单击**管理公共 IP**，并请求公共 IP 地址。此过程为此服务器保留 IP 地址。然后，单击**公开 IP** 以打开从互联网到您的 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 服务实例的连接。

## 公共 IP 端口
{: #publicIPports}

公开公共 IP 的访问权时，IP 地址将与您的 VM 关联，网关的 80 和 443 端口将打开。但是，缺省情况下，Liberty Core 和传统 WebSphere 基础服务器不打开端口 80 和 443。而 IBM HTTP Server 在缺省情况下打开端口 80 和 443。因此，在使用公共 IP 时，您可能需要配置 Liberty Core 和传统 WebSphere 基础服务器来侦听端口 80/443 上的应用程序流量。
* 要配置 Liberty Core 服务器，请参阅[为公共访问权配置 Liberty Core 服务器](networkEnvironment.html#configureLibertyForPublicAccess)。
* 要配置传统 WebSphere 基础服务器，请按[配置传输链](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5//com.ibm.websphere.nd.doc/ae/trun_chain_transport.html){: new_window}中所述，添加 Web 容器传输链来侦听端口 80/443。

## VPN 专用 IP 端口
{: #privateIPports}

您可以通过 VPN 连接到 VM 专用 IP 地址。Liberty 管理中心（9080、9443）、传统 WebSphere 管理控制台（9060、9043）、SSH (22) 以及 80/443 之外的其他端口均仅可以通过图 1 描述的 VPN 连接进行访问。有关将 Liberty 管理中心从应用程序端口分开的详细信息，请参阅样本 Liberty Core **server.xml** 和 **ibm-web-bnd.xml**。

**应避免的问题：**对于 Liberty Core 和传统 WebSphere 基础服务器，供应 VM 时可以预配置防火墙端口。但是，对于 Deployment Manager 或 Collective 控制器与 IBM HTTP Server 并置的 Network Deployment 配置，您可能需要在防火墙上打开端口。请参阅[防火墙端口](systemAccess.html#firewall_ports)以获取详细信息。

## 针对公共 IP 访问配置 Liberty Core 服务器
{: #configureLibertyForPublicAccess}

在使用公共 IP 时，您需要配置 Liberty Core 来侦听端口 80/443 上的应用程序流量。

缺省情况下，使用 Liberty 管理中心和 **default_host** 虚拟主机上可用的应用程序配置 Liberty，该虚拟主机与端口 9080 和 9443 上的 **defaultHttpEndpoint** 相关联。重新配置服务器，以将 Liberty 管理中心与应用程序虚拟主机和端点区分开来，使得它们可用于不同的端口上。

以下片段是调整 server.xml 配置的示例：

```    
    <!-- open port 9080/9443 for incoming http connections -->
    <httpEndpoint id="defaultHttpEndpoint"
        host="*"
        httpPort="9080"
        httpsPort="9443">
        <tcpOptions soReuseAddr="true"/>
    </httpEndpoint>

    <!-- define a new endpoint for public app traffic -->
    <httpEndpoint id="publicHttpEndpoint"
        host="*"
        httpPort="80"
        httpsPort="443">
        <tcpOptions soReuseAddr="true"/>
    </httpEndpoint>

    <!– restrict default_host to vpn so the Liberty Admin Center is not public -->
    <virtualHost id="default_host" allowFromEndpointRef="defaultHttpEndpoint">
      <hostAlias>*:9080</hostAlias>
      <hostAlias>*:9443</hostAlias>
    </virtualHost>

    <virtualHost id="external_host">
      <hostAlias>*:80</hostAlias>
      <hostAlias>*:443</hostAlias>
    </virtualHost>
```
{: codeblock}

现在通过将以下片段包含在应用程序的 **META-INF/ibm-web-bnd.xml** 文件中，将应用程序与 **external_host** 虚拟主机关联：

```
    <?xml version="1.0" encoding="UTF-8"?>
    <web-bnd
        xmlns="http://websphere.ibm.com/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://websphere.ibm.com/xml/ns/javaee   
        http://websphere.ibm.com/xml/ns/javaee/ibm-web-bnd_1_0.xsd"
        version="1.0">

        <virtual-host name="external_host" />
    </web-bnd>
```
{: codeblock}
