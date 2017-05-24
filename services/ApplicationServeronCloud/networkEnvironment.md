---

copyright:
  years: 2015, 2016
lastupdated: "2017-05-24"

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

After you provision a WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} service instance from the Service Dashboard in the {{site.data.keyword.Bluemix_notm}} UI, you can establish an OpenVPN connection by expanding the dropdown menu and downloading your VPN configuration by using the **Download VPN Configuration** button. The VPN configuration contains an **.ovpn** file and certificates that are used to authenticate with the OpenVPN server. Once the OpenVPN connection is established, you can then access your VM through SSH. You can also access your Liberty Admin Center, traditional WebSphere Admin Console, and applications.

The VPN configuration is scoped to your organization and region. It is valid for one year from the time created. Multiple OpenVPN client connections can be established simultaneously by using the same VPN configuration.

**Note:** Your VPN configuration is only valid if your organization contains **active** subscriptions. When the last subscription for an organization is deleted, all the VPN configurations for the organization are suspended. Unexpired VPN configurations are automatically reactivated when a new subscription becomes active.

## Advanced VPN configuration management
{: #advancedVPN}

In most cases, you need only a single VPN configuration that you can download by using the **Download VPN Configuration** button. However, the advanced VPN management page, which is accessed by using the **Advanced VPN Management** button from the Service Dashboard in the {{site.data.keyword.Bluemix_notm}} UI, lets you create and manage multiple VPN configurations. Having multiple configurations might be helpful to transition smoothly to a new VPN configuration when the old one is about to expire. You can also request multiple VPN configurations to manage access to your VMs with different individuals or teams in your organization.  

**Note:** You are allowed a **maximum** of 10 active VPN configurations for your organization at any time.

If your VPN configurations are compromised or expired, you can revoke VPN configuration by using the advanced VPN management page. Additionally, from an audit perspective, you can view a history of all VPN management activity and download active VPN configurations that were created previously from the advanced VPN management page.

All the features available from the Service Dashboard in the {{site.data.keyword.Bluemix_notm}} UI can also be scripted by using our REST APIs. For more information, see the WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} [REST API Documentation](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api#/){: new_window}.

**Note:** Currently, the **Advanced VPN Management** feature is only available in the Frankfurt region.

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
