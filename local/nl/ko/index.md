{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} Local
{: #local}
*마지막 업데이트 날짜: 2016년 1월 15일*

{{site.data.keyword.Bluemix}} Local은 {{site.data.keyword.Bluemix_notm}} 클라우드 기반 플랫폼의 강력함 및 민첩성을 데이터 센터로 가져옵니다. {{site.data.keyword.Bluemix_notm}} Local을 사용하여 안전하게 연결되고 {{site.data.keyword.Bluemix_notm}} Public 동기화를 유지하는 동안 회사 방화벽 뒤에 가장 민감한 워크로드를 보호할 수 있습니다.
{:shortdesc}

IBM®은 환경의 맨 위에서 실행되는 앱과 서비스를 빌드하는 데 주력할 수 있도록 사용자 환경을 모니터하고 유지보수하기 위한 서비스로 클라우드 작업을 사용합니다. 또한 IBM은 비즈니스에 집중할 수 있도록 플랫폼 업데이트를 처리합니다.

{{site.data.keyword.Bluemix_notm}} Local에는 사용자가 독점적으로 사용 가능한 로컬 서비스를 표시하는 신디케이트된 개인용 카탈로그가 포함되어 있습니다. 또한 {{site.data.keyword.Bluemix_notm}} Public에서
사용 가능하며 여기에서 신디케이트된 추가 서비스도 포함되어 있습니다. 신디케이트된 카탈로그는 공용 및 개인 서비스로 구성되는 하이브리드 애플리케이션 작성 기능을 제공합니다. 데이터에 대한 개인정보 보호정책 및 보안 기준에 따라 사용자 비즈니스의 요구사항을 충족해야 하는 공용 서비스를 결정하는 옵션이 있습니다.

{{site.data.keyword.Bluemix_notm}} Local은 최고 성능과 가장 안전한 클라우드 인프라를 사용할 수 있도록 회사 방화벽 뒤에 있는 가상 머신에 설치됩니다. IBM은 IBM의 Relay 기술을 통해 데이터 센터에 {{site.data.keyword.Bluemix_notm}} Local을 설치하고 원격으로 모니터하고 관리합니다.

![{{site.data.keyword.Bluemix_notm}} Local 개요](images/bluemixlocalarchitecture.png "Bluemix Local 개요")

*그림 1. {{site.data.keyword.Bluemix_notm}} Local 상세 개요*

{{site.data.keyword.Bluemix_notm}} Local 환경은 운영 보안이라는 면에서 공용 {{site.data.keyword.Bluemix_notm}}와 보안 표준이 동일합니다. 사용자에게 인프라 및 실제 보안을 통해 제어를 제공하는 하드웨어 및 인프라를 제공합니다. 로컬 {{site.data.keyword.Bluemix_notm}}에 대한 개발자 액세스는 LDAP 정책에 의해 제어되며 이 정책은 환경을 설정할 때 {{site.data.keyword.Bluemix_notm}} 팀에서 구성할 수 있습니다. 로컬 환경 내에서는 관리 콘솔을 사용하여 사용자 역할 및 권한을 관리할 수 있습니다.

{{site.data.keyword.Bluemix_notm}} Local은 {{site.data.keyword.Bluemix_notm}} 런타임 및 64GB의 계산 메모리가 모두 포함되어 제공됩니다.

또한 {{site.data.keyword.Bluemix_notm}} Local에 선택할 수 있는 서비스 세트가 있습니다.

| **유형** | **이름** | **설명** |    
|----------|----------|-----------------|
|포함 | {{site.data.keyword.Bluemix_notm}} 런타임 | VM 및 운영 체제를 설정하고 관리할 필요 없이 신속하게 앱을 시작하고 실행하려면 런타임을 사용하십시오. 모든 {{site.data.keyword.Bluemix_notm}} 런타임은 {{site.data.keyword.Bluemix_notm}} Local 인스턴스에서 사용자에게 사용 가능합니다.|
|포함 | {{site.data.keyword.autoscaling}}| 정책에 따라 애플리케이션의 계산 용량을 동적으로 늘리거나 줄입니다. 이 서비스를 사용하면 {{site.data.keyword.Bluemix}} Local 환경에서 무제한 사용이 가능합니다.|
|선택사항 |{{site.data.keyword.datacshort}}| 이 서비스는 앱에 대한 분산 캐싱 시나리오를 지원하는 인메모리 데이터 그리드를 제공합니다. 50GB의 인메모리 캐시가 포함됩니다. |
|선택사항 | {{site.data.keyword.APIM}} | {{site.data.keyword.APIMfull}} 서비스는
API를 구성, 관리하고 소셜화하는 데 사용합니다. 프록시 URL을 사용하거나 HTTP 데이터 소스의 데이터를 어셈블하여 자원들로 API를 가져올 수 있습니다. {{site.data.keyword.APIM}} 서비스를 사용하면 API가 어떻게 이용되는지를 관리할 수 있게 된다는 이점이 있습니다. |

*표1. 로컬 서비스*

### Relay

Relay는 {{site.data.keyword.Bluemix_notm}} Local에 포함된 전달 기능이며 항상 최신이며 보안 시스템을 포함하기 위해 IBM이 모든 로컬 배치에 자동으로 지속적인 최신 업데이트를 제공하도록 합니다. Relay는 각 {{site.data.keyword.Bluemix_notm}} Local 인스턴스에 특정한 인증서를 사용하여 도입/인식(Inception) 가상 머신 사내 구축형에서 생성된 개방형, 아웃바운드 SSL, VPN 터널을 통해 보안 연결을 달성합니다. 모든 초기 {{site.data.keyword.Bluemix_notm}} 릴리스는 배치 및 업데이트를 위한 자동 에이전트 머신으로도 작동하는 도입/인식(Inception) 가상 머신에서 사용 가능합니다. SSL 연결은 도입/인식(Inception) 가상 머신에서 시작되고, {{site.data.keyword.Bluemix_notm}} 자동 서버에 보안 연결이 다시 설정되면 {{site.data.keyword.Bluemix_notm}} 릴리스의 일관성을 점검한 후 업데이트를 배치할 수 있습니다.

이 터널의 트래픽은 인스턴스의 플랫폼, 계산 자원 및 서비스를 제공하고 유지보수하기 위한 자동화입니다. 이 연결에는 인바운드 웹 포트 443이 사용됩니다. 릴레이는 자동 에이전트 전용 액세스로 제한됩니다. IBM은 릴레이 기능을 사용하여 지속적 테스트와 유효성 검증 프로세스를 통한 플랫폼 업데이트를 제공하여 사용자의 로컬 환경에 푸시되는 모든 배치의 안정성과 안전을 보장합니다.

사용자는 관리자 자격으로 사고, 문제점, 변경, 용량 및 보안 관리를 위해 환경과 관련한 일체의 가시성을 갖습니다.  관리자는 관리 콘솔을 사용하여 환경 정보에 액세스합니다. 릴레이 기술은 최신 데이터를 사용하여 관리 콘솔을 최신 상태로 유지합니다. 사용자 액세스, 보안 로그, 신디케이트된 카탈로그 제어, 업데이트 및 문제 해결을 위한 통신 등에 대해 자세히 알려면 [Managing {{site.data.keyword.Bluemix_notm}} Local 및 {{site.data.keyword.Bluemix_notm}} Dedicated](../admin/index.html#mng)를 참조하십시오.

##{{site.data.keyword.Bluemix_notm}} Local 인스턴스 설정
{: #setuplocal}

{{site.data.keyword.Bluemix_notm}} Local은 사용자가 관리하는 자체 하드웨어에 호스팅된 {{site.data.keyword.Bluemix_notm}} Public 오퍼링의 개인용 버전을 제공하도록 디자인되었습니다. {{site.data.keyword.Bluemix_notm}} 서비스 및 런타임을 사용하여 안전한 고객 호스트 및 관리 클라우드 환경의 컴퓨팅 요구사항을 지원할 수 있습니다.

IBM은 비밀번호로 보호되는 로그인을 사용하여 {{site.data.keyword.Bluemix_notm}} Local에 대한 액세스를 제공합니다. 서비스, 런타임 및 연관된 자원에 액세스하고
{{site.data.keyword.Bluemix_notm}} 앱을 배치 및 제거할 수 있습니다. 다음 단계를 검토하여 IBM 담당자와 함께 {{site.data.keyword.Bluemix_notm}}의 로컬 인스턴스를 설정하십시오.

{{site.data.keyword.Bluemix_notm}}의 개인용 버전 설정:

<ol>
<li>로컬 인스턴스 설정은 <a href="index.html#localinfra">{{site.data.keyword.Bluemix_notm}} Local 인프라 요구사항</a>을 검토하십시오.</li>
<li>시작하려면 IBM 지정 계정 담당자에게 문의하거나 <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a>에 문의하십시오.</li>
<li>IBM과 제공을 위한 마일스톤 날짜가 포함된 {{site.data.keyword.Bluemix_notm}} Local 계약을 체결하십시오.
	<ol type="a">
	<li>{{site.data.keyword.Bluemix_notm}} Local 인스턴스의 사용 요금에 관해 IBM과 함께 작업하십시오. 매월 발생하는 요금은 사용하고자 하는 로컬 서비스 및 모든 {{site.data.keyword.Bluemix_notm}} 공용 서비스에 대한 구독을 기반으로 합니다. 그런 다음 해당 구독 계약과 더불어 사용하는 모든 항목에 대한 송장을 수령하십시오.</li>
	<li>{{site.data.keyword.Bluemix_notm}} Local 인스턴스 설정의 각 단계마다 최종 기한을 식별하십시오.</li>
	</ol>
	</li>
<li>플랫폼 및 계정을 작성한 후 로컬 인스턴스를 시작하고 실행하기 위해 필요한 역할을 담당할 조직의 직원을 식별하십시오. 사용자가 지정하는 역할에 대한 자세한 정보는 <a href="index.html#rolesresponsibilities" target="_blank">{{site.data.keyword.Bluemix_notm}} Local 역할 및 책임</a>을 참조하십시오.
</li>
<li>하드웨어를 제공하고 IBM은 기업 네트워크 및 {{site.data.keyword.Bluemix_notm}} Local 인스턴스 간의 네트워크 연결을 정의하고 설정하도록 도와줍니다. 인프라 요구사항에 대한 자세한 정보는 <a href="index.html#localinfra">{{site.data.keyword.Bluemix_notm}} Local 인프라 요구사항</a>을 참조하십시오.
	<ol type="a">
	<li>IBM은 제공된 내용을 기반으로 네트워크 액세스 및 LDAP를 구성합니다. 관리 액세스 권한이 지정된 담당자에게 부여됩니다. 지원 및 청구에 대한 담당자도 지정해야 합니다.</li>
	<li>IBM은 로컬 환경에서 로컬 서비스 및 다수의 공용 {{site.data.keyword.Bluemix_notm}} 서비스를 표시하는 신디케이트된 카탈로그를 설정합니다.</li>
	<li>네트워크 및 방화벽 구성과 LDAP 엔드포인트 및 액세스를 유효성 검증하십시오.</li>
	</ol>
</li>
</ol>

사용자 환경에 처음 배치하고 구성하기 위해서는 다음 목록과 비슷하게 프로세스가 진행되어야 합니다. 각 태스크를 책임지는 담당자에 대한 자세한 정보는 [역할 및 책임](../local/index.html#rolesresponsibilities)을 참조하십시오.

<ol>
<li>계산 자원, 네트워킹 및 스토리지에 대한 스펙에 부합하는 VMware 구성을 제공합니다. 인프라 요구사항에 대한 자세한 정보는 <a href="../local/index.html#localinfra">{{site.data.keyword.Bluemix_notm}} Local 인프라 요구사항</a>을 참조하십시오.</li>
<li>도입/인식(Inception) 가상 머신에 사용되는 vCenter 클러스터 신임 정보를 제공합니다. 다음 정보를 제공해야 합니다.
<ul>
<li>VMware 클러스터의 이름</li>
<li>사용자 ID와 비밀번호를 포함하는 vCenter 클러스터 신임 정보</li>
<li>데이터 저장소 이름(스토리지 LUN 이름)</li>
<li>VLAN ID/VMware 포트 그룹</li>
<li>자원 풀 이름</li>
</ul>
</li>
<li>사용자와 IBM이 함께 협력하여 이전 태스크에서 제공한 신임 정보의 유효성을 검증합니다.</li>
<li>사용자 네트워크의 7개 IP 주소를 제공합니다. 내부 {{site.data.keyword.Bluemix_notm}} 구성요소에 아웃바운드 인터넷 액세스를 허용하기 위해 보안 웹 프록시를 사용하는 경우, 연결에 필요한 신임 정보를 제공해야 합니다.
<p>**참고**: 웹 프록시에 보안이 설정되어 있지 않으면 신임 정보를 제공할 필요가 없습니다. 또한, 일부 {{site.data.keyword.Bluemix_notm}} Local 고객은 웹 프록시를 사용하지 않는다는 점에 유의하십시오.</p></li>
<li>IBM은 배치를 시작하기 전에 웹 프록시를 통해 허용되어야 하는 URL의 화이트리스트를 제공합니다.</li>
<li>배치에 필요한 도메인 이름 및 사용할 ID를 지정합니다. 로컬 인스턴스를 설정할 때 특별히 정의된 두 개의 도메인이 나타나고, 이 두 개 도메인의 접두부를 선택합니다. 예를 들어, <code>*mycompany*.bluemix.net</code> 및 <code>*mycompany*.mybluemix.net</code>에 대한 접두부를 선택합니다. 그런 다음, 전체 도메인을 선택하여 사용자 정의 도메인을 작성할 수도 있습니다.
<p>사용자 정의 도메인은 필요한 만큼 선택할 수 있습니다. 그러나, 사용자 정의 도메인의 인증은 사용자 자신이 책임져야 합니다. 사용자 정의 도메인 작성에 대한 자세한 정보는 <a href="../manageapps/updapps.html#domain">사용자 정의 도메인 작성 및 사용</a>을 참조하십시오.</p></li>
<li>IBM 운영 센터에 다시 연결하도록 릴레이를 구성하는 데 사용할 기술을 IPSec 또는 OpenVPN 터널 중에서 선택합니다.</li>
<li>IBM이 {{site.data.keyword.Bluemix_notm}} 클러스터 내에 도입/인식(Inception) 가상 머신을 설치하고 시작합니다. 고유 VMware를 제공하는 경우, 고객 대표가 이 태스크를 완료할 수 있도록 IBM 담당자가 도와드립니다.</li>
<li>IBM이 IBM 운영 센터와 다시 통신하도록 릴레이를 구성합니다.</li>
<li>도입/인식(Inception) 가상 머신 저장소는 업데이트된 빌드 아티팩트를 가져옵니다.</li>
<li>회사 LDAP 디렉토리 인스턴스에 연결하기 위해 IBM 신임 정보를 제공합니다.</li>
<li>IBM이 자동화를 사용하여 코어 {{site.data.keyword.Bluemix_notm}} 플랫폼을 배치합니다.</li>
<li>IBM이 탄력적 런타임, 콘솔, 관리 기능 및 모니터링을 포함하는 코어 플랫폼을 배치합니다.</li>
<li>IBM이 환경에 대한 사용자의 관리 액세스 권한을 구성합니다.</li>
<li>IBM이 공용 서비스를 사용하기 위해 로컬 배치의 신디케이션된 카탈로그를 Public {{site.data.keyword.Bluemix_notm}} 인스턴스에 연결합니다. 로컬 인스턴스에서는 공용 서비스를 기본적으로 사용할 수 있습니다. 카탈로그 관리를 위한 관리 페이지에서 로컬 인스턴스에 대해 서비스를 켜거나 끌 수 있습니다.</li>
<li>경보에 대응하기 위해 IBM 운영 팀에서 모니터링하는 로컬 인스턴스의 사용을 시작할 수 있습니다.</li>
</ol>

{{site.data.keyword.Bluemix_notm}} 인스턴스를 설정하고 나면 관리 페이지를 사용하여 {{site.data.keyword.Bluemix_notm}} 인스턴스를 모니터링하고 관리할 수 있습니다. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} Local 및 Dedicated 관리](../administer/index.html#mng)를 참조하십시오. 업그레이드 및 유지보수에 대한 자세한 정보는 [로컬 인스턴스 유지보수](index.html#maintainlocal)를 참조하십시오.

##역할 및 책임
{: #rolesresponsibilities}

{{site.data.keyword.Bluemix_notm}} Local 계정을 설정하는 경우, 인스턴스를 시작하고 실행하기 위해 필요한 역할을 담당할 조직의 직원을 식별하십시오.

###역할

다음 목록은 사용자가 지정하는 고객 역할 및 책임을 보여줍니다.

<dl>
<dt>**조달 담당자**</dt>
<dd>프로젝트의 특정 측면에 관해 작업하는 조직의 적합한 직원 식별을 포함하여, {{site.data.keyword.Bluemix_notm}} Local 환경의 설정에 관해 IBM 담당자와 함께 작업합니다. 이 역할에 지정된 사용자는 패턴 선택, 상업적 배열 및 고객 자원에 대한 액세스 배열을 감독합니다. 이 조달 담당자는 로컬 인스턴스를 설정하기 위한 전체 담당자입니다.</dd>
<dt>**규제 준수 담당자**</dt>
<dd>IBM 담당자와 함께 작업하여 보안 요구사항을 충족하는 토폴로지 및 배치 옵션을 선택합니다. 이 역할에 지정된 사용자는 규제 준수를 달성하는 배치 패턴을 결정하기 위해 IBM 규제 준수 컨설턴트와 함께 작업합니다.</dd>
<dt>**네트워크 전문가**</dt>
<dd>{{site.data.keyword.Bluemix_notm}} 배치의 네트워크 플랜에 관해 IBM 담당자와 함께 작업합니다. 이 역할에 지정된 사용자는 IBM에서 요구하는 필수 네트워킹 스펙을 검토하고 구현 플랜에 따라 IBM과 함께 작업합니다. 설치 및 검증 단계의 끝에서 이 역할에 지정된 사용자는 네트워크 구성이 기업 표준 규제를 준수함을 승인합니다.</dd>
<dt>**DevOps 담당자**</dt>
<dd>IBM 담당자와 함께 작업하여 {{site.data.keyword.Bluemix_notm}} 플랫폼, 서비스 및 런타임에 필요한 유지보수 업데이트를 계획하고 적용합니다. 이 역할에 지정된 사용자는 {{site.data.keyword.Bluemix_notm}} Local 인스턴스의 구성과 관련해서도 IBM 담당자와 함께 작업합니다.</dd>
<dt>**IaaS 전문가**</dt>
<dd>VMware의 배치 플랜에 따라 IBM 담당자와 함께 작업합니다. 일반적으로 데이터 센터의 VMware 관리자입니다. 이 역할에 지정된 사용자는 <a href="../local/index.html#localinfra">{{site.data.keyword.Bluemix_notm}} Local 인프라 요구사항</a>을 검토하고 구현 플랜에 따라 IBM과 함께 작업합니다. 배치 단계의 끝에서 이 역할에 지정된 사용자는 배치가 laaS 계층의 기업 표준에 부합함을 승인합니다.</dd>
</dl>

고객 대표는 전담 CSM(Client Success Manager) 및 다른 IBM 전문가와 협력하여 사용자가 필요로 하는 지원이 반드시 제공될 수 있도록 보장해줍니다. CSM은 6개월간 무료로 제공됩니다. CSM은 다음 태스크를 완료합니다.

<ul>
<li>사용자와 IBM 사이에서 기술적 중재를 제공합니다.</li>
<li>업데이트, 업그레이드, IBM의 전문 상담, {{site.data.keyword.Bluemix_notm}} 지원 엔지니어의 초기 인에이블먼트를 조정합니다.</li>
<li>사용 가능한 지원 유형에 대한 정보를 제공합니다.</li>
<li>필요 시 초기 확대 지점으로 작용합니다.</li>
</ul>

{{site.data.keyword.Bluemix_notm}} 인스턴스와 관련하여 사용자와 협력하는 {{site.data.keyword.Bluemix_notm}} 지원 및 운영 팀은 다음과 같은 이유로만 사용자의 로컬 환경에 액세스합니다.

<ul>
<li>경보에 대한 응답 및 운영 유지보수 수행</li>
<li>지원 티켓에 보고된 문제점 재연</li>
</ul>

###책임

환경 설정에서부터 지속적 유지보수에 이르기까지 사용자와 IBM 모두 다양한 태스크를 완료해야 합니다. 다음 표에서는 도입/인식(Inception), 진행 및 완료 단계에서 태스크 완료를 위한 소유자와 필수 태스크를 보여줍니다.

도입/인식(Inception) 단계는 {{site.data.keyword.Bluemix_notm}} Local 환경을 설정하는 데 사용됩니다. 이 시점에서 사용자는 [Local 인프라 요구사항](../local/index.html#localinfra)에 대한 검토를 마쳤습니다. 이 단계의 1차 목표에는 다음이 포함됩니다.

- 재무 계약을 검토하고 전달을 위한 마일스톤 날짜를 설정합니다.
- {{site.data.keyword.Bluemix_notm}} 플랫폼을 작성하고 런타임 및 서비스에 대한 액세스를 제공합니다.
- 기업 네트워크 및 {{site.data.keyword.Bluemix_notm}} 오퍼레이션 간의 네트워크 연결을 정의하고 설정합니다.
- 관리 팀에 대한 역할을 식별하고 지정합니다.

*표 1. 도입/인식(Inception) 단계 태스크*

| **태스크** | **태스크 세부사항** | **책임자** |
|----------|------------------|-----------------------|
|규제 준수 표준 설정 | 환경에 필요한 정부, 산업 및 개인 기업 표준을 식별합니다. | 고객 |
|보안 및 규제 준수 통합 플랜 작성 | 보안 규제 준수를 달성하는 데 필요한 비용, 스케줄 및 자원을 포함하는 보안 및 통합 플랜을 작성합니다. | IBM |
|규제 준수 플랜 승인 | 규제 준수 플랜을 승인합니다. | 고객 |
|환경에 대한 크기 작성 |  	플랫폼에서 작성된 앱을 지원하는 데 필요한 초기 DEA 및 서비스 프로비저닝뿐 아니라 고가용성 및 재해 복구 목표를 고려하여 사전 정의된 선택사항을 토대로 환경의 크기를 작성합니다. 사용자와 IBM이 공동으로 필요한 데이터베이스, 신디케이트된 고객 카탈로그에 제공되는 서비스 등을 정의합니다. | IBM 및 고객 책임 공유 |
|아키텍처 선택 | 고가용성 및 재해 복구 요구사항을 고려하여 사전 정의된 선택사항을 토대로 아키텍처를 선택합니다. | IBM |
|재해 복구 목표 정의 | 환경에 대한 재해 복구 요구사항을 정의합니다. | 고객 |
|재해 복구 플랜 작성 | 재해 복구 플랜을 상의하여 정의합니다. IBM은 재해 복구 모델을 작성하고 사용자의 피드백 제공 및 플랜 승인 지점에서 사용자와 상의합니다. | IBM 및 고객 책임 공유 |
|백업 및 복구 플랜 작성 | 온오프 사이트 백업 분배를 위한 요구사항과 빈도를 정의하는 백업 및 복구 플랜을 작성합니다. IBM은 패브릭 컴포넌트, IBM 서비스, 사용자 역할을 포함하는 서비스 메타데이터 등을 백업합니다. 사용자는 사용자에게 책임이 있는 애플리케이션 고유 데이터를 백업합니다. | IBM 및 고객 책임 공유 |
|이벤트 발견 및 문제점 판별을 위한 식별 도구 | {{site.data.keyword.Bluemix_notm}} 플랫폼 레벨에서 이벤트 발견 및 문제점 판별에 사용되는 IBM 및 써드파티 도구를 식별합니다. | IBM |
|확대 플랜 정의 | 모니터링 컴포넌트를 통해 발견된 이벤트를 선별하고 해결하는 단계적 확대 플랜을 정의합니다. | IBM |
|인프라, 플랫폼 및 지원 계약에 서명 | 환경에 대한 재무 조건을 포함하여 구독 계약에 서명합니다. 네트워크 및 보안 모니터링 계약에 서명합니다. 지원 구독에 서명합니다. | 고객 |
|환경 조달 | 계산 자원, 네트워크 및 스토리지를 조달합니다. 환경의 인프라 요구사항에 대한 자세한 정보는 [Local 인프라 요구사항](../local/index.html#localinfra)을 참조하십시오. | 고객 |
|VPN 솔루션 설치 | 양방향 VPN 솔루션을 설치합니다. | IBM |
|패브릭, 애플리케이션, 모니터링 및 관리 컴포넌트 설치 | 패브릭 컴포넌트(예: BOSH Director, 클라우드 제어기, 상태 관리자, 메시징, 라우터, DEA 및 서비스 제공자)와, 단계적 확대 및 문제점 발견 플랜에 정의된 모니터링 컴포넌트를 설치하고 구성하며 확인합니다. | IBM |
|보안 컴포넌트 설치 및 구성 | 모니터링 및 단계적 확대 플랜에 연결된 보안 컴포넌트(예: IBM QRadar, 신임 정보 저장소, 침입 방지 시스템, IBM BigFix, IBM Security Privileged Identity Management)를 설치하고 구성합니다. | IBM |
|로그인 서버 구성 | 기업 LDAP에 사용할 로그인 서버를 구성합니다. | IBM |
|사용자 정의 컴포넌트 설치 및 구성 |  	{{site.data.keyword.Bluemix_notm}} 제품 및 서비스 범위의 외부에 상주하는 사용자 정의 컴포넌트를 설치하고 구성합니다. | 고객 |
|{{site.data.keyword.Bluemix_notm}} 파이프라인 연결 | {{site.data.keyword.Bluemix_notm}} 지속적 통합 및 지속적 딜리버리 파이프라인을 IBM 저장소에 연결합니다. | IBM |
|외부 솔루션 컴포넌트 사용자 정의 | 재해 복구 시나리오에 대비해 로드 밸런서를 사용자 정의합니다. | 고객 |
|보안, 규제 준수 및 감사 제어를 위한 상태 추적  | 모든 도구와 프로세스가 식별된 규제 준수 수준에 도달하는 시점까지 상태를 추적합니다. | 고객 |
|실제 인프라 검토 | 위협에 대비한 솔루션 컴포넌트를 호스팅하는 실제 구내와 데이터 센터를 보호하기 위한 보안 제어를 검토합니다. | 고객 |
|모니터링 소프트웨어 검사 | 단계적 확대 및 문제점 판별 플랜에 정의된 대로 모니터링 및 관리 컴포넌트를 검사합니다. | 고객 |
|OS 검사 | 운영 체제 이미지가 규제 준수 표준에 부합하는지 검사합니다. IBM이 OS 이미지에 대한 액세스 권한을 제공합니다. | IBM 및 고객 책임 공유 |

다음은 진행 단계입니다. 진행 단계에서 사용자와 IBM 사이의 지속적 협력 관계를 기술합니다. 이 단계의 1차 목표에는 다음이 포함됩니다.

- 용량을 검토하여 필요한 조정을 합니다.
- 유지보수 및 플랫폼 개선 방안을 검토합니다.
- 문제점 해결 및 근본 원인 분석을 위한 활동을 조정합니다.

*표 2. 진행 단계 태스크*

| **태스크** | **태스크 세부사항** | **책임자** |
|----------|------------------|-----------------------|
|주간 용량 보고서 검토 | 주간 용량 보고서를 검토하고 필요 시 정정 조치를 수행합니다. | 고객 |
|월별 예측 작성 | 정보를 수집하여 용량 및 사용량에 대한 월별 예측을 작성합니다. | IBM 및 고객 책임 공유 |
|용량 예측 검토 | 용량 예측은 예상되는 앱의 새 배치뿐 아니라 용량에 영향을 줄 수 있는 외부 이벤트와 관련되므로 이를 검토합니다. IBM과 함께 예측 및 플랜을 검토합니다. | IBM 및 고객 책임 공유 |
|용량 조정 |  변경이 필요할 때 용량을 추가하거나 제거합니다. | IBM |
|다음 업데이트 및 유지보수 공개 | IBM 컴포넌트의 필수 유지보수를 위한 문서를 작성합니다. | IBM |
|유지보수 수행 | IBM과 함께 30일 창 내에서 필수 유지보수를 스케줄합니다. 사용자는 30일 창에서 작업이 없는 날짜를 제공하고 IBM은 이에 따라 유지보수 일정을 스케줄합니다. | IBM 및 고객 책임 공유 |
|프로비저닝 장애 해결 | 카탈로그에 배치된 고객 작성 서비스의 프로비지닝 장애(발생하는 경우)를 수정합니다. | IBM |
|네트워크 및 IP 스캔 수행 | 네트워크 및 IP 스캔을 일별 및 월별로 수행합니다. | IBM 및 고객 책임 공유 |
|감사 로그에 대한 액세스 권한 제공 | 모든 보안 및 관리 감사 로그에 대한 액세스 권한을 제공합니다.   | IBM 및 고객 책임 공유 |
|테스트 수행 | 운영 테스트 및 써드파티 침투 테스트에 대해 정기적 키 제어를 수행합니다. | IBM 및 고객 책임 공유 |
|상태 보고, 감사 조정 및 규제 준수 미팅  | 규제 준수 검토 상태 미팅에서 상태 보고, 외부 감사 조정 및 표시를 완료합니다. | IBM |
|채용 및 비즈니스 수요 검증 | 고객 환경에 액세스하는 IBM 담당자를 위해 분기별 채용 검증 및 지속적 비즈니스 수요에 대한 검증을 완료합니다. | IBM |
|보안 취약점 해결 | 플랫폼에서 보고된 보안 취약점을 해결합니다. | IBM |

최종 완료 단계는 사용자와 IBM {{site.data.keyword.Bluemix_notm}} 사이의 관계 종료를 나타냅니다. 이 단계의 1차 태스크에는 다음이 포함됩니다.

* 재무 계약 종료
* 모든 네트워크 연결 제거
* 인프라 재사용

*표 3. 완료 단계 태스크*

| **태스크** | **태스크 세부사항** | **책임자** |
|----------|------------------|-----------------------|
|재무 계약 종료 | 재무 계약의 종료를 논의하고 합의합니다. | IBM 및 고객 책임 공유 |
|환경에 대한 커미션 해지 | 환경에 대한 액세스 권한과 신임 정보를 종료합니다. | IBM 및 고객 책임 공유 |
|릴레이 종료 | 릴레이 연결을 종료합니다. | IBM |
|인프라 재사용 | 회사 가이드라인에 따라 인프라를 재사용합니다. | 고객 |

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
<p><strong>참고:</strong> 다중 데이터 저장소를 사용하는 경우 각각에 대해 동일한 접두부를 사용하십시오.</p>
</dd>
<dt>**고가용성**</dt>
<dd>
단일 노드 장애를 지원하려면 n+1 ESXi가 있어야 합니다. 예를 들어, 각각 16x 코어를 의미하는 두 ESXi가 사용되는 경우, 세 번째가 필요합니다.
<p><strong>참고:</strong> 고객 VMware 관리자는 클러스터에서 고가용성 장애 복구를 엄격하게 적용하여 자원을 보장하기로 결정할 수 있습니다.</p>
</dd>
<dt>**네트워크**</dt>
<dd>
권장 요구사항에는 동일한 서브넷에서 아웃바운드 인터넷 액세스 권한을 갖는 7개의 고객 네트워크 IP 주소를 포함하는 고객 액세스 가능 포트 그룹이 포함됩니다. 2개 포트는 도입/인식(Inception) 가상 머신에 사용되고, 3개 포트는 도메인에 사용되는 가상 IP 주소이고, 나머지 2개는 DataPowers를 위한 공용 IP 주소입니다. 그런 다음 {{site.data.keyword.Bluemix_notm}} Local에 사용되는 ESXi 사이에만 두 번째 개인용 VLAN을 정의합니다. 이 VLAN은 VMware에서 포트 그룹으로 표시됩니다. {{site.data.keyword.Bluemix_notm}} Local은
이를 더 안전하고 라우팅 문제를 피하는 데 도움이 되는 개인용 서브넷으로 사용합니다.
<br />
<p>사용하는 포트는 다음과 같습니다.</p>
<ul>
<li>릴레이 연결의 경우 포트 443
<p>**참고**: OpenVPN 대신 IPSec 터널을 사용하도록 선택하는 경우, 이 연결을 위한 고객 포트를 엽니다.</p></li>
<li>LDAP 또는 Active Directory 연결을 위한 포트 389 또는 SSL 636</li>
</ul>
<p>**참고**: IBM이 네트워크 연결의 끊김 여부를 확인할 수 있습니다. 네트워크 연결이 끊기면 IBM에서 사용자에게 연락하여 네트워크 전문가와 함께 문제를 해결합니다.</p>
</dd>
</dl>

###vCenter 서버 구성
다음 버전, 데이터 센터, 자원 풀 및 데이터 저장소 요구사항을 검토하십시오.
<dl>
<dt>**지원되는 VMware 버전**</dt>
<dd>vCenter 및 ESXi 5.1 및 5.5</dd>
<dt>**지원되는 VMware 유형**</dt>
<dd>vSphere Enterprise<br />
분산 가상 스위치를 사용하려는 경우 vSphere Enterprise 플러스</dd>
<dt>**데이터 센터**</dt>
<dd>데이터 센터가 존재하지 않는 경우, 작성하십시오.</dd>
<dt>**데이터 센터 폴더**</dt>
<dd>데이터 센터에서 전파된 관리자 액세스 권한을 부여하지 않으려면 클러스터와 동일한 이름으로 VM 폴더를 작성하십시오.</dd>
<dt>**클러스터**</dt>
<dd>특히 {{site.data.keyword.Bluemix_notm}} Local 사용을 위해
클러스터를 작성하십시오. 클러스터 이름의 예는 `bluemix`입니다.</dd>
<dt>**자원 풀**</dt>
<dd>{{site.data.keyword.Bluemix_notm}} Local 클러스터 아래에 자원 풀을 작성하십시오. 자원 풀 이름의 예는
`local`입니다.</dd>
</dt>**데이터 저장소**</dt>
<dd>{{site.data.keyword.Bluemix_notm}}의 초기 배치에는 7.5TB가 필요합니다.<br />
<br />
**참고**: 둘 이상의 데이터 저장소를 사용하는 경우 각 데이터 저장소는 동일한 접두부로 시작해야 합니다. 접두부가 동일한 여러 데이터 저장소 이름의 예는
`bluemix_datastore_01` 및 `bluemix_datastore_02`입니다.</dd>
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
<dd>역할을 읽기 전용 및 전파되지 않음으로 설정하십시오.<br />
<br />
**참고**: 이 역할은 특정 디스크 오퍼레이션에 대한 태스크 상태를 검색하는 데 필요합니다.</dd>
<dt>**데이터 센터**</dt>
<dd>"{{site.data.keyword.Bluemix_notm}}" 역할을 작성하고 **하위 레벨 파일 오퍼레이션** 및 **가상 머신 파일 업데이트**를 포함하여 **데이터 저장소**에 대한 권한을 부여하십시오.<br />
<br />
**참고**: 이 역할은 데이터 저장소에 대한 파일 포스트를 지원하는 데 필요합니다.</dd>
<dt>**클러스터**</dt>
<dd>역할을 관리자 및 전파됨으로 설정하십시오.</dd>
<dt>**데이터 저장소**</dt>
<dd>각 {{site.data.keyword.Bluemix_notm}} 데이터 저장소에 대해
역할을 관리자 및 전파됨으로 설정하십시오.</dd>
<dt>**네트워크**</dt>
<dd>공용 및 개인용 포트 그룹을 관리자 역할, 전파되지 않음으로 설정하십시오.</dd>
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
IBM은 각각의 유지보수 창에 대해 계획된 변경사항의 브로드캐스트 메시지를 이메일, 전화 또는 기타 방법을 통해 전송합니다.<br />
<br />
**중요**: 유지보수 기간 중에는 일부 서비스를 사용하지 못할 수도 있습니다.</dd>

<dt>**월별 변경 창**</dt>
<dd>월별 유지보수 창은 21일 기간 내에 사용자와 IBM 간 조정을 기반으로 적용됩니다. 사용자는 작동하지 않을 수 있는 21일 기간 내에 특정 날짜 또는 시간을 IBM에 제공할 수 있습니다. IBM은 해당 시간을 중심으로 업데이트를 스케줄하기 위해 시도합니다. 요청을 기반으로 IBM은 사용자에게 스케줄된 유지보수 창을 전달합니다. 월별 변경 창은 실행 중인 Bluemix Local 환경에 영향을 미칠 것으로 예상되지 않습니다.<br />
<br />
**참고**: 업데이트할 특정 시간을 요청하지 않는 경우 유지보수는 창의 마지막에 자동으로 적용됩니다.<br />
<br />
**관리 > 시스템 정보**로 이동하여 보류 중인 업데이트를 확인하고 사용 불가능한 날짜를 설정하며 업데이트를 승인하십시오. 알림 및 보류 중인 업데이트 스케줄링에 대한 자세한 정보는 <a href="../admin/index.html#oc_system">시스템 정보 보기</a>를 참조하십시오.</dd>

<dt>**기타**</dt>
<dd>IBM은 서비스(특히 Bluemix 환경, 런타임 및 서비스의 가용성)에 영향을 줄 수 있는 모든 유지보수를 표준 및 월간 창으로 제한하고자 합니다. 기타 변경 창은 환경 관리를 위한 예외 기반으로 사용될 수 있습니다. IBM은 그러한 변경 창 동안에 사용자에게 미치는 영향을 최소화하기 위해 합리적인 노력을 기울일 것이며 이에 대해 사전에 알려드릴 것입니다.</dd>
</dl>

로컬 인스턴스의 유지보수를 설정하려면 IBM 전용 계정 담당자와 함께 작업하여 표준 유지보수에 대해 합의된 기간을 식별하십시오.

유지보수 업데이트 후 문제가 보고되는 경우 IBM이 업데이트를 롤백할 수 있도록 IBM 담당자와 협의합니다. 계약 시, IBM은 업데이트를 롤백하여 환경을 이전 단계로 복원합니다.

## 재해 복구
{: #dr}

{{site.data.keyword.Bluemix_short}} Public은 지속적으로 혁신 가능한 플랫폼을 제공합니다. 다중 고장 안전 조치로 사용자 조직, 공간 및 앱은 항상 사용 가능 상태를 유지합니다. 지리적으로 여러 위치에 앱을 배치하면 불시의 동시 다발성 하드웨어 또는 소프트웨어 컴포넌트 유실, 전체 데이터 센터의 유실로부터 보호되어 지속적으로 가용성이 보장되므로, 지리적으로 한 위치에서 자연 재해가 발생하여도 대체 위치의 Distributed {{site.data.keyword.Bluemix_notm}} Public 앱 인스턴스는 사용 가능합니다.
{: shortdesc}

{{site.data.keyword.Bluemix_short}} Local의 재해 복구는 사용자 앱의 지속적 가용성, 플랫폼의 내재적 고가용성, 장애 시 인스턴스 복구 능력 등을 통해 가능해집니다. 여러 지역에 앱을 배치하여 앱의 지속적 가용성을 보장하는 것은 사용자의 책임입니다. 고가용성은 Cloud Foundry 및 기타 컴포넌트에 포함된 기술을 통해 플랫폼 레벨에서 빌드됩니다. 또한 IBM과 협력하여 언제든 인스턴스 복원이 필요한 시점에 데이터를 적절히 백업할 수도 있습니다.

### {{site.data.keyword.Bluemix_notm}} Local에 대한 지속적인 가용성 사용
{: #enabling}

기본적으로 {{site.data.keyword.Bluemix_notm}} Public은 지리적으로 여러 위치에 배치됩니다. 그러나 글로벌하게 분산된 {{site.data.keyword.Bluemix_notm}} Local 인스턴스에 대해서는 다음을 수행해야 합니다.

* 개발자는 수동 또는 자동화된 프로세스를 통해 하나 이상의 지역에 앱을 배치해야 합니다. 자연 재해가 두 위치에 모두 영향을 줄 수 없도록, 선택된 지역은 200km 이상 떨어져 있어야 합니다.
* 둘 이상의 서로 다른 지역에 있는 앱을 가리키도록 글로벌 로드 밸런서(예: Akamai 또는 Dyn)를 구성하십시오.

**참고**: 모든 {{site.data.keyword.Bluemix_notm}} 서비스가 지역 분산 배포를 지원하는 것은 아닙니다. 앱을 생성할 때 지역 분산을 원하는 경우 해당 애플리케이션에서 사용하는 서비스가 데이터 동기화를 핵심 기능으로 가지고 있는지도 확인해야 합니다.

#### {{site.data.keyword.Bluemix_notm}} Local 앱을 여러 지리적 위치에 배치
{: #deploying}

두 번째 또는 더 많은 위치에 배치하려면 1차 지리적 위치에서 했던 것과 유사한 프로세스를 따라야 합니다.

1. 새 로컬 환경이 애플리케이션의 추가 인스턴스를 호스팅할 수 있게 하십시오. 새 환경을 작성하려면 IBM 영업부에 문의하여 프로세스를 시작하십시오. 로컬 인스턴스 설정에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} Local 설정](../local/index.html#setuplocal)을 참조하십시오. 각 환경에 액세스하려면 별도로 로그인해야 합니다. 가용성을 보장하려면 호스팅되는 각 환경의 실제 위치가 1차 위치와 200km 이상 떨어져 있어야 합니다.
2. 배치된 새 앱이 호스팅되는 고유 도메인 이름을 확보하십시오. 예를 들어, 원래 도메인이 *mycompany.east.bluemix.net*이면 새 도메인(예: *mycompany.west.bluemix.net*)을 사용하여 새 로컬 환경을 작성하고 새 도메인에 배치할 수 있습니다.
3. 원본 앱을 배치할 때마다 새 위치에도 배치하십시오. 배치에 대한 자세한 정보는 [앱 업로드](../starters/upload_app.html)를 참조하십시오.


#### {{site.data.keyword.Bluemix_notm}} Local에 대한 글로벌 로드 밸런서 사용
{: #glb}

글로벌 로드 밸런서는 지속적 가용성을 보장하여 재해 복구에 필요할 뿐만 아니라 여러 가지 추가적 이점도 있습니다.

* 기본적으로 사용자를 가장 인접한 지역의 {{site.data.keyword.Bluemix_notm}}에 라우트합니다.
* 성능에 기반하여 라우트합니다.
* 트래픽 비율을 새 애플리케이션 버전에 맞게 선택적으로 지정합니다.
* 지역 상태 점검을 토대로 사이트 장애 복구를 제공합니다.
* 애플리케이션 상태 점검을 토대로 사이트 장애 복구를 제공합니다.
* 엔드포인트 사이에서 가중 라우팅을 사용합니다.

Akamai 또는 Dyn과 같은 글로벌 로드 밸런서를 선택할 수 있습니다. Akamai를 글로벌 로드 밸런서로 사용하기 위한 자세한 정보는 [글로벌 트래픽 관리](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp){: new_window}를 참조하십시오. Dyn을 글로벌 로드 밸런서로 사용하기 위한 자세한 정보는 [비즈니스에서 글로벌 로드 밸런싱을 클라우드에 적용하는 4가지 이유](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}를 참조하십시오.

### 고가용성
{: #ha}

지속적 가용성 외에도, {{site.data.keyword.Bluemix_notm}}에서는 Cloud Foundry, Docker 및 기타 컴포넌트에 빌드된 기술을 사용하여 플랫폼 사이에서 고가용성을 제공합니다.

이 기술에는 다음이 포함됩니다.

<dl>
<dt>Cloud Foundry의 확장성</dt>
<dd>Cloud Foundry <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">DEA(Droplet Execution Agent)</a>는 내부에서 실행되는 앱에 대한 상태 점검을 수행합니다. 앱이나 DEA 자체에 문제가 있는 경우 문제 해결을 위해 앱의 추가 인스턴스를 대체 DEA에 배치합니다. 자세한 정보는 <a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">고가용성 및 중복성을 갖도록 CF 구성</a>의 내용을 참조하십시오.
</dd>
<dt>메타데이터 백업</dt>
<dd>메타데이터는 2차 위치(일반적으로 사내 구축형 가상 머신)에 백업됩니다. 가능할 경우 백업은 200km 이상 떨어진 사용자 환경에 복제해야 합니다.</dd>
</dl>

##로컬 인스턴스 복원
{: #restorelocal}

{{site.data.keyword.Bluemix_notm}} Local 설정, 메타데이터 및 구성은 환경에서 예상치 못한 가동 중단에 대처하기 위해 주기적으로 백업됩니다. 사용자에게 백업 책임이 있는 데이터에는 애플리케이션 데이터, 클라우드 데이터베이스 서비스 데이터 및 오브젝트 저장소가 있습니다.

시스템 메타데이터 및 구성을 포함하는 데이터 백업의 일부로서 IBM은 다음 태스크를 완료합니다.

<ul>
<li>모든 백업 사본의 암호화 및 암호화 키 관리</li>
<li>백업 활동의 모니터 및 관리</li>
<li>암호화된 백업 파일 제공</li>
<li>요청된 데이터의 복원</li>
<li>백업 및 수정사항 관리 운영 간의 스케줄링 충돌 관리</li>
</ul>

개인 데이터 보호가 중요하므로 파일이 데이터 센터 외부로 노출되지 않도록 백업 파일 관리를 처리할 때 여러분의 협력을 필요로 합니다. 특히, 다음 태스크를 완료해 주시기 바랍니다.

<ul>
<li>관리하는 다른 백업 데이터에 하듯이 암호화된 백업 데이터 사본을 오프사이트로 이동합니다.</li>
<li>복원이 필요한 경우 백업 파일을 IBM 운영자에게 제공합니다.</li>
</ul>

# rellinks
## 일반
* [탐색: {{site.data.keyword.Bluemix_notm}} Local](http://www.ibm.com/cloud-computing/bluemix/hybrid/local/)
* [{{site.data.keyword.Bluemix_notm}} Local 및 {{site.data.keyword.Bluemix_notm}} Dedicated 관리](../admin/index.html#mng)
* [지원 문의](../troubleshoot/getting_customer_support.html#bluemix_support)
