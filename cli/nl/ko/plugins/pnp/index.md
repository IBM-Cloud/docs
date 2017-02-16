---

copyright:

  years: 2016, 2017

lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Bluemix CLI의 사설 네트워크 피어 플러그인
{: #private_network_cli}

사설 네트워크 피어 명령행 인터페이스(CLI)를 사용하여 두 {{site.data.keyword.Bluemix}} 영역 간의 사설 네트워크 피어를 구성하고 관리하십시오. 사설 네트워크 피어는 IBM Containers(Docker 컨테이너)에서 지원됩니다. Bluemix 영역은 동일한 지역의 서로 다른 가용성 구역에 위치할 수 있거나 다른 지역에 위치할 수 있습니다. 사설 네트워크 피어 CLI 플러그인은 Bluemix CLI 플러그인으로 사용할 수 있습니다. 

사설 네트워크 피어 CLI 플러그인은 Windows, MAC 및 Linux 운영 체제에 사용 가능합니다. 사용자에게 적용 가능한 플러그인을 사용해야 합니다.

시작하기 전에 Bluemix 영역을 작성해야 합니다. 영역의 각 컨테이너에 다른 네트워크에서의 IP 주소가 있는지 확인하십시오. 세부사항은 [사용자 소유의 사설 IP 주소 사용](https://www.{DomainName}/docs/containers/container_security_network.html#container_cli_ips_byoip)을 참조하십시오.

**참고:** Bluemix 영역으로 사설 네트워크 피어를 사용한 후 영역을 삭제해야 하는 경우, 먼저 해당 영역에서 사설 네트워크 피어 연결을 삭제하십시오. 

시작하려면 IBM Bluemix CLI를 설치하십시오. 세부사항은
[Bluemix CLI](http://clis.ng.bluemix.net/ui/home.html)를 참조하십시오.

## 사설 네트워크 피어 CLI 플러그인 설치

**참고**: 이전 버전의 플러그인이 설치되어 있는 경우 이를 삭제해야 합니다. 다음 명령을 사용하여 플러그인을 설치 제거하십시오.

```
bluemix plugin uninstall private-network-peering
```
### 로컬로 설치
[IBM Bluemix CLI 플러그인 저장소](http://plugins.ng.bluemix.net/ui/repository.html#bluemix-plugins)에서 사용자의 플랫폼에 해당하는 사설 네트워크 피어 플러그인을 다운로드하십시오.

다음 명령을 사용하여 사설 네트워크 피어 플러그인을 설치하십시오.

**참고**: 플러그인의 위치로 전환하거나 플러그인 위치에 대한 경로를 지정하십시오.

* Microsoft Windows OS의 경우:

```
bluemix plugin install private-network-peering-windows-amd64.exe
```

* Apple MAC OS의 경우:

```
bluemix plugin install private-network-peering-darwin-amd64
```

* Linux OS의 경우:

```
bluemix plugin install private-network-peering-linux-amd64
```

**참고**: Linux OS용 플러그인을 설치하는 동안 권한이 거부됨을 나타내는 오류 메시지가 표시되는 경우 다음 명령을 실행하여 권한을 변경하십시오.

```
chmod a+x ./private-network-peering-linux-amd64
```

### Bluemix 저장소 설치

Bluemix 저장소에서 플러그인을 설치하려면 다음 단계를 따르십시오.

1. Bluemix 플러그인 저장소 엔드포인트를 추가하십시오.
	```
	bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
	```

2. 다음 명령을 실행하십시오.

	```
	bluemix plugin install private-network-peering -r bluemix-bx
	```

## 사설 네트워크 피어 명령의 목록
다음 명령이 지원됩니다. 사용 가능한 명령의 목록을 나열하려면 `bluemix network` 명령을 사용하십시오.

| 명령     | 설명                                    |
|-------------|------------------------------------------------|
| pnp-routers | 피어에 대해 사용 가능한 모든 라우터를 나열합니다.        |
| pnp-create  | 사설 네트워크 피어 연결을 작성합니다.   |
| pnp-delete  | 사설 네트워크 피어 연결을 삭제합니다.   |
| pnp-show    | 모든 사설 네트워크 피어 연결을 나열합니다.  |
{: caption="표 1. 사설 네트워크 피어 명령" caption-side="top"}


### 명령 사용
명령에 대한 도움말 정보를 보려면 `bluemix network [command] -h`를 실행하십시오.

#### 피어에 대해 사용 가능한 모든 라우터 나열
```
bluemix network pnp-routers [--verbose (or -v)]
```

#####선택적 매개변수
{: #op1}

* **--verbose (or -v)**(플래그): 각 라우터에 대한 자세한 네트워크 정보를 표시합니다.

######명령 예제
{: #ex1}

모든 라우터에 대한 네트워크 정보 표시:

	$ bluemix network pnp-routers
	Listing available routers ...
	OK

	IP              NAME            COMPUTE    REGION          ORGANIZATION    SPACE
	129.41.234.246  default-router  Container  US-South        ywu@us.ibm.com  demo1
	129.41.237.172  default-router  Container  US-South        ywu@us.ibm.com  demo2
	129.41.238.212  default-router  Container  United-Kingdom  ywu@us.ibm.com  demo3


모든 라우터에 대한 자세한 네트워크 정보 표시:


	$ bluemix network pnp-routers -v
	Listing available routers ...
	OK

	Router 'bce1aa25-bad0-4cf1-a831-d53c16463d06':
	FIELD          VALUE
	IP             129.41.234.246
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo1
	Networks       172.31.0.0/16

	Router '9ea160f2-1a30-44cd-bd25-794d441b274b':
	FIELD          VALUE
	IP             129.41.237.172
	Name           default-router
	Compute        Container
	Region         US-South
	Organization   ywu@us.ibm.com
	Space          demo2
	Networks       172.25.0.0/16

	...


#### IP 주소를 사용하여 사설 네트워크 피어 연결 작성
```
bluemix network pnp-create <router_ip> <router_ip> <name>
```

#####매개변수
{: #p1}

* **router_ip**: 연결하려는 두 개의 라우터의 IP 주소. `bluemix network pnp-routers` 명령을 사용하여 IP 주소를 찾을 수 있습니다.
* **name**: 사설 네트워크 피어 연결의 이름

######명령 예제
{: #ex2}

	$ bluemix network pnp-create 129.41.234.246 129.41.237.172 demo
	Creating private network peering connection 'demo' ...
	Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
	OK

	Private network peering connection 'demo' created.


####연결 이름을 사용하여 사설 네트워크 피어 연결 작성

```
bluemix network pnp-create -i <name>
```

#####매개변수
{: #p2}

* **--interactive (-i)**(플래그): 라우터를 선택할 대화식 모드
* **name**: 사설 네트워크 피어 연결의 이름

######명령 예제
{: #ex3}

	$ bluemix network pnp-create -i demo
	Creating private network peering connection 'demo' ...
	List of available routers (select TWO for peering):

	#  ROUTER                          COMPUTE    REGION          ORGANIZATION    SPACE
	1  default-router(129.41.234.246)  Container  US-South        ywu@us.ibm.com  demo1
	2  default-router(129.41.237.172)  Container  US-South        ywu@us.ibm.com  demo2
	3  default-router(129.41.238.212)  Container  United-Kingdom  ywu@us.ibm.com  demo3

	Select first router for peering> 1
	Select second router for peering> 2

	Connecting 'default-router(129.41.234.246)' and 'default-router(129.41.237.172)' ...
	OK

	Private network peering connection 'demo' created.


#### 모든 사설 네트워크 피어 연결 나열
```
bluemix network pnp-show [--verbose (or -v)]
```

#####선택적 매개변수
{: #op2}

* **--verbose (or -v)**(플래그): 각 라우터에 대한 자세한 네트워크 정보를 표시합니다.

######명령 예제
{: #ex4}

기본 정보 표시:

	$ bluemix network pnp-show
	Listing private network peering connections ...
	OK

	ID                                    NAME  STATUS  ROUTER1                         ROUTER2
	17b1c3c7-d614-4fc5-9afe-961e38ee79f8  demo  Active  default-router(129.41.234.246)  default-router(129.41.237.172)

자세한 정보 표시:

	$ bluemix network pnp-show -v
	Listing private network peering connections ...
	OK

	Connection 'bedbc077-8040-41cc-a4aa-d9ce09a2e8ec':
	FIELD              VALUE
	Name               demo
	Status             Active
	Router1 Name       default-router
	Router1 IP         129.41.234.246
	Router1 Networks   172.31.0.0/16
	Router2 Name       default-router
	Router2 IP         129.41.237.172
	Router2 Networks   172.25.0.0/16


#### 사설 네트워크 피어 연결 삭제
```
bluemix network pnp-delete [--force (or -f)] <connection_id>
```
#####매개변수
{: #p3}
* **connection_id**: 한 개 이상의 연결 ID가 쉼표로 구분됩니다.

#####선택적 매개변수
{: #op3}

* **--force (or -f)**(플래그): 확인 프롬프트 없이 연결을 삭제합니다.

######명령 예제:
{: #ex5}

연결 삭제:

	$ bluemix network pnp-delete 17b1c3c7-d614-4fc5-9afe-961e38ee79f8
	Warning: deleted connections cannot be restored.
	Are you sure you want to delete the connection? (yes/no)> yes

	Deleting private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' ...
	OK

	Private network peering connection '17b1c3c7-d614-4fc5-9afe-961e38ee79f8' deleted.


다중 연결 삭제:

```
bluemix network pnp-delete [-f] <connection_id>,<connection_id>,<connection_id>
```
