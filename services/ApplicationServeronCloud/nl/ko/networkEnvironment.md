---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 네트워크 환경
{: #networkEnvironment}

WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스가 프로비저닝되면 다양한 방법으로 VM에 액세스할 수 있습니다. 보안 VPN을 통해 사용자의 VM에 대한 SSH, Traditional WebSphere Admin Console 및 애플리케이션 액세스를 확보할 수 있습니다. 공인 IP 주소로 VM을 인터넷에 연결할 수도 있습니다. 

다음 다이어그램에 해당 네트워크 경로가 표시됩니다. 

그림 1. 공인 IP로 네트워킹하는 다중 테넌트의 클라이언트 보기

![그림1. 공인 IP로 네트워킹하는 다중 테넌트의 클라이언트 보기](images/wasaas_multi_tenantPublicIP.gif)

## VPN 액세스
{: #vpnAccess}

{{site.data.keyword.Bluemix_notm}} UI의 서비스 대시보드에서 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스를 프로비저닝한 후에는 VPN 신임 정보를 다운로드하고 OpenVPN 연결을 설정할 수 있습니다. 그리고 나서 SSH를 통해 VM에 액세스할 수 있습니다. 또한, Liberty Admin Center, Traditional WebSphere Admin Console 및 애플리케이션에 액세스할 수 있습니다. 

## 공용 인터넷 액세스
{: #publicInternetAccess}

선택사항으로 {{site.data.keyword.Bluemix_notm}} UI의 서비스 대시보드에서 **공인 IP 관리**를 클릭하고 공인 IP를 요청하여 WebSphere 서버에 대한 공인 IP 주소를 요청할 수 있습니다. 이 프로세스는 이 서버에 대한 IP 주소를 예약합니다. 그리고 **IP 열기**를 클릭하여 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 서비스 인스턴스에 대한 인터넷의 연결을 여십시오. 

## 공인 IP 포트
{: #publicIPports}

공인 IP에 액세스 권한을 열 때는 IP 주소가 사용자의 VM과 연관되며 포트 80 및 443이 게이트웨이에서 열립니다. 그러나 기본적으로 Liberty Core 및 Traditional WebSphere 기본 서버는 포트 80 및 443을 열지 않습니다. 반대로 포트 80 및 443이 IBM HTTP Server에서 기본적으로 열립니다. 따라서 공인 IP를 사용할 때는 Liberty Core 및 Traditional WebSphere 기본 서버가 포트 80/443에서 애플리케이션 트래픽을 청취하도록 구성해야 할 수 있습니다. 
* Liberty Core 서버를 구성하려면 [공인 액세스용으로 Liberty Core 서버 구성](networkEnvironment.html#configureLibertyForPublicAccess)을 참조하십시오. 
* Traditional WebSphere 기본 서버를 구성하려면 [전송 체인 구성](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5//com.ibm.websphere.nd.doc/ae/trun_chain_transport.html){: new_window}에 설명된 대로 포트 80/443에서 청취하는 웹 컨테이너 전송 체인을 추가하십시오.

## VPN 사설 IP 포트
{: #privateIPports}

VPN 연결을 통해 VM의 사설 IP 주소에 연결합니다. Liberty Admin Center(9080, 9443), Traditional WebSphere Admin Console(9060, 9043), SSH(22) 및 80/443 이외의 포트만 그림 1에 표현된 대로 VPN 연결을 통해 액세스 가능합니다. 애플리케이션 포트에서 Liberty Admin Center 분리하기에 대한 세부사항은 샘플 Liberty Core **server.xml** 및 **ibm-web-bnd.xml**을 참조하십시오. 

**문제점 예방:** Liberty Core 및 Traditional WebSphere 기본 서버의 경우, VM이 프로비저닝될 때 방화벽 포트가 사전 구성됩니다. 그러나 배치 관리자 또는 Collective Controller가 IBM HTTP Server와 함께 배치된 Network Deployment 구성의 경우, 방화벽에 포트를 열어야 할 수 있습니다. 세부사항은 [방화벽 포트](systemAccess.html#firewall_ports)를 참조하십시오. 

## 공인 IP 액세스용으로 Liberty Core 서버 구성
{: #configureLibertyForPublicAccess}

공인 IP를 사용할 때는 Liberty Core가 포트 80/443에서 애플리케이션 트래픽을 청취하도록 구성해야 합니다. 

기본적으로 Liberty는 Liberty Admin Center 및 **default_host** 가상 호스트에서 사용 가능한 애플리케이션과 함께 구성되며, 포트 9080 및 9443의 **defaultHttpEndpoint**와 연관되어 있습니다. 애플리케이션 가상 호스트 및 엔드포인트에서 Liberty Admin Center를 분리하도록 서버를 다시 구성하여 별도의 포트에서 사용 가능하게 하십시오. 

다음 스니펫은 server.xml 구성 조정의 예입니다.

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

이제 사용자 애플리케이션의 **META-INF/ibm-web-bnd.xml** 파일에 다음 스니펫을 포함하도록 해서 사용자의 애플리케이션을 **external_host** 가상 호스트와 연관시키십시오. 

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
