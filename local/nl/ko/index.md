{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} Local
{: #local}
*마지막 업데이트 날짜: 2015년 10월 20일*

{{site.data.keyword.Bluemix}} Local은 {{site.data.keyword.Bluemix_notm}} 클라우드 기반 플랫폼의 강력함 및 민첩성을 데이터 센터로 가져옵니다. {{site.data.keyword.Bluemix_notm}} Local을 사용하여 안전하게 연결되고 {{site.data.keyword.Bluemix_notm}} Public 동기화를 유지하는 동안 회사 방화벽 뒤에 가장 민감한 워크로드를 보호할 수 있습니다. {:shortdesc}

IBM®은 환경의 맨 위에서 실행되는 앱과 서비스를 빌드하는 데 주력할 수 있도록 사용자 환경을 모니터하고 유지보수하기 위한 서비스로 클라우드 작업을 사용합니다. 또한 IBM은 비즈니스에 집중할 수 있도록 플랫폼 업데이트를 처리합니다.

{{site.data.keyword.Bluemix_notm}} Local에는 사용자가 독점적으로 사용 가능한 로컬 서비스를 표시하는 신디케이트된 개인용 카탈로그가 포함되어 있습니다. 또한 {{site.data.keyword.Bluemix_notm}} Public에서
사용 가능하며 여기에서 신디케이트된 추가 서비스도 포함되어 있습니다. 

{{site.data.keyword.Bluemix_notm}} Local은 최고 성능과 가장 안전한 클라우드 인프라를 사용할 수 있도록 회사 방화벽 뒤에 있는 가상 머신에 설치됩니다. IBM은 IBM의 Relay 기술을 통해 데이터 센터에 {{site.data.keyword.Bluemix_notm}} Local을 설치하고 원격으로 모니터하고 관리합니다.

Relay는 {{site.data.keyword.Bluemix_notm}} Local에 포함된 전달 기능이며 항상 최신이고 안정적이며 보안 시스템을 포함하기 위해 IBM이 모든 로컬 배치에 자동으로 지속적인 업데이트를 제공하도록 합니다. Relay는 각 {{site.data.keyword.Bluemix_notm}} Local 인스턴스에 특정한 인증서를 사용하여 도입/인식(Inception) 가상 머신에서 생성된 개방형, 아웃바운드 SSL, VPN 터널을 통해 보안 연결을 달성합니다. 이 터널의 트래픽은 인스턴스의 플랫폼, 계산 자원 및 서비스를 제공하고 유지보수하기 위한 Urban Code Deployer 자동화입니다.

![{{site.data.keyword.Bluemix_notm}} Local 개요](images/bluemixlocalarchitecture.png "Bluemix Local 개요")

*그림 1. {{site.data.keyword.Bluemix_notm}} Local 상세 개요*

{{site.data.keyword.Bluemix_notm}} Local 환경은 운영 보안이라는 면에서 공용 {{site.data.keyword.Bluemix_notm}}와 보안 표준이 동일합니다. 사용자에게 인프라 및 실제 보안을 통해 제어를 제공하는 하드웨어 및 인프라를 제공합니다. 로컬 {{site.data.keyword.Bluemix_notm}}에 대한 개발자 액세스는 LDAP 정책에 의해 제어되며 이 정책은 환경을 설정할 때 {{site.data.keyword.Bluemix_notm}} 팀에서 구성할 수 있습니다. 로컬 환경 내에서는 관리 콘솔을 사용하여 사용자 역할 및 권한을 관리할 수 있습니다. 

{{site.data.keyword.Bluemix_notm}} Local은 {{site.data.keyword.Bluemix_notm}} 런타임 및 64GB의 계산 메모리가 모두 포함되어 제공됩니다. 

또한 {{site.data.keyword.Bluemix_notm}} Local에 선택할 수 있는 서비스 세트가 있습니다. 

| **유형** | **이름** | **설명** |    
|----------|----------|-----------------|
|포함 | {{site.data.keyword.Bluemix_notm}} 런타임 | VM 및 운영 체제를 설정하고 관리할 필요 없이 신속하게 앱을 시작하고 실행하려면 런타임을 사용하십시오. 모든 {{site.data.keyword.Bluemix_notm}} 런타임은 {{site.data.keyword.Bluemix_notm}} Local 인스턴스에서 사용자에게 사용 가능합니다.|
|포함 | {{site.data.keyword.autoscaling}}| 정책에 따라 애플리케이션의 계산 용량을 동적으로 늘리거나 줄입니다. 이 서비스를 사용하면 {{site.data.keyword.Bluemix}} Local 환경에서 무제한 사용이 가능합니다. |
|선택사항 |{{site.data.keyword.datacshort}}| 이 서비스는 앱에 대한 분산 캐싱 시나리오를 지원하는 인메모리 데이터 그리드를 제공합니다. 50GB의 인메모리 캐시가 포함됩니다.  |
|선택사항 | {{site.data.keyword.APIM}} | {{site.data.keyword.APIMfull}} 서비스는
API를 구성, 관리하고 소셜화하는 데 사용합니다. 프록시 URL을 사용하거나 HTTP 데이터 소스의 데이터를 어셈블하여 자원들로 API를 가져올 수 있습니다. {{site.data.keyword.APIM}} 서비스를 사용하면 API가 어떻게 이용되는지를 관리할 수 있게 된다는 이점이 있습니다.  |

*표1. 로컬 서비스*

##{{site.data.keyword.Bluemix_notm}} Local 인스턴스 설정
{: #setuplocal}

{{site.data.keyword.Bluemix_notm}} Local은 사용자가 관리하는 자체 하드웨어에 호스팅된 {{site.data.keyword.Bluemix_notm}} Public 오퍼링의 개인용 버전을 제공하도록 디자인되었습니다. {{site.data.keyword.Bluemix_notm}} 서비스 및 런타임을 사용하여 안전한 고객 호스트 및 관리 클라우드 환경의 컴퓨팅 요구사항을 지원할 수 있습니다. 

IBM은 비밀번호로 보호되는 로그인을 사용하여 {{site.data.keyword.Bluemix_notm}} Local에 대한 액세스를 제공합니다. 서비스, 런타임 및 연관된 자원에 액세스하고
{{site.data.keyword.Bluemix_notm}} 앱을 배치 및 제거할 수 있습니다. 다음 단계를 검토하여 IBM 담당자와 함께 {{site.data.keyword.Bluemix_notm}}의 로컬 인스턴스를 설정하십시오.

{{site.data.keyword.Bluemix_notm}}의 개인용 버전 설정:

<ol>
<li>로컬 인스턴스 설정은 <a href="index.html#localinfra">{{site.data.keyword.Bluemix_notm}} Local 인프라 요구사항</a>을 검토하십시오.</li>
<li>시작하려면 IBM 지정 계정 담당자에게 문의하거나 <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a>에 문의하십시오. </li>
<li>IBM과 제공을 위한 마일스톤 날짜가 포함된 {{site.data.keyword.Bluemix_notm}} Local 계약을 체결하십시오. <ol type="a">
	<li>{{site.data.keyword.Bluemix_notm}} Local 인스턴스의 사용 요금에 관해 IBM과 함께 작업하십시오. 매월 발생하는 요금은 사용하고자 하는 로컬 서비스 및 모든 {{site.data.keyword.Bluemix_notm}} 공용 서비스에 대한 구독을 기반으로 합니다. 
그런 다음 해당 구독 계약과 더불어 사용하는 모든 항목에 대한 송장을 수령하십시오. </li>
	<li>{{site.data.keyword.Bluemix_notm}} Local 인스턴스 설정의 각 단계마다 최종 기한을 식별하십시오. </li>
	</ol>
	</li>
<li>플랫폼 및 계정을 작성한 후 로컬 인스턴스를 시작하고 실행하기 위해 필요한 역할을 담당할 조직의 직원을 식별하십시오. 각 역할마다 해당하는 IBM 담당자가 있습니다. <br />
<p>고객 역할:</p>
<dl>
<dt>**조달 담당자**</dt>
<dd>프로젝트의 특정 측면에 관해 작업하는 조직의 적합한 직원 식별을 포함하여 {{site.data.keyword.Bluemix_notm}} Local 환경의 설정에 관해 IBM 담당자와 함께 작업합니다. 이 역할은 패턴 선택, 상업적 배열 및 고객 자원에 대한 액세스 배열을 감독합니다. 이 조달 담당자는 로컬 인스턴스를 설정하기 위한 전체 담당자입니다. </dd>
<dt>**규제 준수 담당자**</dt>
<dd>IBM 담당자와 함께 작업하여 보안 요구사항을 충족하는 토폴로지 및 배치 옵션을 선택합니다. 이 역할은 규제 준수 목표 및 목표를 달성하는 배치 패턴을 결정하기 위해 IBM 규제 준수 컨설턴트와 함께 작업합니다.</dd>
<dt>**네트워크 전문가**</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 배치의 네트워크 플랜에 관해 IBM 담당자와 함께 작업합니다. 이 역할은 IBM 담당자에게 요구사항을 제공하며 구현 플랜에 관해 함께 작업합니다. 설치 및 검증 단계의 끝에서 이 역할은 기업 표준 규제를 준수하는 네트워크 구성을 "사인오프"합니다.</dd>
<dt>**DevOps 담당자**</dt>
<dd>IBM 담당자와 함께 작업하여 {{site.data.keyword.Bluemix_notm}} 플랫폼, 서비스 및 런타임에 필요한 유지보수 업데이트를 계획하고 적용합니다. 이 역할은 {{site.data.keyword.Bluemix_notm}} Local 인스턴스의 구성과 관련해서도 IBM 담당자와 함께 작업합니다. </dd>
</dl>
<p>IBM 역할:</p>
<dl>
<dt>**IBM 프로비저닝 관리자**</dt>
<dd>고객 조달 담당자와 함께 작업하여 고객 환경을 설정합니다.</dd>
<dt>**IBM 규제 준수 컨설턴트**</dt>
<dd>고객 규제 준수 담당자와 함께 작업하여 보안 요구사항을 충족하는 토폴로지 및 배치 옵션을 선택합니다. </dd>
<dt>**IBM 네트워크 전문가**</dt>
<dd>고객 네트워크 전문가와 함께 작업하여 배치의 네트워크 플랜을 연결합니다. 이 역할은 고객과 함께 작업하여 요구사항을 수집하고 구현 플랜을 작성합니다. 이 역할은 또한 자동화된 테스트를 수행하여 구현 플랜의 실제 결과를 확인합니다.</dd>	
<dt>**IBM DevOps 담당자**</dt>
<dd>배치 토폴로지의 설치 및 지속적인 유지보수에 대해 고객 DevOps 담당자와 함께 작업합니다. 이 역할은 고객과 함께 플랫폼 및 서비스에 필요한 업데이트를 계획하고 수행합니다.</dd>
</dl>
</li>
<li>하드웨어를 제공하고 IBM은 기업 네트워크 및 {{site.data.keyword.Bluemix_notm}} Local 인스턴스 간의 네트워크 연결을 정의하고 설정하도록 도와줍니다. 인프라 요구사항에 대한 자세한 정보는 <a href="index.html#localinfra">{{site.data.keyword.Bluemix_notm}} Local 인프라 요구사항</a>을 참조하십시오.
<ol type="a">
	<li>IBM은 제공된 내용을 기반으로 네트워크 액세스 및 LDAP를 구성합니다. 관리 액세스 권한이 지정된 담당자에게 부여됩니다. 지원 및 청구에 대한 담당자도 지정해야 합니다. </li>
	<li>IBM은 로컬 환경에서 로컬 서비스 및 다수의 공용 {{site.data.keyword.Bluemix_notm}} 서비스를 표시하는 신디케이트된 카탈로그를 설정합니다. </li>
	<li>네트워크 및 방화벽 구성과 LDAP 엔드포인트 및 액세스를 유효성 검증하십시오. </li>
	</ol>
</li>
</ol>
	
##{{site.data.keyword.Bluemix_notm}} Local 인프라 요구사항
{: #localinfra}

{{site.data.keyword.Bluemix_notm}} Local에 대해 사용자는
로컬 인스턴스를 호스팅하기 위한 실제 보안 및 인프라를 소유합니다. IBM은
{{site.data.keyword.Bluemix_notm}} Local을 설정하기 위해 다음 요구사항을 설정합니다. 
###하드웨어
사용 가능한 하드웨어의 유형 및 크기에 대한 요구사항이 있지만 세트 자원의 총 요구사항을 충족하는
모든 조합을 선택할 수 있습니다. 
<dl>
<dt>**VMware ESXi 하드웨어**</dt>
<dd>
ESXi는 실제 서버에서 실행되고 프로세서, 메모리, 스토리지 및 자원을 다중 가상 머신으로
추상화하는 가상화 계층입니다. ESXi당 최소 실제 코어 수가 8인 조건에 대해 다음 자원 총계를 충족하는 임의 조합을 선택하십시오. 다음 사양은 {{site.data.keyword.Bluemix_notm}} 코어 런타임 전용입니다.
<ul>
<li>각각 2.0GHz 이상의 48개 실제 코어</li>
<li>756GB의 실제 RAM</li>
</li>7.5TB의 총 데이터 저장소 크기
<ul>
<li>{{site.data.keyword.Bluemix_notm}}를 보유할 7TB의 데이터 저장소</li>
<li>도입/인식(Inception) 가상 머신을 보유할 500GB의 데이터 저장소</li>
</ul>
</ul>
<p><strong>참고:</strong> 다중 데이터 저장소를 사용하는 경우 각각에 대해 동일한 접두부를 사용하십시오. </p>
</dd>
<dt>**고가용성**</dt>
<dd>
단일 노드 장애를 지원하려면 n+1 ESXi가 있어야 합니다. 예를 들어, 각각 16x 코어를 의미하는 두 ESXi가 사용되는 경우, 세 번째가 필요합니다. <p><strong>참고:</strong> 고객 VMware 관리자는 클러스터에서 고가용성 장애 복구를 엄격하게 적용하여 자원을 보장하기로 결정할 수 있습니다. </p>
</dd>
<dt>**네트워크**</dt>
<dd>
권장 요구사항에는 아웃바운드 인터넷 액세스 권한을 가진 10개의 고객 네트워크 IP 주소가 있는
고객 액세스 가능 포트 그룹이 포함됩니다. 그런 다음 {{site.data.keyword.Bluemix_notm}} Local에 대해
사용되는 ESXi들 사이에만 두 번째 개인용 VLAN을 정의하십시오.
이 VLAN은 VMware에서 포트 그룹으로 표시됩니다. {{site.data.keyword.Bluemix_notm}} Local은
이를 더 안전하고 라우팅 문제를 피하는 데 도움이 되는 개인용 서브넷으로 사용합니다. </dd>
</dl>

###vCenter 서버 구성
다음 버전, 데이터 센터, 자원 풀 및 데이터 저장소 요구사항을 검토하십시오. 
<dl>
<dt>**지원되는 VMware 버전**</dt>
<dd>vCenter 및 ESXi 5.1 및 5.5</dd>
<dt>**데이터 센터**</dt>
<dd>데이터 센터가 존재하지 않는 경우, 작성하십시오. </dd>
<dt>**데이터 센터 폴더**</dt>
<dd>데이터 센터에서 전파된 관리자 액세스 권한을 부여하지 않으려면 클러스터와 동일한 이름으로 VM 폴더를 작성하십시오. </dd>
<dt>**클러스터**</dt>
<dd>특히 {{site.data.keyword.Bluemix_notm}} Local 사용을 위해
클러스터를 작성하십시오. 클러스터 이름의 예는 `bluemix`입니다. </dd>
<dt>**자원 풀**</dt>
<dd>{{site.data.keyword.Bluemix_notm}} Local 클러스터 아래에 자원 풀을 작성하십시오. 자원 풀 이름의 예는
`local`입니다. </dd>
</dt>**데이터 저장소**</dt>
<dd>{{site.data.keyword.Bluemix_notm}}의 초기 배치에는 7.5TB가 필요합니다. <br />
<br />
**참고**: 둘 이상의 데이터 저장소를 사용하는 경우 각 데이터 저장소는 동일한 접두부로 시작해야 합니다. 접두부가 동일한 여러 데이터 저장소 이름의 예는
`bluemix_datastore_01` 및 `bluemix_datastore_02`입니다. </dd>
</dl>

###네트워크 대역폭
권장되는 처리량은 5Mbps 위 및 5Mbps 아래이며,
월별 데이터 사용량은 10GB로 예상할 수 있습니다. IBM은 대규모 데이터 번들이 전달될 때 최대 3GB로 설정하기로 Windows와 합의했습니다. 
###VMware 권한
다음 역할 및 권한을 설정하십시오. 각 권한에 대해 전파가 설정됩니다. 권한이
전파되는 경우, 권한은 오브젝트 계층 구조를 따라 아래쪽으로 전달됩니다. 그러나 하위 오브젝트의 권한은
상위 오브젝트로부터 전파된 권한을 항상 대체합니다. 
<dl>
<dt>**v 센터 서버**</dt>
<dd>역할을 읽기 전용 및 전파되지 않음으로 설정하십시오. <br />
<br />
**참고**: 이 역할은 특정 디스크 오퍼레이션에 대한 태스크 상태를 검색하는 데 필요합니다. </dd>
<dt>**데이터 센터**</dt>
<dd>"{{site.data.keyword.Bluemix_notm}}" 역할을 작성하고 **하위 레벨 파일 오퍼레이션** 및 **가상 머신 파일 업데이트**를 포함하여 **데이터 저장소**에 대한 권한을 부여하십시오. <br />
<br />
**참고**: 이 역할은 데이터 저장소에 대한 파일 포스트를 지원하는 데 필요합니다. </dd>
<dt>**클러스터**</dt>
<dd>역할을 관리자 및 전파됨으로 설정하십시오. </dd>
<dt>**데이터 저장소**</dt>
<dd>각 {{site.data.keyword.Bluemix_notm}} 데이터 저장소에 대해
역할을 관리자 및 전파됨으로 설정하십시오. </dd>
<dt>**네트워크**</dt>
<dd>공용 및 개인용 포트 그룹을 관리자 역할, 전파되지 않음으로 설정하십시오. </dd>
</dl>

###DEA(Droplet Execution Agent) 풀
각 DEA는 다음으로 구성됩니다. 
- 16 - 32GB의 RAM
- 2x - 4x vCPU
- 150 - 300GB의 스토리지

예를 들어, ESXi 호스트 크기가 256GB의 메모리와 16x 코어인 경우,
8개의 DEA가 추가됩니다. ESXi 호스트 크기가 64GB의 메모리와 8x 코어인 경우, 두 개의 ESXi와 네 개의 DEA를
추가해야 합니다. 4개의 DEA마다 추가로 1.5TB의 스토리지가 필요합니다. 이 예제는 32GB의 RAM, 4x vCPU 및
300GB의 스토리지로 구성된 DEA를 기반으로 합니다. 

##로컬 인스턴스 유지보수
{: #maintainlocal}

IBM은 Bluemix Local 플랫폼, 런타임 및 서비스에 대해 IBM이 적합하다고 판단되면 업데이트 및 수정사항을 유지보수하고 설치합니다. 유지보수 창 중에는 서비스를 사용하지 못할 수 있습니다.

**중요**: IBM은 필요에 따라 비상 유지보수를 적용할 수 있도록 서비스를 인터럽트할 수 있는 권한을 보유합니다. IBM은 스케줄된 유지보수 시간을 변경할 수 있지만 그러한 변경은 물론 비상 유지보수 정보에 대해서도 사용자에게 알려드릴 것입니다. 

다음 유형의 유지보수가 {{site.data.keyword.Bluemix_notm}} Local에 필요합니다. 
<dl>
<dt>**표준 유지보수 창**</dt>
<dd>해당 서비스는 사전 정의된 표준 유지보수 창을 이용하며 서비스가 사용 불가능할 수 있습니다. IBM은 유지보수를 수행하기 위해 고객 승인을 요구하지 않지만 서비스에 미치는 영향을 최소화하기 위해 시도합니다.<br />
<br />
IBM은 각각의 유지보수 창에 대해 계획된 변경사항의 브로드캐스트 메시지를 이메일, 전화 또는 기타 방법을 통해 전송합니다. <br />
<br />
**중요**: 유지보수 기간 중에는 일부 서비스를 사용하지 못할 수도 있습니다. </dd>

<dt>**월별 변경 창**</dt>
<dd>월별 유지보수 창은 21일 기간 내에 사용자와 IBM 간 조정을 기반으로 적용됩니다. 사용자는 작동하지 않을 수 있는 21일 기간 내에 특정 날짜 또는 시간을 IBM에 제공할 수 있습니다. IBM은 해당 시간을 중심으로 업데이트를 스케줄하기 위해 시도합니다. 요청을 기반으로 IBM은 사용자에게 스케줄된 유지보수 창을 전달합니다. 월별 변경 창은 실행 중인 Bluemix Local 환경에 영향을 미칠 것으로 예상되지 않습니다.<br />
<br />
**참고**: 업데이트할 특정 시간을 요청하지 않는 경우 유지보수는 창의 마지막에 자동으로 적용됩니다. <br />
<br />
**관리 > 시스템 정보**로 이동하여 보류 중인 업데이트를 확인하고 사용 불가능한 날짜를 설정하며 업데이트를 승인하십시오. 알림 및 보류 중인 업데이트 스케줄링에 대한 자세한 정보는 <a href="../admin/index.html#oc_system">시스템 정보 보기</a>를 참조하십시오.</dd>

<dt>**기타**</dt>
<dd>IBM은 서비스(특히 Bluemix 환경, 런타임 및 서비스의 가용성)에 영향을 줄 수 있는 모든 유지보수를 표준 및 월간 창으로 제한하고자 합니다.
기타 변경 창은 환경 관리를 위한 예외 기반으로 사용될 수 있습니다. IBM은 그러한 변경 창 동안에 사용자에게 미치는 영향을 최소화하기 위해 합리적인 노력을 기울일 것이며 이에 대해 사전에 알려드릴 것입니다. </dd>
</dl>

로컬 인스턴스의 유지보수를 설정하려면 IBM 전용 계정 담당자와 함께 작업하여 표준 유지보수에 대해 합의된 기간을 식별하십시오. 
   
