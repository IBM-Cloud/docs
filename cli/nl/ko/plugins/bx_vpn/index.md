---



copyright:

  years: 2015，2017

lastupdated: "2016-06-20"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} CLI의 VPN 플러그인

*버전:* 1.4.0

명령행 인터페이스(CLI)를 사용하여 {{site.data.keyword.vpn_full}} 서비스를 구성하고 관리할 수 있습니다. VPN CLI 플러그인은 두 버전(Cloud Foundry CLI 플러그인에 사용할 버전과 {{site.data.keyword.Bluemix}} CLI 플러그인에 사용할 버전)으로 사용 가능합니다. 두 플러그인 버전 모두 동일한 기능을 제공합니다.
{:shortdesc}

VPN 플러그인은 Windows, MAC 및 Linux 운영 체제에 사용 가능합니다. 사용자에게 적용 가능한 항목을 사용해야 합니다.

뒤따르는 지시사항은 {{site.data.keyword.Bluemix_notm}} CLI 플러그인 작업에 대한 것입니다. Cloud Foundry(cf) CLI 플러그인으로 플러그인을 사용하려면 [cf CLI의 VPN CLI 플러그인](../vpn/index.html)을 참조하십시오.


다음 정보는 Bluemix CLI의 VPN 플러그인에서 지원하는 모든 명령을 나열하며 해당 이름, 옵션, 사용, 전제조건, 설명 및 예제를 포함합니다. vpn 플러그인을 설치하는 방법에 대해 [Bluemix 명령행 인터페이스 확장](../../index.html#cli_bluemix_ext)을 참조하십시오.

**참고:** *전제조건*에는 명령을 사용하기 전에 필요한 조치가 설명되어 있습니다. 전제조건에는 다음 조치 중 하나 이상이 포함될 수 있습니다.
<dl>
<dt>**엔드포인트**</dt>
<dd>명령을 사용하기 전에 `bluemix api`를 통해 API 엔드포인트를 설정해야 합니다.</dd>
<dt>**로그인**</dt>
<dd>이 명령을 사용하기 전에 `bluemix login` 명령을 사용하여 로그인해야 합니다.</dd>
<dt>**대상**</dt>
<dd>이 명령을 사용하기 전에 `bluemix target` 명령을 사용하여 조직과 영역을 설정해야 합니다.</dd>
</dl>


## bluemix vpn connection-create
VPN 연결을 작성합니다.

```
bluemix vpn connection-create CONNECTION_NAME -g GATEWAY_NAME -k PRESHARED_KEY -subnets "SUBNET/MASK" -cip CUSTOMER_GATEWAY_IP_ADDRESS [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*CONNECTION_NAME*  (필수): 연결의 이름입니다.

-g *GATEWAY_NAME*  (필수): 게이트웨이의 이름입니다.

-k *PRESHARED_KEY*  (필수): 사전 공유 키입니다.

-subnets "*SUBNET*/*MASK*"  (필수): CIDR 형식의 원격 서브넷 주소입니다.

-cip *CUSTOMER_GATEWAY_IP_ADDRESS*  (필수): VPN 터널의 원격 엔드포인트 IP 주소입니다.

-d *DESCRIPTION*  (선택사항): 지정된 매개변수에 대한 설명입니다.

-peer_id *PEER_ID*  (선택사항): 원격 피어의 ID입니다. VPN 터널의 다른 엔드포인트입니다.

-admin_state *ADMIN_STATE*  (선택사항): VPN 연결의 상태입니다. 올바른 값은 `UP` 또는 `DOWN`입니다.

-dpd-action *ACTION*  (선택사항): 피어가 작동하지 않는 것으로 발견될 때 수행할 조치입니다. 올바른 값은 `hold`, `clear`, `disabled`, `restart` 또는 `restart-by-peer`입니다. 기본값은 `hold`입니다.

-gateway_ip *IP_ADDRESS*  (선택사항): 로컬 VPN 터널 엔드포인트의 IP 주소입니다.

-i *INITIATOR_STATE*  (선택사항): 개시자의 상태입니다. 기본값은 `bi-directional`입니다.

-dpd-timeout *VALUE*  (선택사항): 세션이 종료되는 제한시간 값(초)입니다. 범위: 6 - 86400초. 기본값은 `120`초입니다.

-dpd-interval *VALUE*  (선택사항): 킵얼라이브 간격(초)입니다. 구성된 간격으로 킵얼라이브 메시지를 전송하여 피어가 작동 중인지 확인하십시오. 범위: 5-86399초. 기본값은 `15`초입니다.

-ike *NAME*  (선택사항): IKE 정책의 이름입니다.

-ipsec *NAME*  (선택사항): IPSec 정책의 이름입니다.

**예제**:

이름이 `my_connection`인 새 vpn 연결을 작성합니다. 
```
bluemix vpn connection-create my_connection -g my_gateway -k 123456 -subnets "192.168.10.0/24" -cip 162.135.1.1
```


## bluemix vpn ike-create
IKE 정책을 작성합니다. 

```
bluemix vpn ike-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*POLICY_NAME*  (필수): IKE 정책의 이름입니다.

-g *GATEWAY_NAME*  (필수): 게이트웨이의 이름입니다.

-d *DESCRIPTION*  (선택사항): 지정된 매개변수에 대한 설명입니다.

-pfs *GROUP*  (선택사항): DH(Diffie-Hellman) 그룹 ID입니다. 올바른 값은 `Group2`, `Group5` 또는 `Group14`입니다. 기본값은 `Group2`입니다.

-e *ENCRYPTION_ALGORITHM*  (선택사항): 암호화 알고리즘입니다. 올바른 값은 `aes-128`, `aes-192`, `aes-256` 또는 `3des`입니다. 기본값은 `aes-128`입니다.

-lv *LIFETIME_VALUE*  (선택사항): IKE 보안 연관의 유효 기간 값입니다. 범위: 60 - 86400초. 기본값은 `86400`초입니다.

**예제**:

이름이 `my_ike`인 새 IKE 정책을 작성합니다. 
```
bluemix vpn ike-create my_ike -g my_gateway
```


## bluemix vpn ipsec-create
IPSec 정책을 작성합니다. 

```
bluemix vpn ipsec-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*POLICY_NAME*  (필수): IPSec 정책의 이름입니다.

-g *GATEWAY_NAME*  (필수): 게이트웨이의 이름입니다.

-d *DESCRIPTION*  (선택사항): 지정된 매개변수에 대한 설명입니다.

-pfs *GROUP*  (선택사항): DH(Diffie-Hellman) 그룹 ID입니다. 올바른 값은 `Group2`, `Group5` 또는 `Group14`입니다. 기본값은 `Group2`입니다.

-e *ENCRYPTION_ALGORITHM*  (선택사항): 암호화 알고리즘입니다. 올바른 값은 `aes-128`, `aes-192`, `aes-256` 또는 `3des`입니다. 기본값은 `aes-128`입니다.

-lv *LIFETIME_VALUE*  (선택사항): 보안 연관의 유효 기간 값입니다. 범위: 60 - 86400초. 기본값은 `3600`초입니다.

**예제**:

이름이 `my_policy`인 IPSec 정책을 작성합니다. 
```
bluemix vpn ipsec-create my_policy -g my_gateway
```


## bluemix vpn gateway-create
VPN 게이트웨이를 작성합니다.

```
bluemix vpn gateway-create GATEWAY_NAME -t TYPE [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*GATEWAY_NAME*  (필수): 게이트웨이의 이름입니다.

-t *TYPE*  (필수): 서비스가 사용되도록 설정할 컨테이너입니다. 올바른 값은 `allSingleContainers`, `allContainerGroups` 또는 `allContainers`입니다. 기본값이 없으므로 유형을 지정해야 합니다.

-gateway_ip *IP_ADDRESS*  (선택사항): 게이트웨이의 IP 주소입니다.

-subnets *SUBNET_ADDRESS*  (선택사항): CIDR 형식의 서브넷 주소입니다.

**예제**:

이름이 `my_gateway`이고 유형이 `allContainerGroups`인 게이트웨이를 작성합니다. 
```
bluemix vpn gateway-create my_gateway -t allContainerGroups
```


## bluemix vpn connections
모든 현재 연결에 대한 정보를 표시합니다.

```
bluemix vpn connections
```

**전제조건**:  엔드포인트, 로그인, 대상 설정


## bluemix vpn ikes
현재 IKE 연결에 대한 정보를 표시합니다.

```
bluemix vpn ikes
```

**전제조건**:  엔드포인트, 로그인, 대상 설정


## bluemix vpn ipsecs
현재 IPSec 연결에 대한 정보를 표시합니다.

```
bluemix vpn ipsecs
```

**전제조건**:  엔드포인트, 로그인, 대상 설정


## bluemix vpn gateways
현재 게이트웨이에 대한 정보를 표시합니다.

```
bluemix vpn gateways
```

**전제조건**:  엔드포인트, 로그인, 대상 설정


## bluemix vpn connection
특정 연결에 대한 모든 정보를 표시합니다.

```
bluemix vpn connection CONNECTION_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*CONNECTION_NAME*  (필수): 표시할 연결의 이름입니다.


## bluemix vpn ike
IKE 연결에 대한 정보를 표시합니다.

```
bluemix vpn ike POLICY_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*POLICY_NAME*  (필수): 표시할 IKE 정책의 이름입니다.


## bluemix vpn ipsec
IPSec 연결에 대한 정보를 표시합니다.

```
bluemix vpn ipsec POLICY_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*POLICY_NAME*  (필수): 표시할 IPSec 정책의 이름입니다.


## bluemix vpn gateway
게이트웨이에 대한 연결 정보를 표시합니다. 

```
bluemix vpn gateway GATEWAY_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*GATEWAY_NAME*  (필수): 표시할 게이트웨이의 이름입니다.


## bluemix vpn connection-delete
기존 연결을 삭제합니다.

```
bluemix vpn connection-delete CONNECTION_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*CONNECTION_NAME*  (필수): 삭제할 연결의 이름입니다.


## bluemix vpn ike-delete
기존 IKE 정책을 삭제합니다.

```
bluemix vpn ike-delete POLICY_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*POLICY_NAME*  (필수): 삭제할 IKE 정책의 이름입니다.


## bluemix vpn ipsec-delete
기존 IPSec 정책을 삭제합니다.

```
bluemix vpn ipsec-delete POLICY_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*POLICY_NAME*  (필수): 삭제할 IPSec 정책의 이름입니다.


## bluemix vpn gateway-delete
기존 게이트웨이를 삭제합니다.

```
bluemix vpn gateway-delete GATEWAY_NAME
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*GATEWAY_NAME*  (필수): 삭제할 게이트웨이의 이름입니다.


## bluemix vpn connection-update
기존 VPN 연결을 업데이트합니다.

```
bluemix vpn connection-update CONNECTION_NAME [-g GATEWAY_NAME] [-k PRESHARED_KEY] [-subnets "SUBNET/MASK"] [-cip CUSTOMER_GATEWAY_IP_ADDRESS] [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*CONNECTION_NAME*  (필수): 연결의 이름입니다.

-g *GATEWAY_NAME*  (선택사항): 게이트웨이의 이름입니다.

-k *PRESHARED_KEY*  (선택사항): 사전 공유 키입니다.

-subnets "*SUBNET*/*MASK*"  (선택사항): CIDR 형식의 서브넷 주소입니다.

-cip *CUSTOMER_GATEWAY_IP_ADDRESS*  (선택사항): VPN 터널의 원격 엔드포인트 IP 주소입니다.

-d *DESCRIPTION*  (선택사항): 지정된 매개변수에 대한 설명입니다.

-peer_id *PEER_ID*  (선택사항): 원격 피어의 ID입니다. VPN 터널의 다른 엔드포인트입니다.

-admin_state *ADMIN_STATE*  (선택사항): VPN 연결의 상태입니다. 올바른 값은 `UP` 또는 `DOWN`입니다.

-dpd-action *ACTION*  (선택사항): 피어가 작동하지 않는 것으로 발견될 때 수행할 조치입니다. 올바른 값은 `hold`, `clear`, `disabled`, `restart` 또는 `restart-by-peer`입니다. 

-gateway_ip *IP_ADDRESS*  (선택사항): 로컬 VPN 터널 엔드포인트의 IP 주소입니다.

-i *INITIATOR_STATE*  (선택사항): 개시자의 상태입니다. 

-dpd-timeout *VALUE*  (선택사항): 세션이 종료되는 제한시간 값(초)입니다. 범위: 6 - 86400초.

-dpd-interval *VALUE*  (선택사항): 킵얼라이브 간격(초)입니다. 구성된 간격으로 킵얼라이브 메시지를 전송하여 피어가 작동 중인지 확인하십시오. 범위: 5-86399초. 

-ike *NAME*  (선택사항): IKE 정책의 이름입니다.

-ipsec *NAME*  (선택사항): IPSec 정책의 이름입니다.


## bluemix vpn ike-update
IKE 정책을 업데이트합니다.

```
bluemix vpn ike-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*POLICY_NAME*  (필수): IKE 정책의 이름입니다.

-g *GATEWAY_NAME*  (선택사항): 게이트웨이의 이름입니다.

-d *DESCRIPTION*  (선택사항): 지정된 매개변수에 대한 설명입니다.

-pfs *GROUP*  (선택사항): DH(Diffie-Hellman) 그룹 ID입니다. 올바른 값은 `Group2`, `Group5` 또는 `Group14`입니다. 

-e *ENCRYPTION_ALGORITHM*  (선택사항): 암호화 알고리즘입니다. 올바른 값은 `aes-128`, `aes-192`, `aes-256` 또는 `3des`입니다. 

-lv *LIFETIME_VALUE*  (선택사항): IKE 보안 연관의 유효 기간 값입니다. 범위: 60 - 86400초.


## bluemix vpn ipsec-update
IPSec 정책을 업데이트합니다.

```
bluemix vpn ipsec-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*POLICY_NAME*  (필수): IPSec 정책의 이름입니다.

-g *GATEWAY_NAME*  (선택사항): 게이트웨이의 이름입니다.

-d *DESCRIPTION*  (선택사항): 지정된 매개변수에 대한 설명입니다.

-pfs *GROUP*  (선택사항): DH(Diffie-Hellman) 그룹 ID입니다. 올바른 값은 `Group2`, `Group5` 또는 `Group14`입니다. 

-e *ENCRYPTION_ALGORITHM*  (선택사항): 암호화 알고리즘입니다. 올바른 값은 `aes-128`, `aes-192`, `aes-256` 또는 `3des`입니다. 

-lv *LIFETIME_VALUE*  (선택사항): 보안 연관의 유효 기간 값입니다. 범위: 60 - 86400초.


## bluemix vpn gateway-update
기존 VPN 게이트웨이를 업데이트합니다.

```
bluemix vpn gateway-update GATEWAY_NAME [-t TYPE] [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**전제조건**:  엔드포인트, 로그인, 대상 설정

**명령 옵션**:

*GATEWAY_NAME*  (필수): 게이트웨이의 이름입니다.

-t *TYPE*  (선택사항): 서비스가 사용되도록 설정할 컨테이너입니다. 올바른 값은 `allSingleContainers`, `allContainerGroups` 또는 `allContainers`입니다. 

-gateway_ip *IP_ADDRESS*  (선택사항): 게이트웨이의 IP 주소입니다.

-subnets *SUBNET_ADDRESS*  (선택사항): CIDR 형식의 서브넷 주소입니다.
