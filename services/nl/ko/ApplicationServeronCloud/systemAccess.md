---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#시스템 액세스
{: #system_access}
이 주제에는 시스템에 액세스하고 액세스를 설정하는 다양한 방법과 함께 서비스 인스턴스 작성 및 관리 방법이 포함되어 있습니다.
{: shortdesc}

*마지막 업데이트 날짜: 2016년 6월 08일*
{: .last-updated}

## WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}에서 REST API 사용
{: #restapi_usage}

WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}의 인스턴스가 다음 방법 중 하나로 작성, 프로비저닝, 관리 및 삭제됩니다. 

* {{site.data.keyword.Bluemix_notm}} UI의 {{site.data.keyword.Bluemix_notm}} 카탈로그 및 서비스 대시보드에서.
* RESTful API를 사용하는 애플리케이션 또는 스크립트의 작성에서.

Swagger 2.0 호환 REST API를 사용하여 클라이언트는 포털과 대시보드를 통해 제공된 것과 동일한 기능에 액세스합니다.지원되는 REST API 및 자원에 대한 추가 정보는 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} [REST API 문서](https://new-console.{DomainName}/apidocs/212){: new_window}를 참조하십시오. 

**참고:** 서비스 인스턴스를 작성한 후 작성된 Tee-Shirt 크기에 따라 서비스를 즉각 사용하지 못할 수도 있습니다.서비스 인스턴스의 현재 상태를 판별하도록 리턴된 JSON의 **상태** 필드를 조회할 것을 권장합니다.

**참고:** 기본적으로 API 기본 URL은 [미 남부 지역](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api/v1){: new_window}의 엔드포인트를 가리킵니다. 영국 또는 시드니 지역을 사용 중인 경우 사용자의 애플리케이션이 다음 엔드포인트 중 하나를 사용하는지 확인하십시오.

* [영국 지역](https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api/v1){: new_window}
* [시드니 지역](https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api/v1){: new_window}


## 서비스 대시보드
{: #service_dashboard}

서비스 인스턴스를 작성하고 나면 서비스 대시보드로 이동됩니다. 조직 대시보드의 서비스 아이콘을 클릭하여 언제든 서비스 대시보드로 되돌아갈 수 있습니다.
서비스 대시보드에서 다음에 액세스할 수 있습니다.

*  이 문서의 링크
*  필요한 OpenVPN 구성 파일을 다운로드하기 위한 링크
*  가상 머신을 시작하고 중지하는 기능. 처음에 VM이 시작됩니다. 
*  호스트 이름.
*  관리 사용자 및 관리자 비밀번호. 
*  개인용 SSH 키. 
*  WebSphere® 관리 사용자 및 관리자 비밀번호.
*  Admin Center 및 Admin Console URLS.

**참고**: 특정 양의 컴퓨트, 메모리 및 입출력 자원으로 인해, 클라이언트가 5% 감소 비율로 중지된 상태의 누적 VM에 대해 청구됩니다. 클라이언트는 10개 이하의 IP 주소 또는 64GB 이하 메모리를 사용하는 고정된 수의 중지된 인스턴스에 관리됩니다. 


## WebSphere Application Server for Bluemix 인스턴스의 openVPN 설정
{: #setup_openvpn}

OpenVPN은 Bluemix 가상 머신의 WebSphere Application Server에 액세스하는 데 필요합니다. OpenVPN이 설치되어 있어야 하며 관리자 권한으로 실행 중이어야 합니다.  

### 다음 지시사항을 사용하여 Windows에서 openVPN을 설정하십시오. 

1. [openVPN Windows 다운로드](http://swupdate.openvpn.org/community/releases/) 링크에서 다운로드하십시오.
  * 64비트의 경우, [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window} 또는
  * 32비트의 경우, [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window}
2. 반드시 [Windows 관리자로 실행](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}하고 openVPN을 설치하십시오.
3. 서비스 대시보드에 있는 WebSphere Application Server for Bluemix 인스턴스의 OpenVPN 다운로드 링크에서 VPN 구성 파일을 다운로드하십시오. 압축 파일의 네 개 파일을 모두 **{OpenVPN home}\config** 디렉토리에 추출하십시오. 예: 

  <pre>  
    C:\Program Files\OpenVPN\Config
  </pre>
  {: codeblock}

4. openVPN 클라이언트 프로그램 "OpenVPN GUI"를 시작하십시오. 반드시 [Windows 관리자로 실행](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}을 선택해서 프로그램을 시작하십시오. 그렇지 않으면 연결하지 못할 수 있습니다.

### 다음 지시사항을 사용하여 Linux에서 openVPN을 설정하십시오. 
1. openVPN을 설치하려면 이 [지시사항](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}을 따르십시오.
  * RPM Package Manager를 수동으로 다운로드하고 설치해야 하는 경우 [openVPN Unix/Linux 다운로드](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}로 이동하십시오. Linux 관리자의 도움이 필요할 수 있습니다.
3. 서비스 대시보드에 있는 WebSphere Application Server for Bluemix 인스턴스의 OpenVPN 다운로드 링크에서 VPN 구성 파일을 다운로드하십시오. openVPN 클라이언트를 시작하려는 디렉토리에 파일의 압축을 푸십시오. 네 파일이 모두 같은 디렉토리에 있어야 합니다.
3. openVPN 클라이언트 프로그램을 시작하십시오. 터미널 창을 열고 구성 파일이 포함된 디렉토리로 이동하십시오. 루트로 다음 명령을 실행하십시오. 

  <pre>
      $ openvpn --config vt-wasaas-wasaas.ovpn
  </pre>
  {: codeblock}  

### 다음 지시사항을 사용하여 Mac에서 openVPN을 설정하십시오. 
1. 오픈 소스 소프트웨어 제품인 [Tunnelblick](https://tunnelblick.net/){: new_window}를 설치하는 것이 한 방법입니다. 
2. WebSphere 서비스에서 VPN 구성 파일의 압축을 푸십시오. Tunnelblick에서 Mac의 관리자 비밀번호를 입력하도록 프롬프트를 표시하고 연결하는 데 사용할 수 있는 VPN 세트에 구성을 추가합니다.
3. VPN 네트워크에 연결하고 나서 가상 머신에 액세스할 수 있습니다. 사용자가 처음 액세스한 후에 Tunnelblick에서 구성을 캐시하면 [Tunnelblick](https://tunnelblick.net/){: new_window}에서 연결할 수 있습니다. 쉽게 액세스하려면 맨 위 메뉴 표시줄에 아이콘을 둘 수 있습니다.


## SSH를 사용하여 WebSphere Application Server for Bluemix VM에 액세스
{: #using_ssh}

이러한 지시사항에서는 OpenSSH를 클라이언트로 사용한다고 가정합니다. OpenSSH는 일반적으로 Linux 또는 Windows에서 실행 중인 Cygwin에서 사용할 수 있습니다. Windows 명령 프롬프트에서 실행하도록 설치할 수도 있습니다.

OpenSSH의 설치를 확인하려면 다음 명령을 입력하십시오.
  ```
      $ ssh -V
  ```
  {: codeblock}

사용자의 응답은 다음과 같아야 합니다.
  ```
      OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

다음 지시사항을 사용하여 WebSphere Application Server for Bluemix VM에 대한 SSH 액세스를 설정하십시오. 

1. 사용자가 처음 연결할 때 표시되는 경고 메시지, "호스트 x.x.x.x의 인증을 확립할 수 없습니다."를 검토하십시오. 이 메시지가 표시되는 것은 정상입니다. 롬프트가 표시되면 예를 선택하십시오. 공개 키가 이제 사용자 virtuser에 대해 VM에 설치되었습니다.
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

{{site.data.keyword.IBM}}에서 제공되는 링크를 사용하고 있으므로 경고를 무시하고 연결할 수 있습니다. 브라우저에서 보안 예외를 저장하도록 제안하는 경우 이 방법이 추후 경고를 방지하는 가장 쉬운 방법입니다. 

또 다른 옵션으로는 수신되는 서명자 인증서를 내보낸 다음 신뢰할 수 있는 루트 인증서로 브라우저에 가져오는 것입니다. 이 옵션을 사용하려면 인증서 발급자의 공통 이름에 VM의 IP 주소를 맵핑하는 *호스트* 파일에 항목을 작성해야 합니다. 이 이름은 wl<pureapplication.ibmcloud.com 형식으로 되어 있습니다. 이제 URL에서 IP 주소가 아니라 호스트 이름을 사용하면 문제없이 연결되어야 합니다. 그런 다음에는 URL에 IP 주소가 아니라 해당 호스트 이름을 사용하여 Admin Center 또는 Admin Console에 액세스해야 합니다. 

마지막으로 고객은 외부에서 작성한 애플리케이션의 고유 루트 인증서를 설치해야 하는 경우도 있습니다. 자세한 정보는 [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} 또는 [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} Knowledge Center를 참조하십시오.

## 방화벽 포트
{: #firewall_ports}

애플리케이션과 데이터베이스에 액세스 가능하도록 방화벽에서 포트를 열어야 할 수도 있습니다. 
  * 각 WebSphere Application Server for Bluemix 노드에서 WAS_HOME/virtual/bin 디렉토리에 openFirewallPorts.sh 스크립트가 있습니다. 
  * 각 Liberty Collective 호스트에서 WAS_HOME/virtual/bin 디렉토리에 openFirewallPorts.sh 스크립트가 있습니다.

사용법:
  ```
      $ openFirewallPorts.sh -ports <PORT>:<PROTOCOL>,... -persist true|false
  ```
  {: codeblock}

* PORT는 포트 번호입니다.
* PROTOCOL은 TCP 또는 UDP입니다.
* -persist는 true 또는 false입니다.

여러 포트를 지정하려면 포트를 쉼표(",")로 구분하십시오. 

**참고**: 열려 있는 포트의 sport 및 dport가 모두 방화벽의 INPUT 및 OUTPUT 섹션에서 열립니다. sudo를 사용하여 루트로 이 스크립트를 실행해야 합니다. 직접 iptables를 수정할 수도 있습니다.
