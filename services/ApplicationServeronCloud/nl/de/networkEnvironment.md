---

Copyright:
  Jahre: 2015, 2016
Letzte Aktualisierung: 28.10.2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Netzumgebung
{: #networkEnvironment}

Nach der Bereitstellung der WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}-Serviceinstanz gibt es verschiedene Möglichkeiten für den Zugriff auf die VMs. Sie können über ein sicheres VPN eine Verbindung herstellen, um über SSH, die klassische WebSphere-Administrationskonsole oder Anwendungen auf eine VM zuzugreifen+++. Außerdem kann die VM über eine öffentliche IP-Adresse mit dem Internet verbunden werden.

Im folgenden Diagramm sind die Netzpfade dargestellt:

Abbildung 1. Clientansicht des Multi-Tenant-Netzbetriebs mit öffentlicher IP-Adresse

![Abbildung 1. Clientansicht des Multi-Tenant-Netzbetriebs mit öffentlicher IP-Adresse](images/wasaas_multi_tenantPublicIP.gif)

## VPN-Zugriff
{: #vpnAccess}

Nach der Bereitstellung einer WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}-Serviceinstanz über das Service-Dashboard in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle können Sie Ihre VPN-Berechtigungsnachweise herunterladen und eine OpenVPN-Verbindung herstellen. Anschließend können Sie über SSH auf Ihre VM zugreifen. Ferner können Sie auf das Liberty Admin Center, die klassische WebSphere-Administrationskonsole und Anwendungen zugreifen.

## Zugriff auf das öffentliche Internet
{: #publicInternetAccess}

Optional können Sie eine öffentliche IP-Adresse für die VM des WebSphere-Servers anfordern. Klicken Sie dazu im Service-Dashboard in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle auf **Öffentliche IP verwalten** und fordern Sie eine öffentliche IP-Adresse an. Bei diesem Prozess wird die IP-Adresse für den betreffenden Server reserviert. Klicken Sie anschließend auf **IP öffnen**, um die Internetverbindung für die WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}-Serviceinstanz zu öffnen.

## Ports für öffentliche IP
{: #publicIPports}

Wenn Sie den Zugriff auf die öffentliche IP öffnen, wird die IP-Adresse der VM zugeordnet, und die Ports 80 und 443 werden am Gateway geöffnet. Die Ports 80 und 443 werden von Liberty Core-Servern und klassischen WebSphere-Basisservern jedoch nicht standardmäßig geöffnet. Im IBM HTTP Server werden diese Ports dagegen standardmäßig geöffnet. Deshalb müssen Sie Liberty Core-Server und klassische WebSphere-Basisserver bei der Verwendung einer öffentlichen IP-Adresse möglicherweise so konfigurieren, dass sie an Port 80/443 für Anwendungsdatenverkehr empfangsbereit sind.
* Informationen zur Konfiguration des Liberty Core-Servers finden Sie in [Liberty Core-Server für öffentlichen Zugriff konfigurieren](networkEnvironment.html#configureLibertyForPublicAccess).
* Fügen Sie zum Konfigurieren des klassischen WebSphere-Basisservers eine Web-Container-Transportkette hinzu, die an Port 80/443 empfangsbereit ist. Weitere Informationen hierzu finden Sie in [Transportketten konfigurieren](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5//com.ibm.websphere.nd.doc/ae/trun_chain_transport.html){: new_window}.

## VPN-Ports für private IP
{: #privateIPports}

Über die VPN-Verbindung können Sie eine Verbindung zur privaten IP-Adresse der VM herstellen. Der Zugriff auf das Liberty Admin Center (9080, 9443), die klassische WebSphere-Administrationskonsole, SSH (22) und andere Ports als 80/443 ist nur über die VPN-Verbindung möglich (siehe Abbildung 1). Informationen dazu, wie Sie das Liberty Admin Center von den Anwendungsports trennen können, enthalten die Liberty Core-Beispieldateien **server.xml** und **ibm-web-bnd.xml**.

**Störungen vermeiden**: Im Falle von Liberty Core-Servern und klassischen WebSphere-Basisservern sind die Firewall-Ports bei der Bereitstellung der VM vorkonfiguriert. Bei Network Deployment-Konfigurationen, in denen der Deployment Manager oder der Verbundcontroller mit dem IBM HTTP Server kollokiert ist, müssen jedoch möglicherweise Ports an der Firewall geöffnet werden. Einzelheiten hierzu finden Sie in [Firewall-Ports](systemAccess.html#firewall_ports).

## Liberty Core-Server für Zugriff auf öffentliche IP-Adresse konfigurieren
{: #configureLibertyForPublicAccess}

Bei Verwendung einer öffentlichen IP-Adresse müssen Sie den Liberty Core-Server so konfigurieren, dass er für Anwendungsdatenverker an Port 80/443 empfangsbereit ist.

Liberty ist standardmäßig so konfiguriert, dass das Liberty Admin Center und die Anwendungen auf dem virtuellen Host **default_host** zur Verfügung stehen, der **defaultHttpEndpoint** an Port 9080 und 9443 zugeordnet wird. Rekonfigurieren Sie den Server, um das Liberty Admin Center vom virtuellen Host und Endpunkt der Anwendungen zu trennen und an separaten Ports verfügbar zu machen.

Das folgende Snippet ist ein Beispiel für Konfigurationsanpassungen an der Datei 'server.xml':

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

Ordnen Sie die Anwendung nun dem virtuellen Host **external_host** zu, indem Sie das folgende Snippet in die Datei **META-INF/ibm-web-bnd.xml** der Anwendung einfügen:

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
