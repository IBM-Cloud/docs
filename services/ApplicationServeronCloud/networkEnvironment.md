---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Network environment
{: #networkEnvironment}

After your WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} service instance is provisioned, you can access your VM in several ways. You can connect over a secure VPN to get SSH, traditional WebSphere Admin Console, and application access to your VM. You can also connect your VM to the internet with a public IP address.

The following diagram shows these network paths:

Figure 1. Client view of Multi-tenant networking with Public IP

![Figure1. Client view of Multi-tenant networking with Public IP](images/wasaas_multi_tenantPublicIP.gif)

## VPN access
{: #vpnAccess}

After you provision a WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} service instance from the Service Dashboard in the {{site.data.keyword.Bluemix_notm}} UI, you can download your VPN credentials and establish an OpenVPN connection. You can then access your VM through SSH. You can also access your Liberty Admin Center, traditional WebSphere Admin Console, and applications.

## Public internet access
{: #publicInternetAccess}

Optionally, you can request a public IP address for your WebSphere server VM by clicking **Manage Public IP** on the Service Dashboard in the {{site.data.keyword.Bluemix_notm}} UI and requesting a public IP. This process reserves the IP address for this server. Then, click **Open IP** to open the connection from the internet to your WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} service instance.

## Public IP ports
{: #publicIPports}

When you open access to your public IP, the IP address is associated with your VM, and ports 80 and 443 are opened at the gateway. However, by default, Liberty Core, and traditional WebSphere Base servers do not open ports 80 and 443. Conversely, ports 80 and 443 are opened by default on the IBM HTTP Server. Therefore, you might need to configure your Liberty Core and traditional WebSphere Base servers to listen for application traffic on port 80/443 when you use public IP.
* To configure your Liberty Core server, see [Configure Liberty Core Server for public access](networkEnvironment.html#configureLibertyForPublicAccess).
* To configure your traditional WebSphere Base server, add a Web container transport chain listening on port 80/443 as described in [Configuring transport chains](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5//com.ibm.websphere.nd.doc/ae/trun_chain_transport.html){: new_window}.

## VPN private IP ports
{: #privateIPports}

You connect to your VM's private IP address over the VPN connection. Your Liberty Admin Center (9080, 9443), traditional WebSphere Admin Console (9060, 9043), SSH (22), and ports other than 80/443 are only accessible through the VPN connection as depicted in Figure 1. See the sample Liberty Core **server.xml** and **ibm-web-bnd.xml** for details about separating the Liberty Admin Center from your application ports.

**Avoid trouble:** For Liberty Core and traditional WebSphere Base servers, the Firewall ports are preconfigured when your VM is provisioned. However, for Network Deployment configurations where the Deployment manager or the Collective controller is collocated with the IBM HTTP Server, you might need to open ports on the firewall. See [Firewall ports](systemAccess.html#firewall_ports) for details.

## Configure Liberty Core server for Public IP access
{: #configureLibertyForPublicAccess}

You need to configure Liberty Core to listen for application traffic on port 80/443 when you use the public IP.

By default, Liberty is configured with the Liberty Admin Center and applications available on the **default_host** virtual host, which is associated with the **defaultHttpEndpoint** on port 9080 and 9443. Reconfigure your server to separate the Liberty Admin Center from the application virtual host and endpoint and make them available on separate ports.

The following snippet is an example of server.xml configuration adjustments:

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

Now associate your application with the **external_host** virtual host by including the following snippet in your application's **META-INF/ibm-web-bnd.xml** file:

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
