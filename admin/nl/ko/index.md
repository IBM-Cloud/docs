{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} 관리
{: #administer}
*마지막 업데이트 날짜: 2016년 1월 20일*

**계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg)을 클릭하여 조직, 영역 및 지정된 사용자를 관리하고 **조직 관리**를 선택하십시오. {{site.data.keyword.Bluemix_notm}} Local 또는 {{site.data.keyword.Bluemix_notm}} Dedicated 사용자인 경우, 로컬 또는 전용 인스턴스 관리에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} Local 및 {{site.data.keyword.Bluemix_notm}} Dedicated 관리](index.html#mng)를 참조하십시오. {:shortdesc}

##계정 관리
{: #mngacct}

{{site.data.keyword.Bluemix}} Public에서 사용자 인터페이스의 대시보드를 통해 사용자 액세스 권한을 비롯한 모든 조직 및 영역을 관리할 수 있습니다. 사용량 및 청구 정보를 모니터링할 수도 있습니다. {:shortdesc}

###조직 및 영역
{: #orgsandspaces}

조직 관리자 또는 계정 소유자는 조직 관리 페이지에서 사용자 액세스 권한을 비롯한 조직 또는 영역 설정을 확인하고 관리할 수 있습니다. 조직 관리 페이지를 열려면 **계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg)을 클릭하고 **조직 관리**를 선택하십시오.

####조직

조직은 다음과 같은 항목으로 정의됩니다. 

<dl>
<dt>사용자</dt>
<dd>조직과 영역에 대한 기본 권한이 있는 역할입니다. 먼저
관리자가 조직에 지정되어 있어야 조직 내의 영역에 대한 다른
권한을 부여받을 수 있습니다. 자세한 정보는
[사용자 및
역할](index.html#userroles)을 참조하십시오.</dd>
<dt>도메인</dt>
<dd>조직에 할당된 인터넷 라우트를 제공합니다. 라우트는 하위 도메인과 도메인으로
구성됩니다. 하위 도메인은 보통 애플리케이션 이름입니다. 도메인은 애플리케이션에 대해 등록한 시스템 도메인 또는 사용자 정의 도메인일 수 있습니다.<br/>
<p>**참고**: 사용자 정의 도메인을 추가하는 경우, 사용자 정의 도메인을 분석하여 {{site.data.keyword.Bluemix_notm}} 시스템 도메인을 가리키도록 DNS 서버를 구성해야 합니다. 이런 방법으로
{{site.data.keyword.Bluemix_notm}}에서 사용자 정의 도메인에
대한 요청을 수신하면 이 요청을 적절하게 애플리케이션에 전달할 수 있습니다. </p></dd>
<dt>할당량</dt>
<dd>조직에서 사용하기 위해 할당할 수 있는 서비스의
수와 메모리 양을 비롯한 조직의 자원 한계를
나타냅니다. 조직이 작성되면 할당량이
지정됩니다. 조직의 영역에 있는 모든 애플리케이션이나
서비스가 할당량의 사용에 영향을 미칩니다. 종량과금제 또는 구독 요금제를
사용하면 조직의 요구사항이 변경됨에 따라 Cloud Foundry 애플리케이션과
컨테이너의 할당량을 조정할 수 있습니다. </dd>
</dl>

{{site.data.keyword.Bluemix_notm}}에서는
조직을 사용하여 사용자 간 협업을 지원하고, 다음과 같은 방식으로 프로젝트 자원의
논리적 그룹화를 손쉽게 수행할 수 있습니다. 

<ul>
<li>조직에서 영역, 애플리케이션, 서비스, 도메인, 라우트, 사용자를 함께 그룹화할
수 있습니다. </li>
<li>사용자별로 영역 및 조직에 대한 액세스를 관리할 수 있습니다.
</li>
</ul>

조직을 작성하는 경우 조직 이름은 {{site.data.keyword.Bluemix_notm}}에서
고유해야 합니다. 조직을 작성한 사용자에게 자동으로 *조직 관리자* 권한이 지정되므로, 조직 이름 편집, 조직 삭제 및 조직에 영역 작성 등을 수행할 수 있습니다.

조직을 삭제하면 조직 내에 있는 영역, 애플리케이션 및
서비스도 모두 삭제됩니다. 

{{site.data.keyword.Bluemix_notm}}에서는
조직 및 조직 내의 영역에 사용자를 지정하여 프로젝트에 대한 협업을 지원합니다.
**사용자** 탭을 사용하여 조직의 사용자를 표시하고 관리할 수
있습니다. **사용자** 탭에서 **새 사용자 초대** 링크를 클릭하여 조직에 사용자를 초대할 수도 있습니다. 조직 내의 사용자에게 지정할 수 있는 권한은 다음과 같습니다. 

<ul>
<li>조직 사용자</li>
<li>조직 관리자</li>
<li>조직의 청구 관리자</li>
<li>조직 감사자</li>
</ul>

####영역

조직 내에서는 영역을 사용하여 애플리케이션, 서비스
및 사용자를 그룹화할 수 있습니다. 

조직에 사용자를 추가한 후에는
조직 내의 영역에 대한 권한을 사용자에게 부여할 수 있습니다. 조직과 마찬가지로,
영역의 경우도 사용자에게 지정할 수 있는 권한이 있습니다. 

<ul>
<li>영역 관리자</li>
<li>영역 개발자</li>
<li>영역 감사자</li>
</ul>

**참고**: 영역에서 사용자에게 적어도 하나의 권한이 지정되어 있어야 합니다. 

영역의 **도메인** 탭은 영역에 지정된
도메인의 읽기 전용 목록입니다. 시스템 도메인은 항상 영역에 사용할 수 있으며,
사용자 정의 도메인도 영역에 할당할 수 있습니다. 영역에 작성된 애플리케이션은
영역에 대해 나열된 도메인을 사용할 수 있습니다. 

###사용자 및 역할
{: #userroles}

계정 소유자는 조직 및 영역에 대한 모든 오퍼레이션을 수행합니다. 

####사용자 유형

계정의 구성원이거나
협업자일 수 있습니다.

<dl>
<dt>구성원</dt>
<dd>사용자가 {{site.data.keyword.Bluemix_notm}}
계정을 작성했거나 {{site.data.keyword.Bluemix_notm}}의
첫 경험으로 계정을 사용하도록 초대되어 이 초대를 통해 가입한 경우 사용자는
이 계정의 구성원입니다.</dd>
<dt>협업자</dt>
<dd>이전에 다른 계정으로 {{site.data.keyword.Bluemix_notm}}를
사용했지만 {{site.data.keyword.Bluemix_notm}}
계정을 사용하도록 초대되고 초대를 허용한 경우 사용자는 이 계정의
협업자입니다. </dd>
</dl>

####사용자 역할

조직이나 영역에서
다른 사용자 역할을 수행하도록 사용자에게 다음 권한이 지정될 수 있습니다.

<dl>
<dt>조직 관리자</dt>
<dd>조직 관리자에게 다음 권한이 있습니다.<ul>
<li>조직 내 영역 작성 또는 삭제</li>
<li>조직의 구성원 또는 계정 소유자이기도 한 경우
조직에 사용자 초대</li>
<li>조직에 이미 있는 기존 사용자 관리</li>
<li>조직의 도메인 관리</li>
</ul>
<p>**참고**: 협업자 유형의 사용자이고 이전에 다른 계정으로 {{site.data.keyword.Bluemix_notm}}를 사용한 적이 있으면 조직 관리자 역할이 지정되어도 조직에 사용자를 초대할 수 없습니다. 사용자를 초대하려면 사용자 유형이
구성원이어야 합니다. 이 문제점에 대한 해결 방법은
<a href="../troubleshoot/index.html#ts_adduser">조직에
사용자를 추가할 수 없음</a>을 참조하십시오. </p>
</dd>
<dt>청구 관리자</dt>
<dd>청구 관리자는 조직의 런타임 및 서비스 사용량 정보를
볼 권한이 있습니다. </dd>
<dt>조직 감사자</dt>
<dd>조직 감사자는 영역에 있는 애플리케이션 및 서비스
컨텐츠를 볼 권한이 있습니다.</dd>
<dt>영역 관리자</dt>
<dd>영역 관리자는 다음 권한이 있습니다.
<ul>
<li>영역에 사용자 추가 및 사용자 관리</li>
<li>영역에 대한 기능 사용 설정</li>
</ul>
</dd>
<dt>영역 개발자</dt>
<dd>영역 개발자는 다음 권한이 있습니다.<ul>
<li>영역 내에서 애플리케이션 및 서비스 작성, 삭제 및 관리</li>
<li>영역 내에서 로그에 대한 액세스</li>
</ul>
</dd>
<dt>영역 감사자</dt>
<dd>영역 감시자는 영역에 대한 모든 정보(예: 애플리케이션 및
서비스, 설정, 보고서, 로그에 대한 정보)에 대한 읽기 전용 액세스 권한이
있습니다. </dd>
</dl>

###조직 관리
{: #orgmng}

조직 관리자 또는 계정 소유자는 조직을
관리할 수 있습니다. 관리 태스크에는 조직 작성, 조직 이름 바꾸기, 영역 작성, 영역에 사용자 초대, 사용자 역할 변경 및 기존 조직 삭제가 포함됩니다.

<ul>
<li>조직 작성<p>지불 계정을 가진 사용자만
조직을 작성할 수 있습니다. 지불 계정을 사용하여
다음 단계에 따라 조직을 작성할 수 있습니다.</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} 대시보드로 이동하여 **계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg)을 클릭하고 **조직 관리**를 선택하십시오.</li>
<li>**조직 작성**을 클릭하고
프롬프트에 따라 조직을 작성하십시오.</li>
</ol>
</li>
<li>조직 이름 바꾸기<p>조직의 이름을 바꾸려면
다음 단계를 수행하십시오.</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} 대시보드로 이동하여 **계정 및 지원** 아이콘 ![계정 및 지원](images/account_support.svg)을 클릭하고 **조직 관리**를 선택하십시오.</li>
<li>이름을 바꿀 조직을 선택하십시오.</li>
<li>**조직** 필드에 새 이름을 입력하고
**저장**을 클릭하십시오.</li>
</ol>
</li>
<li>구성원 나열<p>사용자 조직이나 영역의 구성원을 나열하려면 다음 단계를 수행하십시오. </p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} 대시보드로 이동하여 **계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg)을 클릭하고 **조직 관리**를 선택하십시오. **사용자** 탭에서 사용자 조직의 구성원과 이들의 역할을 확인할 수 있습니다. </li>
<li>이 영역의 구성원과 이들의 역할을 보려면 조직의 영역 이름을 클릭하십시오. </li>
</ol>
</li>
<li>영역 작성<p>조직에서 영역을 작성할 수 있습니다.
예를 들어, *dev* 영역은 개발 환경으로,
*test* 영역은 테스트 환경으로, *production*
영역은 프로덕션 환경으로 작성할 수 있습니다.
그런 다음 앱을 영역과 연관시킵니다. 영역을 작성하려면
다음 단계를 수행하십시오.</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} 대시보드로 이동하여 **계정 및 지원** 아이콘 ![계정 및 지원](images/account_support.svg)을 클릭하고 **조직 관리**를 선택하십시오.</li>
<li>조직 이름 다음의 **영역 작성**을 클릭하고 지시에 따라 영역을 작성하십시오.</li>
</ol>
</li>
<li>영역에 사용자 초대<p>조직에 사용자를 협업자로
초대할 수 있습니다. 조직의 사용자를 다른 영역에
추가할 수도 있습니다. 사용자는 자신에게 추가된 영역에만
액세스할 수 있습니다. 사용자를 영역에 추가하려면
다음 단계를 수행하십시오.</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} 대시보드로 이동하여 **계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg)을 클릭하고 **조직 관리**를 선택하십시오. 그런 다음 조직에서 **사용자 추가**를 클릭하고 지시에 따라 사용자를 조직에 추가하십시오.</li>
<li>사용자를 영역에 추가하십시오. 탐색 분할창에서 영역을 선택하고 **사용자 추가**를 클릭한 다음 지시에 따라 사용자를 영역에 추가하십시오.</li>
</ol>
</li>
<li>사용자 역할 변경
<p>사용자 역할을 변경하려면 다음 단계를 수행하십시오.</p>
<ol>
<li>{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스에서 **계정 및 지원** 아이콘 ![계정 및 지원](images/account_support.svg)을 클릭하고 **조직 관리**를 선택하십시오.</li>
<li>**사용자** 탭에서 **관리자**, **청구 관리자** 또는 **감사자** 선택란을 선택하여 조직에서 사용자의 역할을 변경하십시오. 또는 탐색 분할창에서 영역을 선택하고 **사용자** 탭에서 **관리자**, **개발자** 또는 **감사자** 선택란을 선택하여 영역에서 사용자의 역할을 변경하십시오. </li>
<li>**저장**을 클릭하십시오.</li>
</ol>
</li>
<li>기존 조직 삭제<p>조직을 삭제하려면 {{site.data.keyword.Bluemix_notm}} 등록 및 ID 지원에 문의하십시오.</p>
<p>**참고**: 삭제 오퍼레이션은 되돌릴 수 없습니다. 조직과 연관된 애플리케이션 및
서비스가 모두 손실됩니다.</p>
</li>
</ul>

## {{site.data.keyword.Bluemix_notm}} Local 및 {{site.data.keyword.Bluemix_notm}} Dedicated 관리
{: #mng}

{{site.data.keyword.Bluemix_notm}} Local 또는 {{site.data.keyword.Bluemix_notm}} Dedicated에 대한 관리자 액세스 권한이 있으면 **관리** 페이지로 이동하여 자원을 관리하고, 할당 사용량을 모니터링하고, 사용자 권한을 관리하고, 업그레이드 알림을 스케줄링하고, 보안 보고서 및 로그를 확인하는 등 다양한 작업을 수행할 수 있습니다. 조직을 관리하려면 영역을 작성하고 사용자 역할 및 권한을 설정합니다. [조직 관리](index.html#orgmng)를 참조하십시오.
{:shortdesc}

*표 1. {{site.data.keyword.Bluemix_notm}} Local 또는 Dedicated 인스턴스* 관리를 위한 관리 태스크

| 수행할 수 있는 작업 | 세부사항 |    
|----------------|---------|
|시스템 사용량 모니터링 | **관리 &gt; 사용량**을 클릭하십시오. 시스템 정보를 확인하고, CPU 사용량을 모니터링하고, 사용량을 계획하여 기업에 가장 최선의 결정을 내리십시오.|
|카탈로그 관리 | **관리 &gt; 카탈로그 관리**를 클릭하십시오. 사용자에게 표시되는 서비스를 관리하십시오.|
|조직 관리 | **관리 &gt; 조직 관리**를 클릭하십시오. 조직을 작성하고, 조직의 할당량을 모니터링하고, 요구사항에 따라 신속하게 의사결정을 내리십시오.|
|영역 작성 및 사용자 역할 지정 | **계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg)을 클릭하고 **조직 관리**를 선택하십시오. 사용자 조직 내에 영역을 작성하십시오. 사용자를 추가하고 조직과 영역을 사용자에게 지정하십시오. |
|관리자 권한 관리 | **관리 &gt; 사용자 관리**를 클릭하십시오. 사용자를 추가하거나 제거하고, 사용자 권한을 조정하십시오. |
|보고서 및 로그 검토 | **관리 &gt; 보고서 및 로그**를 클릭하십시오. 사용자 인스턴스와 관련된 보안 보고서 및 감사 로그를 검토하십시오.|
|시스템 정보 보기 | **관리 &gt; 시스템 정보**를 클릭하십시오. 보류된 업데이트, 인스턴스의 이름 및 버전, 지역, API URL, CLI URL, LDAP 구성 세부사항, 그룹 및 사용자 맵핑, 통계 및 공유 도메인과 같은 시스템 정보를 확인하십시오.  |

### 시스템 정보 보기
{: #oc_system}

시스템 정보를 보려면 **관리 &gt; 시스템 정보**를 클릭하십시오.

보류 중인 업데이트, 일반 시스템 정보 및 LDAP 구성 세부사항에 대한
다양한 섹션을 펼치고 볼 수 있습니다. 

* 업데이트 섹션에서 사용자 파트에서 조치가 필요한
보류 중인 업데이트를 볼 수 있습니다. 또한 달력 앱에 스케줄된 업데이트를 가져오기 위해
달력 링크를 사용하여 업데이트를 쉽게 추적할 수도 있습니다.

<ol>
<li>특정 업데이트에 대한 조치를 취하려면 다음 단계를 완료하십시오. <ol type="a">
<li>모든 보류 중인 업데이트를 보려면 <strong>보류 중인 업데이트 <em>수</em></strong>를
클릭하십시오.</li>
<li>조치를 취하거나 업데이트 창, 스케줄된 날짜 또는 중단 상태가 포함된 업데이트의 세부사항을 보려면
업데이트를 선택하십시오.</li>
<li>업데이트 적용에 편리하지 않은 업데이트 창에서 특정 날짜를 설정하려면
<strong>SET UNAVAILABLE DATES</strong>를 클릭하십시오. 사용 불가능한 날짜를 설정하는 경우 IBM 승인 및
업데이트 스케줄은 사용자 선택사항을 기반으로 합니다. 업데이트가 승인되고 스케줄된 경우
알림을 수신합니다.</li>
<li>사용 불가능한 날짜가 포함되지 않은 경우 업데이트를 승인하려면 <strong>APPROVE</strong>를
클릭하십시오. 승인하면 스케줄된 업데이트 창 기간 중에 업데이트가 적용됩니다. IBM은 업데이트 배치 시작 및 종료 시
알림을 전송합니다.</li>
</ol>
</li>
<li>사용자 선택사항의 달력 앱에 스케줄된 업데이트를 가져오려면 다음 단계를 완료하십시오.
<ol type="a">
<li>달력 앱을 여십시오.</li>
<li>앱의 시스템 정보 페이지에 나열된 **달력 URL**을 붙여넣어 달력 업데이트를 가져오십시오. 또는 달력 URL을 클릭하여 달력 파일을 다운로드한 다음 `.ics` 파일을 사용하여 달력 앱에 가져오십시오.</li>
<li>신임 정보를 입력하십시오.</li>
<li>스케줄된 업데이트를 보십시오.</li>
</ol>
</li>
</ol>

* 일반 정보 섹션에서 다음 정보를 볼 수 있습니다. 
    * {{site.data.keyword.Bluemix_notm}} 빌드에 대한 기본 정보
    * 버전, URL 지역 및 CLI 문서에 대한 링크를 포함한 API 정보
    * 사용자의 시스템 및 서비스에 대한 공유 도메인 정보
    * 애플리케이션, 사용자 및 조직의 총 수에 대한 통계
* LDAP 구성 세부사항 섹션에서 LDAP 서버를 선택하면 사용자 및
그룹 맵핑에 대한 정보를 볼 수 있습니다. {{site.data.keyword.IBM}} WebID를 사용 중인 경우에는
LDAP 구성 세부사항 섹션에 표시됩니다. 

### 사용법 정보 보기
{: #oc_resource}

자원 정보를 보려면 **관리 &gt; 사용법**을 클릭하십시오.

자원 모니터링 섹션에서 다음 정보를
볼 수 있습니다.

* 사용된 메모리의 양(GB 단위) 및 디스크 공간의 양(GB 단위)과 같은 자원 사용 정보를 볼 수 있습니다. 모든 DEA(Droplet Execution Agent)에 대한
평균 CPU 사용량을 볼 수 있습니다. **CPU** 타일을 클릭하면 각 DEA에 대한 CPU 사용량을 볼 수 있습니다. 사용량이 가장 많은 DEA가
처음에 나열되며, 각각은 작업 및 IP 주소로 식별됩니다. CPU 사용량은 시스템 프로세스의 CPU 소비량,
사용자 프로세스의 CPU 소비량 및 대기 프로세스의 CPU 소비량을 포함하는 세 개의 카테고리로 구분됩니다. 
* 지난 날짜, 주 또는 월에 대해 송신 대역폭 및 수신 대역폭에 대한 네트워크 사용량 정보를 볼 수 있습니다. 표시되는 데이터는
공용 및 개인용 네트워크 둘 다의 입출력 트래픽 합계를 기반으로 합니다. 
* 지난 10분, 시간, 일에 대한 {{site.data.keyword.Bluemix_notm}}의 평균 응답 시간
* 지난 10분, 시간, 일에 대한 {{site.data.keyword.Bluemix_notm}}의 초당 평균 트랜잭션 수

### 보고서 보기
{: #oc_report}

{{site.data.keyword.Bluemix_notm}} 인스턴스에 대한 DataPower&trade;, 방화벽 및 로그인 감사 등의
보안 보고서 및 로그를 볼 수 있습니다.

보고서 및 로그를 보려면 **ADMINISTRATION &gt; REPORTS AND LOGS**를 클릭하십시오.

다음 옵션 중에서 선택하십시오.

* 필드에서 시작 및 종료 날짜를 선택하여 표시될 보고서 및 로그를 필터링할 수 있습니다.
* 탐색 분할창에서 다양한 보고서를 펼치고 볼 수 있습니다. 
* 보고서 및 로그의 콜렉션 내에서 검색할 수 있습니다. 검색은 보고서 이름과 보고서 및 로그에
포함된 텍스트 컨텐츠에 적용됩니다. 또한 **관리 이벤트**, **DataPower
보고서**, **방화벽** 및 **로그인 감사**를 기준으로 검색을 필터링할 수도 있습니다. 
* 보고서 또는 로그를 표시할 때 ![다운로드](images/icon_download.svg) 아이콘을
클릭하여 이를 다운로드할 수 있습니다.

### 상태 보기
{: #oc_status}

{{site.data.keyword.Bluemix_notm}} 상태 페이지를 사용하여 {{site.data.keyword.Bluemix_notm}} 인스턴스의 상태를 모니터링할 수 있습니다. 상태 페이지는 {{site.data.keyword.Bluemix_notm}}의 주요 서비스 및 {{site.data.keyword.Bluemix_notm}} 플랫폼에 영향을 미치는 주요 이벤트에 대한 알림 및 공지사항을 찾는 중심 위치입니다.

알림에 대한 RSS 피드를 구독하면 따로 확인할 필요가 없습니다. 상태 페이지 및 RSS 피드 설정에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 보기](../troubleshoot/getting_customer_support.html#status)를 참조하십시오.

### 카탈로그 관리
{: #oc_catalog}

{{site.data.keyword.Bluemix_notm}} 카탈로그에서 사용자에게 표시되는 {{site.data.keyword.Bluemix_notm}} 서비스 및 스타터를 관리할 수 있습니다.**관리 &gt; 카탈로그 관리**를 클릭하십시오. 

서비스 또는 스타터 타일을 선택하여 서비스 또는 스타터 플랜 가시성을 편집하십시오. 가시성을 편집하려면 다음 옵션 중에서 선택하십시오. 
* 숨겨진 서비스 또는 스타터를 표시하여 사용자가 카탈로그에서 볼 수 있도록 하려면
**모든 플랜 사용**을 선택하십시오. 
* 서비스 또는 스타터를 {{site.data.keyword.Bluemix_notm}} 카탈로그에서
사용자에게 숨기려면 **모든 플랜 사용 안함**을 선택하십시오. 
* 개별 플랜의 가시성을 제어하려면 플랜 이름을 선택한 후 드롭 다운 메뉴를 사용하여 **모든 조직에 대해 사용**,
**모든 조직에 대해 사용 안함** 또는 **특정 조직에 대해 플랜 사용**을 선택하십시오. 

### 조직 관리
{: #oc_organizations}

조직을 작성 및 삭제하고 조직에 관리자를 추가하고 할당 사용량을 모니터링하여 조직을 관리할 수 있습니다. 

**관리 &gt; 조직 관리**를 클릭하십시오. 

다양한 섹션을 펼치고 볼 수 있습니다. 조직에 대한 할당 플랜을 검토하고 관리할 수도 있습니다. 

* 새 조직을 작성하고 관리자를 추가하려면 <strong>조직 작성</strong>을 클릭하십시오. 조직의 이름을 입력한 후
관리자로 추가할 사용자의 이름 또는 이메일을 입력하십시오. 여러 이름을 입력하고 선택하여
둘 이상의 관리자를 추가할 수 있습니다. <strong>조직 작성</strong>을 클릭하여 변경사항을 저장하고 조직을 작성하십시오. 
* 할당량 모니터링 섹션에서 해당 섹션을 펼치고
다음 정보를 볼 수 있습니다. 
    * 환경 메모리 사용량. 이 섹션에는 전체 시스템 환경에 대한 메모리 사용량 세부사항이 있습니다.
차트는 사용된 시스템 메모리, 총 시스템 메모리, 사용된 할당량 및 할당된 총 할당량을
포함하는 정보를 제공합니다. 다음 용어 목록은 차트에 표시되는 메모리 사용량의 유형을 정의합니다. 
	<dl>
	<dt><strong>사용된 시스템 메모리</strong></dt>
	<dd>사용자 환경에서 사용된 실제 메모리입니다. </dd>
	<dt><strong>총 시스템 메모리</strong></dt>
	<dd>사용자 환경에서 사용 가능한 총 실제 메모리입니다. </dd>
	<dt><strong>배치된 할당량</strong></dt>
	<dd>모든 조직에서 배치된 모든 앱에 할당된 메모리의 합계입니다. 배치된
	할당량의 합계는 사용자 환경의 실제 총 시스템 메모리를 초과할 수 있습니다. 예를 들어, 총 시스템 메모리가 16GB이고 총 5개의 다른 조직에 각각 4GB의 메모리를 할당하는 경우,
총 할당량은 조직에 대해 할당된 총 시스템 메모리를 초과합니다. 그러나 많은 경우에 조직은 각 조직에 대해
개별적으로 할당된 총 할당량을 사용하지 않습니다. 또한 모든 조직이 동시에 총 메모리 할당량을 모두 사용하지는 않습니다. </dd>
	<dt><strong>총 할당량</strong></dt>
	<dd>모든 조직에 할당된 총 메모리입니다. </dd>
	</dl>
	* 조직 메모리 사용량. 이 섹션에는 조직 레벨에서 메모리 사용량의 세부사항이 있습니다. 총 할당 허용량 및
각 조직에 배치된 할당량을 볼 수 있습니다. 차트는 조직당 최상위 메모리 사용량을 기준으로 나열되는 정보를 제공하며,
기본적으로 메모리 사용량이 가장 많은 조직이 먼저 나열됩니다. **최상위 메모리 사용량** 및
**초과 메모리 할당**을 기준으로 정렬할 수 있습니다. 
	<dl>
	<dt><strong>최상위 메모리 사용량</strong></dt>
	<dd>메모리 사용량이 가장 많은 조직을 식별하려면 이 옵션을 사용하십시오. 최상위 메모리
	사용량을 기준으로 정렬하여 메모리 사용량이 가장 많은 조직을 식별하십시오. 목록은 배치된 할당량을 기준으로 정렬됩니다. </dd>
	<dt><strong>초과 메모리 할당</strong></dt>
	<dd>필요한 양보다 많은 할당량 플랜이 있는 조직을 식별하려면 이 옵션을 사용하십시오.
	초과 메모리 사용량을 기준으로 정렬하여 조직에 할당된 할당량에 대해 가장 적은 메모리를
사용하는 조직을 식별할 수 있습니다. </dd>
	</dl>
* 조직의 할당량 플랜을 변경하려면 조직 메모리 사용량 섹션의
차트에서 편집할 조직의 막대를 클릭하거나
조직 목록 섹션에서 해당 조직의 이름을 선택하십시오. 조직 편집 페이지에서 할당량 플랜을 변경하고
조직의 이름을 변경하고 관리자를 추가 또는
제거할 수 있습니다. 조직의 현재 사용량에 대해 충분하지 않은
할당량 플랜을 선택하는 경우에는 메시지를 수신합니다. 조직 편집 페이지에서 변경한 사항을 저장하려면
**저장**을 클릭하십시오. 
* 조직 목록 섹션에서 {{site.data.keyword.Bluemix_notm}} 환경에 있는
모든 조직을 볼 수 있습니다. 
	* 조직을 삭제하려면 조치 열에서 ![삭제](images/icon_trash.svg)를 클릭하십시오. 
	* 조직의 할당량 플랜을 보고 편집하려면 목록에서 해당 조직의 이름을 클릭하십시오. 
	* 조직의 이름을 편집하고 관리자를 추가 또는 제거하려면 목록에서 조직의 이름을 클릭하십시오. 

### 사용자 및 권한 관리
{: #oc_useradmin}

LDAP를 통해 회사의 사용자 레지스트리에서 {{site.data.keyword.Bluemix_notm}} 인스턴스에 사용자를 추가할 수 있습니다. 
사용자를 단독으로 또는 그룹으로 추가하고 사용자 권한을 볼 수 있습니다. 
`관리` 권한이 지정된 경우에는 다른 사용자에 대한 권한을 설정하고 관리할 수도 있습니다. **관리 &gt; 사용자 관리**를 클릭하십시오. 

사용자 관리 페이지에 로컬 또는 전용 인스턴스의 모든 사용자가 표시됩니다.
각 사용자의 권한이 표시되어 있습니다. 권한은 없음,
`관리`, `카탈로그`, `로그인`,
`보고서` 및 `사용자`일 수 있습니다. 권한을 사용으로 설정하거나
사용자에게 아이콘에 의해 표시되는 대로 해당 권한에 대한 `보기` 또는 `쓰기` 능력을
지정할 수 있습니다. 각 유형 및 아이콘에 대한 설명은
[권한](#permissions)의 내용을 참조하십시오. 

다음 옵션에서 선택하십시오.
* 사용자를 찾으십시오. **검색** 필드를 사용하여 테이블에서 사용자를
찾을 수 있습니다. 
* 사용자 추가. `관리` 권한 또는
`사용자` 권한(`쓰기` 능력 포함)이 있으면 사용자를 추가할 수 있습니다. 사용자 또는 사용자 그룹을 추가하려면 **단일 사용자 추가** 또는 **사용자 그룹 추가**를 클릭하십시오. 
**검색** 필드에서 검색할 사용자 이름 또는 그룹 이름을 입력하고
**조직** 목록에서 사용자 또는 사용자 그룹이 추가될 조직을 선택하십시오. 추가할 사용자 또는 그룹을 찾은 경우에는 사용자 이름을 클릭한 후에
**단일 사용자 추가** 또는 **복수 사용자 추가**를 클릭하여 추가하십시오. 
50명이 넘는 사용자의 그룹은 백그라운드 일괄처리 작업을 통해 추가됩니다. 
추가 오퍼레이션이 완료되면 사용자 또는 그룹이 보기 및 검색이 가능하도록 테이블에 추가됩니다. 
사용자가 추가되는 경우 사용자에게는 지정된 권한이 없습니다. 
* 권한과 조직 편집. `관리` 권한이 있으면 다른 사용자의
권한과 조직을 편집할 수 있습니다. 권한을 편집하려면 사용자를 찾고
사용자 이름을 클릭하십시오. 권한의 사용 여부를 설정하려면 열린 창에
표시된 다음 옵션 중에서 선택하십시오. 
	* 권한을 사용으로 설정하려면 목록에서 **설정**을 선택하십시오.
	* 해당 권한에 대한 `보기`(읽기 전용) 능력을 허용하려면
목록에서 **읽기**를, 해당 권한에 대한 `쓰기`(편집, 추가, 제거)
능력을 허용하려면 **쓰기**를 선택하십시오.
	* 권한을 사용 안함으로 설정하려면 **해제**를 선택하십시오.조직을 편집하려면 다음 옵션에서 선택하십시오.
	* 사용자를 조직에 추가하려면 검색 필드를 사용하여 조직을 찾은 다음 옵션에서
클릭하여 선택하고 **추가**를 클릭하십시오.
	* ![제거, 빼기 부호로 표시됨](images/icon_remove.svg) 아이콘을 클릭하여 조직에서 사용자를 제거하십시오.완료되면, **저장**을 클릭하십시오.
* 사용자 제거. `관리` 권한이 있거나
`사용자` 권한(`쓰기` 능력 포함)이 있으면 사용자를 제거할 수 있습니다.
사용자를 제거하려면 사용자를 찾고 ![삭제](images/icon_trash.svg) 아이콘을 클릭한 후 **제거**를 클릭하십시오.

### 권한
{: #permissions}

사용자에게 다음 권한을 지정할 수 있습니다. 

| **사용자 권한** | **설명** |       
|-----------------|-------------------|
| 관리 | `관리` 권한이 있는 사용자는 다른 사용자의 권한을 편집할 수 있습니다.  |
| 카탈로그 | `카탈로그` 권한이 있는 사용자에게는 로컬 또는 전용 인스턴스에서 사용 가능한 서비스에 대한 `보기` 또는 `쓰기`(수정) 능력이 지정될 수 있습니다.  |  
| 로그인 | `로그인` 권한이 있는 사용자에게는 관리 페이지가 표시됩니다. 이 권한이 없는 사용자는 관리 메뉴 옵션을 볼 수 없습니다. |
| 보고서 | `보고서` 권한이 있는 사용자에게는 보안 보고서에 대한
`보기` 또는 `쓰기`(수정) 능력이 지정될 수 있습니다.  |
| 사용자 | `사용자` 권한이 있는 사용자에게는 사용자 목록
`보기` 능력 또는 사용자 `쓰기`(추가 또는 제거) 능력이 지정될 수 있습니다.
이 권한은 다른 사용자에 대한 권한의 설정을 허용하지 않습니다. |

*표 2. 권한*

권한을 사용으로 설정하거나
사용자에게 다음 아이콘에 의해 표시되는 대로 해당 권한에 대한 `보기` 또는 `쓰기` 능력을
지정할 수 있습니다.

* 권한 옆의 ![사용, 선택 표시로 표시됨](images/icon_enabled.svg) 아이콘은 이 권한이 사용으로 설정된 상태임을 의미합니다. 
* ![보기, 눈 모양으로 표시됨](images/icon_read.svg) 아이콘은 사용자가 해당 권한에 대한 `보기`(읽기 전용) 능력을
갖고 있음을 의미합니다.
* ![쓰기, 연필로 표시됨](images/icon_write.svg) 아이콘은 사용자가 해당 권한에 대한 `쓰기`(편집, 추가 또는 제거)
능력을
갖고 있음을 의미합니다.

### Admin REST API를 통해 사용자 관리
{: #usingadminapi}

`Admin` REST API를 사용하여
{{site.data.keyword.Bluemix_notm}} 인스턴스의 사용자를 추가 및 제거할 수 있습니다. 명령행에서 기본 작업을 사용할 수 있도록
`Admin` REST API 엔드포인트와 JSON 응답이
시범 수준으로 제공됩니다. 여기 나와 있는 예제의 엔드포인트와 URL은
변경되거나 긴급 공지 후 더 이상 제공되지 않을 수 있습니다.

아래 예제를 사용하기 위한 전제조건으로
다음과 같은 도구가 필요합니다. 또한 기타 도구를 사용하도록 선택할 수 있습니다.
* REST API 요청을 명령으로 입력하기 위한 cURL. cURL은 HTTP 요청을
서버로 보내고 명령행 인터페이스를 통해 서버 응답을
수신하는 데 사용할 수 있는 무료 유틸리티입니다. [cURL
다운로드 사이트](http://curl.haxx.se/download.html){: new_window}에서 cURL을 다운로드할 수 있습니다.
* Python 정상 인쇄 JSON 도구를 사용하기 위한 Python. 이 선택적 도구는
JSON 텍스트를 입력으로 받아들이고 읽기 쉬운 출력을 제공합니다.
[Python 다운로드 사이트](https://www.python.org/downloads){: new_window}에서 Python을 다운로드할 수 있습니다.

#### 관리 콘솔에 로그인

`Admin` API 요청을 실행하기 전에
관리 콘솔에 로그인해야 합니다. `관리` 권한 또는
`사용자` 권한(`쓰기` 능력 포함)이 있으면
사용자를 추가하거나 제거할 수 있습니다. 다른 사용자의 권한을 편집하려면
`관리` 권한이 있어야 합니다. 

관리 콘솔에 로그인하려면 `https://<your_host>.ibm.com/login` 엔드포인트에서
기본 액세스 인증을 사용할 수 있습니다. 서버에서 사용자 세션의 쿠키가 리턴됩니다. 관리 콘솔의 모든 작업에
이 쿠키를 사용합니다. 

**참고:** 몇 시간 동안 사용하지 않으면
세션이 비활성화됩니다.

관리 콘솔에 로그인하려면
다음 명령을 실행하십시오.

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://<your_host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>user_id</em>:<em>password</em></dt>
<dd class="pd">사용자 ID와 비밀번호를 승인하고 기본 권한 헤더를
보냅니다. </dd>


<dt class="pt dlterm">-c <em>filename</em></dt>
<dd class="pd">지정된 사용자 ID와 비밀번호를 지정된 파일에 쿠키로
저장합니다. </dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">승인 헤더를 보냅니다.</dd>

</dl>

다음은 이 명령의 출력을 표시하는 예입니다.```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

#### 조직 나열
{: #listingorg}

사용자를 추가할 때 조직을 지정해야 합니다. `Admin` REST API를
사용하여 모든 조직을 나열할 수 있습니다.
조직을 나열하려면
`사용자` 권한(`읽기` 능력 포함)이
있어야 합니다. 모든 조직을 나열하려면 다음 명령을 실행하십시오.

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">파일에서 <samp class="ph codeph">-c</samp> 옵션을 사용하여 이전에
저장한 사용자 ID와 비밀번호를 HTTP 서버에 쿠키로
전달합니다.</dd>

</dl>

각 조직마다 결과에 다음 정보가 포함됩니다. 
* `"guid"`: 조직의 GUID입니다.
* `"name"`: 조직의 이름입니다.

다음은 이 명령의 출력을 표시하는 예입니다.```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

#### 사용자 나열
{: #listingusr}

`Admin` REST API를 사용하여 등록된 사용자를 나열함으로써
사용자가 이미 {{site.data.keyword.Bluemix_notm}}
환경에 추가되었는지 판별할 수 있습니다. 등록된 사용자를 나열하려면
`사용자` 권한(`읽기` 능력 포함)이
있어야 합니다. 모든 사용자를 나열하려면 다음 명령을 실행하십시오.

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">파일에서 <samp class="ph codeph">-c</samp> 옵션을 사용하여 이전에
저장한 사용자 ID와 비밀번호를 HTTP 서버에 쿠키로
전달합니다.</dd>
</dl>

각 등록된 사용자마다 결과에 다음 정보가 포함되어 있습니다. 
* `"first_name"`(이름) 및 `"last_name"`(성)
* `"user_id"`: 사용자 ID 및 이메일 주소입니다.
* `"guid"`: 조직의 GUID입니다.
* `"permissions"`: 사용자에게 지정된 관리 콘솔 관련 권한입니다.

다음은 이 명령의 출력을 표시하는 예입니다.

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
},
                {
                    "display": "ops.catalog.write"
},
                {
                    "display": "ops.reports.write"
},
                {
                    "display": "ops.catalog.read"
},
                {
                    "display": "ops.users.write"
},
                {
                    "display": "ops.reports.read"
},
                {
                    "display": "ops.login"
},
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

#### 사용자 추가

`Admin` REST API를 사용하여
{{site.data.keyword.Bluemix_notm}} 인스턴스에 사용자를 추가할 수 있습니다. 사용자를 추가하려면 `사용자`
권한(`쓰기` 능력 포함)이 있어야 합니다.

한 사용자 또는 사용자 목록을 추가할 수 있습니다. 단일 조직 또는 여러 조직에
사용자를 추가할 수 있습니다. -->사용자를 추가하려면
다음 정보를 제공해야 합니다.

* 사용자의 이름과 성. [사용자 나열](index.html#listingusr)에 나와 있는
`"first_name"` 및 `"last_name"`을 제공하십시오.
* 이메일 주소 및 사용자 ID: 이메일 주소와 사용자 ID에 대해 [사용자 나열](index.html#listingusr)에 나와 있는
`"user_id"`를 제공하십시오. 
* `"guid"`. [조직 나열](index.html#listingorg)에 나와 있는 조직의 GUID를 제공하십시오.

JSON 파일에 정보를 제공합니다.

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">파일에서 <samp class="ph codeph">-c</samp> 옵션을 사용하여 이전에
저장한 사용자 ID와 비밀번호를 HTTP 서버에 쿠키로
전달합니다.</dd>
</dl>

<ol>
<li>올바른 JSON 형식의 정보가 들어 있는 JSON 파일을
작성하십시오. <p>예를 들어, 다음과 같은 컨텐츠가 있는 `user.json`이라는
이름의 파일을 작성합니다.
</p>
<pre>
{
    "members": [
        {
            "emails": [
"some_user_id@domain.com"
],
            "first_name": "Some_first_name",
            "last_name": "Some_last_name",
            "user_id": "some_user_id@domain.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>Post the content of the JSON file to the user's endpoint by running the following
command:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<your_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">

<dt class="pt dlterm">-v </dt>
<dd class="pd">자세한 출력을 지정합니다.</dd>


<dt class="pt dlterm">-X POST</dt>
<dd class="pd">POST 요청을 지정하고 기본 GET 요청을 대체합니다.</dd>


<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">content-type 헤더를 지정합니다. 이 경우 JSON입니다.</dd>


<dt class="pt dlterm">-d *data*</dt>
<dd class="pd">데이터를 지정합니다. 이 경우, POST 요청을 통해
`user.json` 파일을 HTTP 서버로 보냅니다.</dd>

</dl>



다음은 이 명령의 출력을 표시하는 예입니다.

```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

#### 사용자 제거

`Admin` REST API를 사용하여
{{site.data.keyword.Bluemix_notm}} 인스턴스에서 사용자를 제거할 수 있습니다. 사용자를 제거하려면 `사용자`
권한(`쓰기` 능력 포함)이 있어야 합니다. 

사용자를 제거하려면
사용자의 ID를 제공해야 합니다.다음 명령을 실행하십시오. 

`curl -v -b ./cookies.txt -X DELETE https://<your_host>.ibm.com/codi/v1/users?user_id=<some_user_id@domain.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">DELETE 요청을 지정합니다.</dd>
</dl>

다음은 이 명령의 출력을 표시하는 예입니다.

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}

### 사용자 정의 서비스 API
{: #servicebrokerapi}

새 서비스를 등록하거나 작성하고, 서비스를 업데이트 및 삭제할 때는 3가지 API를 사용할 수 있습니다.

모든 API는 <code>https://opsconsole.&lt;subdomain&gt;.bluemix.net/</code>을 기준으로 합니다.

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>이 값은 로컬 또는 전용 인스턴스의 이름입니다. {{site.data.keyword.Bluemix}} 인스턴스의 하위 도메인은
온보딩 중에 지정되었습니다. </dd>
</dl>

### 새 서비스 등록

새 서비스를 등록하려면 다음 API와 코드 예제를 사용하십시오.

#### 라우트

```
POST /codi/v1/serviceBrokers
```
{: screen}

#### 요청

*표 3. 필드*

| **이름** | **설명** |
|-----------------|-------------------|
| name | 서비스 브로커의 이름입니다.  |
| auth_username | 서비스 브로커와 연결하는 데 사용하는 사용자 이름입니다.  |
| auth_password | 서비스 브로커와 연결하는 데 사용하는 비밀번호입니다.  |
| broker_url | 서비스 브로커와 연결하는 데 사용하는 URL입니다.  |
| owningOrganization | 서비스 화이트리스트를 작성하는 초기 조직입니다. |

##### 본문

```
{
  "name" : "Service broker's name",
  "auth_username" : "username",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

##### 헤더

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### 응답

##### 상태

```
201 Created
```
{: screen}

##### 본문

```
{
  "entity": {
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

### 서비스 업데이트

서비스를 업데이트하려면 다음 API와 코드 예제를 사용하십시오.

#### 라우트

`PUT /codi/v1/serviceBrokers`
{: screen}

#### 요청

*표 4. 필드*

| **이름** | **설명** |
|-----------------|-------------------|
| name | 서비스 브로커의 이름입니다. 서비스 작성 시 사용한 이름에서 이 이름을 변경할 수 없습니다. |
| auth_username | 서비스 브로커와 연결하는 데 사용하는 사용자 이름입니다.  |
| auth_password | 서비스 브로커와 연결하는 데 사용하는 비밀번호입니다.  |
| broker_url | 서비스 브로커와 연결하는 데 사용하는 URL입니다.  |
| owningOrganization | 서비스 화이트리스트를 작성하는 초기 조직입니다. |

##### 본문

```
{
  "name" : "Service Broker's name",
  "auth_username" : "username",
  "auth_password" : "newPassword",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

##### 헤더

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### 응답

##### 상태

```
201 Created
```
{: screen}

##### 본문

```
{
  "entity": {
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

### 서비스 삭제

서비스를 삭제하려면 다음 API와 코드 예제를 사용하십시오.

*표 5. 매개변수*

| **이름** | **설명** |
|-----------------|-------------------|
| name | 서비스 브로커의 이름입니다. 서비스 작성 시 사용한 이름에서 이 이름을 변경할 수 없습니다. |

#### 라우트

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

#### 요청

##### 헤더

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### 응답

##### 상태

```
204 No Content
```
{: screen}

### cf CLI를 사용하여 사용자 관리
{: #usingadmincli}

{{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인과 함께
Cloud Foundry 명령행 인터페이스를 사용하여 {{site.data.keyword.Bluemix_notm}} Local 또는
{{site.data.keyword.Bluemix_notm}} Dedicated 환경의 사용자를
관리할 수 있습니다. 예를 들어,
LDAP 레지스트리에서 사용자를 추가할 수 있습니다.

시작하기 전에 cf 명령행 인터페이스를 설치하십시오. {{site.data.keyword.Bluemix_notm}} 관리
CLI 플러그인에는 cf 버전 6.11.2 이상이 필요합니다.[Cloud Foundry 명령행 인터페이스 다운로드](https://github.com/cloudfoundry/cli/releases){: new_window}

**제한사항:** Cloud Foundry 명령행 인터페이스는
Cygwin에서는 지원되지 않습니다. Cygwin 명령행 창 외의
명령행 창에서 Cloud Foundry 명령행 인터페이스를 사용하십시오.

#### {{site.data.keyword.Bluemix_notm}} 관리
CLI 플러그인 추가

cf 명령행 인터페이스가 설치된 후에 {{site.data.keyword.Bluemix_notm}}
관리 CLI 플러그인을 추가할 수 있습니다.

저장소를 추가하고 플러그인을 설치하려면 다음 단계를 완료하십시오.

<ol>
<li>{{site.data.keyword.Bluemix_notm}} 관리 플러그인 저장소를 추가하려면 다음 명령을 실행하십시오. <br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://opsconsole.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 인스턴스 URL의 하위 도메인입니다.</dd>
</dl>
</li>
<li>{{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인을 설치하려면 <br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code> 명령을 실행하십시오.
</li>
</ol>

명령 목록을 보려면 다음 명령을 실행하십시오.

`cf plugins`
{: codeblock}

명령에 대한 추가 도움말을 보려면 `-help` 옵션을 사용하십시오.

{{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인의 사용 방법에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 관리](../cli/plugins/bluemix_admin/index.html)를 참조하십시오.
