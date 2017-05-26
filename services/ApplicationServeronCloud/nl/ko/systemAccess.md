---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#시스템 액세스
{: #system_access}


시스템에 액세스하고 액세스를 설정하는 다양한 방법과 함께 서비스 인스턴스 작성 및 관리 방법이 이 섹션에서 논의됩니다.
{: shortdesc}


## WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}에서 REST API 사용
{: #restapi_usage}

WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}의 인스턴스는 다음 방법 중 하나로 작성, 프로비저닝, 관리 및 삭제됩니다. 

* {{site.data.keyword.Bluemix_notm}} UI의 {{site.data.keyword.Bluemix_notm}} 카탈로그 및 서비스 대시보드에서.
* RESTful API를 사용하는 애플리케이션 또는 스크립트의 작성에서.

Swagger 2.0 호환 REST API를 사용하여 클라이언트는 포털과 대시보드를 통해 제공된 것과 동일한 기능에 액세스합니다. 지원되는 REST API 및 리소스에 대한 추가 정보는 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} [REST API 문서](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api#/){: new_window}를 참조하십시오. REST API를 사용하는 예를 보여주는 샘플 코드를 가져오려면 Git 호스팅 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} [REST API 샘플](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window}을 다운로드하십시오. 

**참고:** 서비스 인스턴스를 작성한 후 작성된 Tee-Shirt 크기에 따라 서비스를 즉각 사용하지 못할 수도 있습니다. 서비스 인스턴스의 현재 상태를 판별하도록 리턴된 JSON의 **상태** 필드를 조회할 것을 권장합니다.

**참고:** [REST API 샘플](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window}에서 참조되는 **apiEndpoint** URL은 미국 남부 지역을 가리킵니다. 다른 지역을 사용 중인 경우 애플리케이션에서 적합한 **apiEndpoint**를 참조하는지 확인하십시오.

*표 1. Rest API 구현을 위한 API 엔드포인트 URL*

| **지역 이름** | **지리적 위치** | **지역 접두부** | **API 엔드포인트 URL** |       
|:-------------:|:----------:|:--------------:|:-------------:|
| 미국 남부 | 댈러스, 텍사스, 미국 | ng | https://wasaas-broker.ng.bluemix.net/wasaas-broker/api  |
| 영국 | 런던, 영국 | eu-gb | https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api  |
| 시드니 | 시드니, 호주 | au-syd | https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api  |
| 프랑크푸르트 | 프랑크푸르트, 독일 | eu-de | https://wasaas-broker.eu-de.bluemix.net/wasaas-broker/api  |



## 서비스 대시보드
{: #service_dashboard}

서비스 인스턴스를 작성하고 나면 서비스 대시보드로 이동됩니다. 조직 대시보드의 서비스 아이콘을 클릭하여 언제든 서비스 대시보드로 되돌아갈 수 있습니다.
서비스 대시보드에서 다음에 액세스할 수 있습니다.

* 이 문서의 링크
* 필요한 OpenVPN 구성 파일을 다운로드하기 위한 링크
* 가상 머신을 시작하고 중지하는 기능. 처음에 VM이 시작됨
* 호스트 이름
* 관리 사용자 및 관리자 비밀번호
* 개인용 SSH 키 
* WebSphere® 관리 사용자 및 관리자 비밀번호
* Admin Center 및 Admin Console URLS

**참고**: 특정 양의 컴퓨팅, 메모리 및 입출력 리소스로 인해, 클라이언트가 5% 감소 비율로 중지된 상태의 누적 VM에 대해 청구됩니다. 클라이언트는 10개 이하의 IP 주소 또는 64GB 이하 메모리를 사용하는 고정된 수의 중지된 인스턴스에 관리됩니다. 


## WebSphere Application Server in Bluemix 인스턴스의 openVPN 설정
{: #setup_openvpn}

OpenVPN은 WebSphere Application Server in Bluemix 가상 머신에 액세스하는 데 필요합니다. 관리자 권한으로 설치하고 실행 중이어야 합니다.

### 다음 지시사항을 사용하여 Windows에서 openVPN을 설정하십시오. 

1. [openVPN Windows 다운로드](http://swupdate.openvpn.org/community/releases/) 링크에서 다운로드하십시오.
  * 64비트의 경우, [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window} 또는
  * 32비트의 경우, [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window}
2. 반드시 [Windows 관리자로 실행](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}하고 openVPN이 설치되어 있어야 합니다.
3. 서비스 대시보드의 WebSphere Application Server in Bluemix 인스턴스의 OpenVPN 다운로드 링크에서 VPN 구성 파일을 다운로드하십시오. 압축 파일의 네 개 파일을 모두 **{OpenVPN home}\config** 디렉토리에 추출하십시오. 예: 

  <pre>  
    C:\Program Files\OpenVPN\Config
  </pre>
  {: codeblock}

4. openVPN 클라이언트 프로그램 "OpenVPN GUI"를 시작하십시오. 반드시 [Windows 관리자로 실행](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}을 선택해서 프로그램을 시작하십시오. 그렇지 않으면 연결하지 못할 수 있습니다.

### 다음 지시사항을 사용하여 Linux에서 openVPN을 설정하십시오. 
1. openVPN을 설치하려면 [지시사항](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}을 따르십시오.
  * RPM Package Manager를 수동으로 다운로드하고 설치해야 하는 경우 [openVPN Unix/Linux 다운로드](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}로 이동하십시오. Linux 관리자의 도움이 필요할 수 있습니다.
3. 서비스 대시보드의 WebSphere Application Server in Bluemix 인스턴스의 OpenVPN 다운로드 링크에서 VPN 구성 파일을 다운로드하십시오. openVPN 클라이언트를 시작하려는 디렉토리에 파일의 압축을 푸십시오. 네 파일이 모두 같은 디렉토리에 있어야 합니다.
3. openVPN 클라이언트 프로그램을 시작하십시오. 터미널 창을 열고 구성 파일이 포함된 디렉토리로 이동하십시오. 루트로 다음 명령을 실행하십시오. 

  <pre>
      $ openvpn --config vt-wasaas-wasaas.ovpn
  </pre>
  {: codeblock}  

### 다음 지시사항을 사용하여 Mac에서 openVPN을 구성하십시오. 
1. 오픈 소스 소프트웨어 제품인 [Tunnelblick](https://tunnelblick.net/){: new_window}를 설치하는 것이 한 방법입니다. 
2. WebSphere 서비스에서 VPN 구성 파일의 압축을 푸십시오. Tunnelblick에서 Mac의 관리자 비밀번호를 입력하도록 프롬프트를 표시하고 연결하는 데 사용할 수 있는 VPN 세트에 구성을 추가합니다.
3. VPN 네트워크에 연결하고 나서 가상 머신에 액세스할 수 있습니다. 사용자가 처음 액세스한 후에 Tunnelblick에서 구성을 캐시하면 [Tunnelblick](https://tunnelblick.net/){: new_window}에서 연결할 수 있습니다. 쉽게 액세스하려면 맨 위 메뉴 표시줄에 아이콘을 둘 수 있습니다.


## SSH를 사용하여 WebSphere Application Server in Bluemix VM에 액세스
{: #using_ssh}

이러한 지시사항에서는 OpenSSH를 클라이언트로 사용한다고 가정합니다. OpenSSH는 일반적으로 Linux 또는 Windows에서 실행 중인 Cygwin에서 사용할 수 있습니다. Windows 명령 프롬프트에서 실행하도록 설치할 수도 있습니다.

OpenSSH의 설치를 확인하려면 다음 명령을 입력하십시오.
  ```
      $ ssh -V
  ```
  {: codeblock}

다음 메시지는 응답의 예입니다.
  ```
      OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

다음 지시사항을 사용하여 WebSphere Application Server in Bluemix VM에 대한 SSH 액세스를 설정하십시오. 

1. 사용자가 처음 연결할 때 표시되는 경고 메시지, "호스트 x.x.x.x의 인증을 확립할 수 없습니다."를 검토하십시오. 이 메시지는 정상입니다. 프롬프트가 표시되면 예를 선택하십시오. 공개 키가 이제 사용자 virtuser에 대해 VM에 설치되었습니다.
2. 개인 키를 사용하여 virtuser에 로그인하십시오. 최상의 결과를 위해서는 개인 키 인증 메소드를 사용하십시오.
3. 개인 키의 컨텐츠를 파일에 복사하십시오.
4. 명령을 실행하십시오. 

  <pre>
    $ ssh virtuser@169.53.246.xxx -i /path/privateKeyFileName
  </pre>
  {: codeblock}

5. 다음 명령을 사용하여 virtuser를 root로 전환해서 전체 sysadmin 권한을 얻으십시오. 

  <pre>
    $ sudo su root
  </pre>
  {: codeblock}

6. 개인용 ssh 키로 시스템에 액세스할 때 문제가 발생하는 경우, 제공되는 루트 비밀번호를 사용하십시오. 이어지는 명령을 실행하고 비밀번호를 제공하여 루트로 로그인하십시오.

 <pre>
    $ ssh root@169.53.246.x
  </pre>
  {: codeblock}

7. 시스템에 액세스하는 데 사용하는 키가 개인용 ssh 키인지 루트 비밀번호인지 상관없이 즉시 루트 비밀번호로 변경하십시오. 
8. SSH 명령을 단순화하려면 %HOME%/.ssh 디렉토리에 "config"라는 이름의 파일을 작성하십시오. 예: 

  <pre>
   Host VM1
      Hostname 169.53.246.xxx
      User virtuser
      IdentityFile /path/privateKeyFileName
  </pre>
  {: codeblock}

9. virtuser로 연결하려면 "ssh VM1"을 실행하십시오.

## 시스템 경로
{: #system_paths}

* Liberty Profile 명령은 */opt/IBM/WebSphere/Liberty/bin*에서 실행할 수 있습니다. 
* Liberty Profile 서버 프로파일 위치는 */opt/IBM/WebSphere/Profiles/Liberty/servers/server1*입니다.
* Traditional WebSphere Application Server 명령은 */opt/IBM/WebSphere/AppServer/bin*에서 실행할 수 있습니다.
* 서버의 Traditional WebSphere Application Server 프로파일 위치는 */opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1*입니다.

## Admin Center 및 Admin Console 링크 사용
{: #console_links}

Admin Center 또는 Admin Console에 대한 링크를 클릭하면 *신뢰할 수 없는 연결* 경고가 표시될 수 있습니다. 정확한 메시지 텍스트는 브라우저마다 다르므로 정확한 단계에 따라 경고를 무시하거나 제거하십시오.

{{site.data.keyword.IBM}}에서 제공되는 링크를 사용하고 있으므로 경고를 무시하고 안전하게 연결할 수 있습니다. 브라우저에서 보안 예외를 저장하도록 제안하는 경우 이 방법이 추후 경고를 방지하는 가장 쉬운 방법입니다. 

또 다른 옵션으로는 수신되는 서명자 인증서를 내보낸 다음 신뢰할 수 있는 루트 인증서로 브라우저에 가져오는 것입니다. 이 옵션을 사용하려면 인증서 발급자의 공통 이름에 VM의 IP 주소를 맵핑하는 *호스트* 파일에 항목을 작성해야 합니다. 이 이름은 wl<pureapplication.ibmcloud.com 형식으로 되어 있습니다. 이제 URL에서 IP 주소 대신에 호스트 이름을 사용하는 경우, 문제없이 연결할 수 있습니다. 그리고 나서 URL에 IP 주소 대신에 해당 호스트 이름을 사용하여 Admin Center 또는 Admin Console에 액세스해야 합니다. 

마지막으로 고객은 외부에서 작성한 애플리케이션의 고유 루트 인증서를 설치해야 하는 경우도 있습니다. 자세한 정보는 [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} 또는 [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} Knowledge Center를 참조하십시오.

## 방화벽 포트
{: #firewall_ports}

애플리케이션과 데이터베이스에 액세스 가능하도록 방화벽에서 포트를 열어야 할 수도 있습니다. 
  * 각 WebSphere Application Server in Bluemix 노드에서 WAS_HOME/virtual/bin 디렉토리의 openFirewallPorts.sh 스크립트를 찾습니다. 
  * 각 Liberty Collective 호스트에서 WAS_HOME/virtual/bin 디렉토리의 openFirewallPorts.sh 스크립트를 찾습니다. 

사용법:
  ```
      $ openFirewallPorts.sh -ports <PORT>:<PROTOCOL>,... -persist true|false
  ```
  {: codeblock}

* PORT는 포트 번호입니다.
* PROTOCOL은 TCP 또는 UDP입니다.
* -persist는 true 또는 false입니다.

여러 포트를 지정하려면 포트를 쉼표(",")로 구분하십시오. 

**참고**: 열려 있는 포트의 sport 및 dport가 방화벽의 INPUT 및 OUTPUT 섹션에서 열립니다. sudo를 사용하여 루트로 이 스크립트를 실행해야 합니다. 직접 iptables를 수정할 수도 있습니다.

## 웹 서버 구성
{: #configure_webserver}

셀 또는 통합(collective)을 프로비저닝하면 사전 구성된 환경을 받습니다. 특히 Traditional Network Deployment 셀의 경우 다음과 같은 환경을 받습니다. 

* 개발 및 테스트 목적으로 IBM HTTP Server와 함께 배치된 배치 관리자. 

* 배치 관리자에 연합된 사용자 정의 노드.

* STARTED 상태로 모두 초기에 프로비저닝되는 배치 관리자, IHS Server 및 노드 에이전트.

모든 사용자 요청을 처리하기 위해 웹 서버가 필요한 경우에는 애플리케이션을 배치한 후에 플러그인을 생성해서 전파해야 할 수 있습니다. 

**문제점 예방:** 플러그인을 생성해서 전파하기 전에 다음 전제조건 태스크가 완료되었는지 확인하십시오. 

* 로컬 Windows, Linux 또는 MAC 환경에 [openVPN](systemAccess.html#setup_openvpn)이 구성, 시작되었으며 사용자가 적합한 지역에 연결되었는지 확인하십시오.

* WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 서비스 대시보드에서 **관리자 콘솔 열기**를 클릭하고 wsadmin 및 서비스 대시보드에 제공된 관리자 비밀번호로 로그인하십시오. 

* Admin Console에서 배치 관리자가 비어 있는 사용자 정의 노드와 연합되어 있으므로 애플리케이션 서버(예: ***server1***)를 작성하십시오. 

* 작성한 서버를 시작하십시오. 

* 애플리케이션 설치 중에 사용자의 애플리케이션 모듈이 방금 시작한 서버와 웹 서버(예: ***webserver1***)에 맵핑되었는지 확인하십시오.

다음 상위 레벨 단계는 전제조건 태스크가 완료되었다고 가정합니다. 

1. Admin Console에서 다음과 같이 환경 옵션에서 플러그인을 생성하십시오. 
   1. 환경 > 글로벌 웹 서버 플러그인 구성 업데이트를 선택하십시오. 
   2. **확인** 또는 **새 플러그인 구성 파일 생성하도록 겹쳐쓰기**를 클릭하십시오.
2. 배치 관리자에서 플러그인을 웹 서버 구성에 복사하십시오. 

  ```
   cp /opt/IBM/WebSphere/Profiles/DefaultDmgr01/config/cells/plugin-cfg.xml /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
  ```
  {: codeblock}
3. **IHS_HOME/conf**(예: */opt/IBM/WebSphere/HTTPServer/conf*)에서 **httpd.conf**를 편집하고 다음 두 개의 행이 존재하는지 확인하십시오. 

    ```
    LoadModule was_ap22_module /opt/IBM/WebSphere/Plugins/bin/64bits/mod_was_ap22_http.so
    WebSpherePluginConfig /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
    ```
    {: codeblock}  
4. 다음 두 개의 명령으로 포트를 여십시오.

  ```
   export serverPorts=2810:TCP,2810:UDP,8880:TCP,8880:UDP,9101:TCP,9101:UDP,9061:TCP,9061:UDP,9080:TCP,9080:UDP,9354:TCP,9354:UDP,9044:TCP,9044:UDP,9443:TCP,9443:UDP,5060:TCP,5060:UDP,5061:TCP,5061:UDP,11005:TCP,11005:UDP,11007:TCP,11007:UDP,9633:TCP,9633:UDP,7276:TCP,7276:UDP,7286:TCP,7286:UDP,5558:TCP,5558:UDP,5578:TCP,5578:UDP

   sudo /opt/IBM/WebSphere/AppServer/virtual/bin/openFirewallPorts.sh -ports $serverPorts -persist true
  ```
    {: codeblock}
5. 다음 두 개의 명령으로 웹 서버를 중지하고 시작하십시오. 
    ```
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k stop
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k start
    ```
    {: codeblock}
8. 플러그인을 통해 애플리케이션에 액세스하십시오. 
  ```
   http://169.53.246.xxx/contextRoot/
  ```
  {: codeblock}

**참고:** 제공된 단계는 웹 서버를 구성하려고 할 때 많은 경로 중 하나를 표시합니다. 추가적인 지원이 필요하면 [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/search/configure%20web%20server?scope=SSAW57_9.0.0){: new_window}를 참조하십시오.

**참고:** 애플리케이션에 액세스할 수 없는 경우, 방화벽에 포트 액세스 문제가 있을 수 있습니다. 따라서 애플리케이션 서버, 노드 에이전트, 웹 서버 및 배치 관리자 중에서 다시 시작해야 할 수 있습니다. 또한 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 서비스 대시보드에 액세스하여 각각의 가상 머신을 다시 시작해야 할 수 있습니다. 

## SSL 구성
{: #ssl_configuration}

Traditional WebSphere Application Server 및 Liberty 프로파일은 [SSL_TLSv2](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.security.component.80.doc/security-component/jsse2Docs/protocols.html){: new_window} 프로토콜로 구성되어 있습니다. 프로토콜을 변경하려면 다음 파일을 수정하십시오. 

Traditional WebSphere Application Server의 경우:

1. /opt/IBM/WebSphere/Profiles/*profile_name*/config/cell/*cell_name*의 **security.xml**을 편집하고 다음 행을 수정하십시오. 

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}

2. /opt/IBM/WebSphere/Profiles/*profile_name*/properties의 **ssl.client.props**를 편집하고 다음 행을 수정하십시오. 

  ```
  com.ibm.ssl.protocol=SSL_TLSv2
  ```
{: codeblock}

Liberty 프로파일의 경우: 

1.   /opt/IBM/WebSphere/Profiles/Liberty/servers/server1의 **server.xml**을 편집하고 defaultSSLConfig ssl 구성 요소에 있는 다음 행을 수정하십시오. 

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}
