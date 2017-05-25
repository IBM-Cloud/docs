---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 網路環境
{: #networkEnvironment}

佈建 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 服務實例之後，您可以使用數種方式存取 VM。您可以透過安全的虛擬私密網路 (VPN) 連接，以便取得 VM 的 SSH、傳統 WebSphere 管理主控台及應用程式存取。您也可以使用公用 IP 位址將 VM 連接至網際網路。

下圖顯示這些網路路徑：

圖 1. 使用公用 IP 的多方承租戶用戶端畫面

![圖 1. 使用公用 IP 的多方承租戶用戶端畫面](images/wasaas_multi_tenantPublicIP.gif)

## VPN 存取
{: #vpnAccess}

在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，從「服務儀表板」佈建 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 服務實例之後，您可以下載 VPN 認證，並建立 OpenVPN 連線。接著可以透過 SSH 存取 VM。您也可以存取「Liberty 管理中心」、傳統「WebSphere 管理主控台」，以及應用程式。

## 公用網際網路存取
{: #publicInternetAccess}

您可以選擇性地為 WebSphere 伺服器 VM 要求公用 IP 位址，方法是在 {{site.data.keyword.Bluemix_notm}} 使用者介面的「服務儀表板」按一下**管理公用 IP**，然後要求公用 IP。這個處理程序會為這部伺服器保留 IP 位址。然後，按一下**開啟 IP**，以開啟從網際網路到 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 服務實例的連線。

## 公用 IP 埠
{: #publicIPports}

當您開放公用 IP 的存取權時，IP 位址會與您的 VM 相關聯，且會在閘道開啟埠 80 和 443。不過，依預設，Liberty Core 和傳統 WebSphere Base 伺服器不會開啟埠 80 和 443。相反地，IBM HTTP Server 上的埠 80 和 443 會依預設開啟。因此，當您使用公用 IP 時，可能需要配置 Liberty Core 與傳統 WebSphere Base 伺服器，以在埠 80/443 上接聽應用程式資料流量。
* 若要配置 Liberty Core 伺服器，請參閱[配置 Liberty Core 伺服器，以進行公用存取](networkEnvironment.html#configureLibertyForPublicAccess)。
* 若要配置傳統 WebSphere Base 伺服器，請新增一個 Web 容器傳輸鏈，接聽埠 80/443，如[配置傳輸鏈](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5//com.ibm.websphere.nd.doc/ae/trun_chain_transport.html){: new_window}中所述。

## VPN 專用 IP 埠
{: #privateIPports}

您透過 VPN 連線來連接 VM 的專用 IP 位址。您的「Liberty 管理中心」（9080、9443）、傳統「WebSphere 管理主控台」（9060、9043）、SSH (22) 和非 80/443 的埠，只能透過 VPN 連線存取，如圖 1 中所描述。請參閱範例 Liberty Core **server.xml** 和 **ibm-web-bnd.xml**，以取得區隔「Liberty 管理中心」與您應用程式埠的詳細資料。

**避免麻煩：**對於 Liberty Core 和傳統 WebSphere Base 伺服器而言，防火牆埠會在佈建 VM 時預先配置。不過，對於 Network Deployment 配置而言，部署管理程式或群體控制器是與 IBM HTTP Server 並置，因此您可能需要在防火牆上開啟埠。如需詳細資料，請參閱[防火牆埠](systemAccess.html#firewall_ports)。

## 配置 Liberty Core 伺服器的公用 IP 存取
{: #configureLibertyForPublicAccess}

當您使用公用 IP 時，您需要配置 Liberty Core，以在埠 80/443 上接聽應用程式資料流量。

依預設，Liberty 的配置會在 **default_host** 虛擬主機上提供「Liberty 管理中心」以及應用程式，此虛擬主機會與埠 9080 和 9443 上的 **defaultHttpEndpoint** 相關聯。請重新配置伺服器，以區隔「Liberty 管理中心」與應用程式虛擬主機和端點，並在不同的埠上提供它們。

下列 Snippet 是 server.xml 配置調整的範例：

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

現在，請讓您的應用程式與 **external_host** 虛擬主機相關聯，方法是在應用程式的 **META-INF/ibm-web-bnd.xml** 檔中包含下列 Snippet：

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
