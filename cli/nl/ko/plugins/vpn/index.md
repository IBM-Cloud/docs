---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# IBM VPN CLI
*마지막 업데이트 날짜: 2016년 3월 3일*

명령행 인터페이스(CLI)를 사용하여 IBM® VPN(Virtual Private Network) 서비스를 구성 및 관리할 수 있습니다. IBM VPN CLI는 Cloud Foundry CLI 플러그인과 함께 사용되는 플러그인입니다. 이 플러그인은 Windows, MAC 및 Linux 운영 체제에서 사용 가능합니다. 적절한 운영 체제를 사용 중인지 확인하십시오.

시작하기 전에 Cloud Foundry CLI를 설치하십시오. 자세한 정보는 [Cloud Foundry 명령행 인터페이스](https://console.{DomainName}/docs/cli/downloads.html)를 참조하십시오. 

##IBM VPN CLI 플러그인 설치
**참고:** IBM VPN CLI 플러그인 이전 버전이 설치되어 있는 경우 먼저 이전 버전을 설치 제거해야 합니다. 다음 명령을 사용하십시오. 

```
cf uninstall-plugin vpn
```  

**로컬로 설치**

1. [IBM Bluemix CLI 플러그인 저장소](http://plugins.ng.bluemix.net)에서 사용 중인 플랫폼용 IBM VPN 플러그인을 다운로드하십시오.
2. 다음 명령을 사용하여 IBM VPN 플러그인을 설치하십시오.
**참고:** VPN 플러그인이 있는 위치로 전환하거나 플러그인 위치의 경로를 지정하십시오.  

	**MS Windows OS:**

	```
	cf install-plugin vpn_windows64.exe
	```  

	**Apple MAC OS:**

	```
	cf install-plugin vpn_mac_os_amd64
	```  

	**Linux OS:**

	```
	cf install-plugin vpn_linuxamd64
	```  


**Bluemix 저장소에서 설치**  

1. Cloud Foundry CLI 저장소에 Bluemix 저장소를 추가하십시오. 다음 명령을 사용하십시오.

	```
	cf add-plugin-repo bluemix http://plugins.ng.bluemix.net
	```  
2. 다음 명령을 실행하십시오.  

	```
	cf install-plugin vpn -r bluemix
	```
##IBM VPN 서비스 명령 목록

### cf vpn-create connection

VPN 연결을 작성합니다.

```
cf vpn-create connection <connection name> -g <gateway name> -k <preshared key> -subnets ["<subnet/mask>"] -cip <customer gateway IP address> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### 매개변수
{: #p1}

**connection name:**
연결 이름입니다.

**gateway name:**
게이트웨이 이름입니다.

**-k:**
사전공유 키입니다.

**subnet/mask:**
CIDR 형식의 원격 서브넷 주소입니다. 

**customer gateway IP address:**
VPN 터널의 원격 엔드포인트 IP 주소입니다. 

##### 선택적 매개변수:
{: #op1}

**-d:** 지정된 매개변수에 대한 설명입니다.

**-peer_id:** 원격 피어의 ID입니다. VPN 터널의 기타 엔드포인트입니다.

**-admin_state:** VPN 연결 상태입니다. 값: UP 또는 DOWN.

**-dpd-action:** 피어가 작동 중지로 발견될 때 수행해야 하는 조치입니다. 값: hold, clear, disabled, restart, restart-by-peer. 기본값: hold

**-gateway_ip:** 로컬 VPN 터널 엔드포인트의 IP 주소입니다. 

**-i:** 개시자의 상태입니다. 기본값: bi-directional.

**-dpd-timeout:** 세션이 종료되는 제한시간 값(초)입니다. 범위: 6 - 86400초. 기본값: 120초. 활성 상태 지속 제한시간 값은 활성 상태 지속 간격 값보다 커야 합니다.

**-dpd-interval:** 활성 상태 지속 간격(초)입니다. 구성된 간격으로 활성 상태 지속 메시지를 보내 피어의 활성 여부를 확인합니다. 범위: 5 - 86399초. 기본값: 15초

**-ike:** IKE 정책의 이름입니다.

**-ipsec:** IPSec 정책의 이름입니다.


### cf vpn-create ike

IKE 정책을 작성합니다.

```
cf vpn-create ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 매개변수
{: #p2}

**policy name:**
IKE 정책의 이름입니다.

**gateway name:**
게이트웨이 이름입니다. 

##### 선택적 매개변수:
{: #op2}

**-d:** 지정된 매개변수에 대한 설명입니다.

**-pfs:** DH(Diffie-Hellman) 그룹 ID입니다. 값: Group2, Group5, Group14. 기본값: Group2 

**-e:** 암호화 알고리즘입니다. 값: aes-128, aes-192, aes-256, 3des. 기본값: aes-128

**-lv:** IKE SA(Security Association)의 수명 값입니다. 범위: 60 - 86400초. 기본값: 86400초


### cf vpn-create ipsec

IPSec 정책을 작성합니다.

```
cf vpn-create ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 매개변수
{: #p3}

**policy name:**
IPSec 정책의 이름입니다. 

**gateway name:**
게이트웨이 이름입니다. 

##### 선택적 매개변수:
{: #op3}

**-d:** 지정된 매개변수에 대한 설명입니다.

**-pfs:** DH(Diffie-Hellman) 그룹 ID입니다. 값: Group2, Group5, Group14. 기본값: Group2  

**-e:** 암호화 알고리즘입니다. 값: aes-128, aes-192, aes-256, 3des. 기본값: aes-128

**-lv:** SA(Security Association)의 수명 값입니다. 범위: 60 - 86400초. 기본값: 3600초

### cf vpn-create gateway

VPN 게이트웨이를 작성합니다.

```
cf vpn-create gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### 매개변수
{: #p4}

**gateway name:**
게이트웨이 이름입니다.

**-t:** 서비스를 사용하려는 컨테이너입니다. 값: allSingleContainers, allContainerGroups, allContainers. 기본값: 기본값은 없으며 유형을 지정해야 합니다. 

#####선택적 매개변수:
{: #op4}

**-gateway_ip:**
게이트웨이의 IP 주소입니다. 

**-subnets:**
CIDR 형식의 서브넷 주소입니다. 

### cf vpn-show gateways

현재 게이트웨이에 대한 정보를 표시합니다.

```
cf vpn-show gateways
```
### cf vpn-show ikes

현재 IKE 연결에 대한 정보를 표시합니다.

```
cf vpn-show ikes
```
### cf vpn-show ipsecs

현재 IPSec 연결에 대한 정보를 표시합니다.

```
cf vpn-show ipsecs
```
### cf vpn-show connections

모든 현재 연결에 대한 정보를 표시합니다.

```
cf vpn-show connections
```
### cf vpn-show ike

IKE 연결에 대한 정보를 표시합니다.

```
cf vpn-show ike <policy name>
```
### cf vpn-show ipsec

IPSec 연결에 대한 정보를 표시합니다.

```
cf vpn-show ipsec <policy name>
```
### cf vpn-show gateway

게이트웨이에 대한 연결 정보를 표시합니다.

```
cf vpn-show gateway <gateway name>
```
### cf vpn-show connection

특정 연결에 대한 정보를 모두 표시합니다.

```
cf vpn-show connection <connection name>
```
### cf vpn-delete

기존 연결, 정책 또는 게이트웨이를 삭제합니다.

```
cf vpn-delete ike <policy name>
```

```
cf vpn-delete ipsec <policy name>
```

```
cf vpn-delete connection <connection name>
```

```
cf vpn-delete gateway <gateway name>
```


### cf vpn-update connection

기존 VPN 연결을 업데이트합니다.

```
cf vpn-update connection <connection name> -g <gateway name> -cip <customer gateway IP address> -subnets ["<subnet/mask>"] -k <preshared key> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### 매개변수
{: #p5}

**connection name:**
연결 이름입니다.


##### 선택적 매개변수:
{: #op5}

**gateway name:**
게이트웨이 이름입니다.

**customer gateway IP address:**
VPN 터널의 원격 엔드포인트 IP 주소입니다. 

**subnet/mask:**
CIDR 형식의 서브넷 주소입니다. 

**-k:**
사전공유 키입니다.

**-d:** 지정된 매개변수에 대한 설명입니다.

**-peer_id:** 원격 피어의 ID입니다. VPN 터널의 기타 엔드포인트입니다.

**-admin_state:** VPN 연결 상태입니다. 값: UP 또는 DOWN.

**-dpd-action:** 피어가 작동 중지로 발견될 때 수행해야 하는 조치입니다. 값: hold, clear, disabled, restart, restart-by-peer. 기본값: hold

**-gateway_ip:** 로컬 VPN 터널 엔드포인트의 IP 주소입니다. 

**-i:** 개시자의 상태입니다. 기본값: bi-directional.

**-dpd-timeout:** 세션이 종료되는 제한시간 값(초)입니다. 범위: 6 - 86400초. 기본값: 120초

**-dpd-interval:** 활성 상태 지속 간격(초)입니다. 구성된 간격으로 활성 상태 지속 메시지를 보내 피어의 활성 여부를 확인합니다. 범위: 5 - 86399초. 기본값: 15초

**-ike:** IKE 정책의 이름입니다.

**-ipsec:** IPSec 정책의 이름입니다.


### cf vpn-update ike

IKE 정책을 업데이트합니다.

```
cf vpn-update ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 매개변수
{: #p6}

**policy name:**
IKE 정책의 이름입니다. 

##### 선택적 매개변수:
{: #op6}

**gateway name:**
게이트웨이 이름입니다. 

**-d:** 지정된 매개변수에 대한 설명입니다.

**-pfs:** DH(Diffie-Hellman) 그룹 ID입니다. 값: Group2, Group5, Group14. 기본값: Group2 

**-e:** 암호화 알고리즘입니다. 값: aes-128, aes-192, aes-256, 3des. 기본값: aes-128

**-lv:** IKE SA(Security Association)의 수명 값입니다. 범위: 60 - 86400초. 기본값: 86400초


### cf vpn-update ipsec

IPSec 정책을 업데이트합니다.

```
cf vpn-update ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### 매개변수
{: #p7}

**policy name:**
IPSec 정책의 이름입니다.


##### 선택적 매개변수:
{: #op7}

**gateway name:**
게이트웨이 이름입니다.

**-d:** 지정된 매개변수에 대한 설명입니다.

**-pfs:** DH(Diffie-Hellman) 그룹 ID입니다. 값: Group2, Group5, Group14. 기본값: Group2 

**-e:** 암호화 알고리즘입니다. 값: aes-128, aes-192, aes-256, 3des. 기본값: aes-128

**-lv:** SA(Security Association)의 수명 값입니다. 범위: 60 - 86400초. 기본값: 3600초

### cf vpn-update gateway

기존 VPN 게이트웨이를 업데이트합니다.

```
cf vpn-update gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### 매개변수
{: #p8}

**gateway name:**
게이트웨이 이름입니다.

#####선택적 매개변수:
{: #op8}

**-t:** 서비스를 사용하려는 컨테이너입니다. 값: allSingleContainers, allContainerGroups, allContainers. 기본값: 기본값은 없으며 유형을 지정해야 합니다.

**-gateway_ip:**
게이트웨이의 IP 주소입니다. 

**-subnets:**
CIDR 형식의 서브넷 주소입니다. 

# 재링크
## 일반  
{: #general}  
* [IBM VPN 서비스](../../../services/vpn/index.html)
* [Cloud Foundry CLI](https://console.{DomainName}/docs/cli/downloads.html){: new_window}
