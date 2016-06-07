---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} Local 및 {{site.data.keyword.Bluemix_notm}} Dedicated 관리
{: #mng}
*마지막 업데이트 날짜: 2016년 5월 16일*

{{site.data.keyword.Bluemix_notm}} Local 또는 {{site.data.keyword.Bluemix_notm}} Dedicated에 대한 관리자 액세스 권한이 있으면 **관리** 페이지로 이동하여 자원을 관리하고, 할당 사용량을 모니터링하고, 사용자 권한을 관리하고, 업그레이드 알림을 스케줄링하고, 보안 보고서 및 로그를 확인하는 등 다양한 작업을 수행할 수 있습니다. 영역을 작성하고 [사용자 역할 및 권한](index.html#oc_useradmin)을 설정하여 조직을 관리할 수 있습니다. [조직 관리](../admin/orgs_spaces.html)를 참조하십시오.
{:shortdesc}

*표 1. {{site.data.keyword.Bluemix_notm}} Local 또는 Dedicated 인스턴스* 관리를 위한 관리 태스크

| 수행할 수 있는 작업 | 세부사항 |    
|----------------|---------|
|시스템 사용량 모니터링 | **관리 &gt; 사용량**을 클릭하십시오. 시스템 정보를 확인하고, CPU 사용량을 모니터링하고, 사용량을 계획하여 기업에 가장 최선의 결정을 내리십시오. [사용량 정보 보기](index.html#oc_resource)를 참조하십시오.|
|카탈로그 관리 | 사용자 및 조직에 표시되는 서비스를 관리하려면 **관리 &gt; 카탈로그 관리**를 클릭하십시오. [카탈로그 관리](index.html#oc_catalog)를 참조하십시오.|
|조직 관리 | 조직을 작성하고 조직의 할당량을 모니터링하며 요구사항에 따라 신속하게 의사결정을 내리려면 **관리 &gt; 조직 관리**를 클릭하십시오. [조직 관리](index.html#oc_organizations)를 참조하십시오.|
|영역 작성 및 사용자 역할 지정 | 조직 내에 영역을 작성하려면 **계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg)을 클릭한 후 **조직 관리**를 선택하십시오. 사용자를 추가하고 조직과 영역을 사용자에게 지정하십시오.[조직 관리](../admin/orgs_spaces.html)를 참조하십시오. |
|관리자 권한 관리 | 사용자를 추가하거나 제거하고 사용자 권한을 조정하려면 **관리 &gt; 사용자 관리**를 클릭하십시오. [사용자 및 권한 관리](index.html#oc_useradmin)를 참조하십시오. |
|보고서 및 로그 검토 | 인스턴스에 대한 보안 보고서 및 감사 로그를 보려면 **관리 &gt; 보고서 및 로그**를 클릭하십시오. [보고서 보기](index.html#oc_report)를 참조하십시오. |
|시스템 정보 보기 | 보류 중인 업데이트, 인스턴스의 이름 및 버전, 지역, API URL, CLI URL, LDAP 구성 세부사항, 그룹 및 사용자 맵핑, 통계, 공유 도메인 등의 시스템 정보를 보려면 **관리 &gt; 시스템 정보**를 클릭하십시오. 보류 중인 업데이트 섹션에서 알림을 확장하기 위해 달력 필드 및 이벤트 구독에 액세스할 수도 있습니다. [시스템 정보 보기](index.html#oc_system)를 참조하십시오. |
|알림 확장 및 이벤트 구독 설정 | **관리 &gt; 시스템 정보 &gt; 보류 중인 업데이트 *수***를 클릭하십시오. 웹 후크로 원하는 웹 서비스와 통합하여 업데이트 또는 인시던트에 대한 이벤트 알림 구독을 설정할 수 있습니다. [알림 및 이벤트 구독](index.html#oc_eventsubscription)을 참조하십시오. |


## 알림 및 이벤트 구독
{: #oc_eventsubscription}

상태 페이지를 확인하여 항상 사용하는 환경의 상태를 알 수 있습니다. {{site.data.keyword.Bluemix_notm}}에서는 또한 관리 페이지의 알림 영역에 이벤트(예: 스케줄된 유지보수 및 업그레이드)에 대한 알림을 전송합니다. 인시던트는 상태 페이지에서 보고됩니다.

### 알림

로컬 또는 전용 환경에 대한 IBM의 알림을 보고 환경의 상태를 모니터할 수 있습니다. 다음 표에서 다양한 유형의 알림과 그러한 알림이 게시되는 위치에 대한 정보를 검토하십시오.

*표 2. 이벤트 유형 및 알림 방법*

| **이벤트 유형** | **알림 방법** |       
|-----------------|-------------------|
| 유지보수 업데이트 | 관리 페이지의 알림에 곧 있을 유지보수 업데이트에 대한 경보가 표시됩니다. **관리** 페이지로 이동하여 **알림** 아이콘 ![알림](images/icon_announcement.svg)을 선택하십시오. 보류 중 및 완료 알림의 전체 목록 및 히스토리를 보려면 **관리 &gt; 시스템 정보 ** &gt; **보류 중인 업데이트** *수*를 클릭하십시오. 관리 페이지의 유지보수 업데이트 경보를 원하는 웹 서비스와 통합하여 메시지를 도움말 데스크 이메일 주소로 라우트하거나 SMS 메시지를 원하는 전화번호로 라우트하는 이벤트 구독을 설정함으로써 알림 기능을 확장할 수 있습니다. |
| 중요 인시던트 | 상태 페이지에 중요 인시던트에 대한 경보가 표시됩니다. **계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg)을 클릭한 후 **상태**를 선택하십시오. 상태 페이지의 인시던트 경보를 원하는 웹 서비스와 통합하여 메시지를 도움말 데스크 이메일 주소로 라우트하거나 SMS 메시지를 원하는 전화번호로 라우트하는 이벤트 구독을 설정함으로써 알림 기능을 확장할 수 있습니다. |  
| 상태 | 플랫폼, 서비스 및 {{site.data.keyword.Bluemix_notm}} 인스턴스의 최신 상태를 볼 수 있습니다. **계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg)을 클릭한 후 **상태**를 선택하십시오.   |

### 이벤트 구독 설정

웹 후크를 구현하는 이벤트 구독을 사용하여 관리 페이지 및 상태 페이지로 전송되는 알림의 기능을 확장할 수 있습니다. 웹 후크는 원하는 대상(예: 도움말 데스크 이메일 주소(이메일을 통해) 또는 전화번호(SMS 메시지를 통해))으로 직접 알림을 라우트합니다. 알림 유형(특히, 유지보수 업데이트 또는 중요 인시던트)과 알림에 포함되는 정보를 사용자 정의할 수 있습니다.

웹 후크를 사용하여 특정 이벤트 구독을 설정하려면 다음 단계를 완료하십시오.

* 유지보수 업데이트 알림의 경우, **시스템 정보** &gt; **보류 중인 업데이트** *수*로 이동한 후 **구독** 아이콘 ![구독](images/icon_subscribe.svg)을 클릭하십시오.
* 인시던트 경보 알림의 경우, **계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg) &gt; **상태**를 클릭한 후 **구독** 아이콘 ![구독](images/icon_subscribe.svg)을 클릭하십시오. 

**참고**: 기술된 두 방법 중 하나를 사용하여 해당 유형의 알림을 표시하는 이벤트 구독 페이지에 액세스할 수 있습니다.

1. **구독 추가**를 클릭하십시오.

2. 이벤트 구독 양식을 채우십시오. 양식의 필드 및 페이로드 섹션에서 사용할 값에 대한 정보는 다음 표를 검토하십시오.

*표 3. 이벤트 구독 양식 필드*

| **필드** | **설명** |
|-----------------|-------------------|
| 유형 | 웹 후크를 선택하십시오. |
| 방법 | GET 또는 POST를 선택하십시오.  |
| 이벤트 | 업데이트에 대한 알림을 구독할지 또는 인시던트에 대한 알림을 구독할지 선택하십시오. |
| URL | 사용하는 웹 서비스에 후크할 URL을 입력하십시오.  |
| 설명 | 작성할 이벤트 구독에 대한 설명을 추가하십시오.  |
| 사용자 이름 | 사용하는 웹 서비스의 사용자 이름을 입력하십시오. 개인 신임 정보를 사용하지 않으려는 경우 {{site.data.keyword.Bluemix_notm}}에서 사용할 기능 ID를 설정할 수 있습니다. |
| 비밀번호 | 사용하는 웹 서비스의 비밀번호를 입력하십시오. |
| 페이로드 | POST 방법을 선택한 경우, 사용 중인 웹 서비스에 고유한 특성을 IBM 알림에 사용되는 값과 쌍을 지어 입력하십시오. 알림을 채우는 데 사용할 수 있는 IBM 값은 다음 표를 참조하십시오. 이 섹션에 정보를 입력하지 않으면 추가 정보가 없는 알림이 수신됩니다. |

*표 4. 페이로드 섹션 값*

| **IBM 값** | **설명** | **이벤트 유형** |
|----------------|----------------|------------------------|
| {{content.title}} | 메시지 제목 |  업데이트 및 인시던트  |
| {{status}} | 업데이트 또는 인시던트의 상태 | 업데이트 및 인시던트 |
| {{type}} | 업데이트 또는 인시던트 | 업데이트 및 인시던트 | 
| {{region}} | 영향을 받는 지역 | 업데이트 및 인시던트 |
| {{content.message}} | 메시지 설명 |   업데이트 및 인시던트  |
| {{content.severity}} | 심각도 등급 | 인시던트 |
| {{content.category}} | 영향을 받는 서비스 | 인시던트 |
| {{content.subCategoryName}} | 영향을 받는 컴포넌트 | 인시던트 |
| {{content.scheduleWindow}} | 스케줄된 업데이트 날짜 | 업데이트 |
| {{content.disruption}} | 영향을 받는 컴포넌트 | 업데이트 |

이벤트 구독이 저장되면 사용하는 웹 서비스를 통해 설정한 방법으로 알림이 수신됩니다. 인시던트의 경우 상태 페이지에, 그리고 유지보수 업데이트의 경우 관리 페이지의 알림 영역에 알림이 계속 게시됩니다.

저장된 이벤트 구독을 선택하여 최근 활동을 볼 수 있습니다. 클릭하여 최근 활동 항목을 펼치면 세부사항이 표시됩니다. 세부사항에는 페이로드 섹션에서 사용할 수 있는 알림에 대한 IBM 값이 포함됩니다. 이러한 값을 보려면 최근 활동 항목을 펼치고 **이벤트**를 펼친 후 **오브젝트**를 펼치십시오.

## 유지보수 업데이트
{: #oc_schedulemaintenance}

**관리 &gt; 시스템 정보 &gt; 보류 중인 업데이트 *수***로 이동하여 **시스템 업데이트** 페이지에 액세스하여 스케줄 및 보류 중인 유지보수 업데이트를 확인할 수 있습니다. 

**참고**: 사전 승인된 유지보수 기간 설정을 시작하려면 다음 섹션을 참조하십시오. IBM이 사용자 환경에 대한 유지보수를 스케줄하려면 해당 기간을 설정해야 합니다.

<dl>
<dt>시스템을 중단하지 않는 업데이트</dt>
<dd>시스템을 중단하지 않는 업데이트는 사용자 환경, 실행 중인 애플리케이션 또는 애플리케이션에 대한 사용자 액세스에 영향을 주지 않습니다. 이 업데이트 유형은 케이스별 승인이 필요하지 않으며 시스템 업데이트 페이지에서 설정한 사전 승인된 사용 가능한 유지보수 기간 동안 적용됩니다.</dd>
<dt>시스템을 중단하는 업데이트</dt>
<dd>시스템을 중단하는 업데이트는 사용자 환경, 실행 중인 애플리케이션 또는 애플리케이션에 대한 사용자 액세스에 영향을 줄 수 있습니다. 할당된 21일 유지보수 기간 내에서 각각의 해당 유지보수 업데이트를 스케줄하고 승인해야 합니다. 사전 승인된 업데이트 기간을 기반으로 하는 제안된 배치 날짜 및 시간을 선택하거나 업데이트를 스케줄할 때 IBM이 선택할 두 개의 추가 시간 및 날짜를 선택할 수 있습니다.</dd>
</dl>


### 사전 승인된 유지보수 기간 설정
{: #preapprovedmaintenance}

업데이트 스케줄 및 승인을 시작하기 전에 사전 승인된 유지보수 기간을 설정해야 합니다. 시스템을 중단하지 않는 업데이트는 사전 승인된 시간 동안 스케줄됩니다. 시스템을 중단하지 않는 업데이트는 사용자 환경, 실행 중인 애플리케이션 또는 애플리케이션에 대한 사용자 액세스에 영향을 주지 않습니다. 이 업데이트 유형은 케이스별 승인이 필요하지 않으며 시스템 업데이트 페이지에서 설정한 사전 승인된 사용 가능한 유지보수 기간에 적용됩니다.

일주일에 최소 3일 동안 최소 24시간의 사용 가능한 시간을 설정해야 합니다. 예를 들어, 독립된 3일 동안 세 번의 8시간 기간을 설정하거나 독립된 4일 동안 6시간 기간을 설정할 수 있습니다. 기간이 업데이트를 적용할 수 있는 충분한 시간을 제공하도록 하려면 각 기간이 최소 4시간 동안 지속되어야 합니다.

1. **관리 &gt; 시스템 정보 &gt; 보류 중인 업데이트 *수* &gt; 가용성 관리**로 이동하십시오.
2. **사용 가능한 업데이트 기간 관리** 섹션을 펼치십시오.
3. **새로 추가** ![새로 추가](images/add-new.png)를 클릭하십시오.
4. 기간의 빈도, 지속 기간 및 시작 시간을 선택하여 첫 번째 가용성 기간을 설정하십시오.
5. **제출**을 클릭하십시오.
6. 주별 기간의 최소 요구사항을 충족할 때까지 이 프로세스를 반복하십시오.

### 사용 불가능한 유지보수 기간 설정

사전 승인된 사용 가능한 유지보수 기간을 설정한 후 사용자 환경을 업데이트할 수 없는 특정 날짜 및 시간을 설정하도록 선택할 수 있습니다. 예를 들어, 트래픽이 높은 주말 또는 공휴일에는 유지보수가 적용되지 않도록 선택하여 사용자가 애플리케이션을 사용할 수 있도록 할 수 있습니다.

1. **관리 &gt; 시스템 정보 &gt; 보류 중인 업데이트 *수* &gt; 가용성 관리**로 이동하십시오.
2. **사용 불가능한 업데이트 기간 관리** 섹션을 펼치십시오.
3. **새로 추가** ![새로 추가](images/add-new.png)를 클릭하십시오.
4. 기간의 빈도, 지속 기간 및 시작 시간을 선택하여 사용 불가능한 기간을 설정하십시오.
5. **제출**을 클릭하십시오.

### 업데이트 스케줄 및 승인
{: #scheduleandapprove}

사전 승인된 유지보수 기간을 설정하면 해당 시간 동안 시스템을 중단하지 않는 업데이트가 자동으로 스케줄됩니다. 해당 업데이트 유형에 대한 명시적 승인은 필요하지 않습니다. 그러나 업데이트 중인 항목, 업데이트에 걸릴 시간 및 업데이트가 스케줄된 시간을 포함하여 각 유지보수 업데이트에 대한 세부사항을 볼 수 있습니다. 

시스템을 중단하지 않는 업데이트에 대한 세부사항을 보려면 다음 단계를 완료하십시오.

1. **관리 &gt; 시스템 정보 &gt; 보류 중인 업데이트 *수***로 이동하십시오.
2. **고객 스케줄링 필수**가 **아니오**로 설정된 업데이트 행을 식별하십시오.
3. 해당 업데이트의 행을 선택하여 세부사항을 보십시오.

시스템을 중단하는 업데이트는 사용자 환경, 실행 중인 애플리케이션 또는 애플리케이션에 대한 사용자 액세스에 영향을 줄 수 있습니다. 할당된 21일 유지보수 기간 내에서 각각의 해당 유지보수 업데이트를 스케줄하고 승인해야 합니다. 사전 승인된 업데이트 기간을 기반으로 하는 제안된 배치 날짜 및 시간을 선택하거나 업데이트를 스케줄할 때 IBM이 선택할 두 개의 추가 시간 및 날짜를 선택할 수 있습니다.

승인이 필요하지 않은 시스템을 중단하지 않는 업데이트의 경우, 다음 단계를 완료하십시오.

1. **관리 &gt; 시스템 정보 &gt; 보류 중인 업데이트 *수***로 이동하십시오.
2. **고객 스케줄링 필수**가 **예**로 설정된 업데이트 행을 식별하십시오.
3. 해당 업데이트의 행을 선택하여 업데이트 설명, 제안된 업데이트 날짜 및 시간, 영향을 받는 컴포넌트 및 업데이트 지속 기간을 포함하여 업데이트 세부사항을 검토하십시오.
4. **스케줄 및 승인**을 선택하십시오.
5. **제안된 날짜**, **대체 날짜** 또는 **사전 승인된 모든 기간** 옵션에서 선택하십시오.
6. **제출**을 선택하십시오. 

선택사항을 기반으로 허용한 제한된 날짜, 사전 승인된 기간 중 하나 또는 대체 날짜 및 시간 중 하나 동안 업데이트가 적용됩니다. IBM이 업데이트 스케줄 날짜를 최종 확인하면 **시스템 업데이트** 페이지의 업데이트 세부사항에 스케줄된 날짜가 반영됩니다.

### 스케줄된 업데이트에 대한 달력 피드 설정

시스템 업데이트 페이지에서 **달력** 아이콘 ![달력](images/icon_calendar.svg)을 클릭하고 `.ics` 파일을 다운로드하여 스케줄된 업데이트를 선택한 달력 앱으로 가져와서 업데이트 스케줄을 추적하도록 선택할 수 있습니다.

<ol>
<li>달력 앱을 여십시오.</li>
<li>**달력** 아이콘 ![달력](images/icon_calendar.svg)을 클릭하여 달력 파일을 다운로드한 후 `.ics` 파일을 사용하여 달력 앱으로 가져오십시오.</li>
<li>신임 정보를 입력하십시오.</li>
<li>스케줄된 업데이트를 보십시오.</li>
</ol>

원하는 웹 서비스와 통합하는 이벤트 구독을 사용하여 관리 페이지의 알림 기능을 확장할 수도 있습니다. 업데이트 또는 인시던트에 대한 이벤트 알림 구독을 설정하려면 [이벤트 구독 및 알림](index.html#oc_eventsubscription)을 참조하십시오.

## 시스템 정보 보기
{: #oc_system}

시스템 정보를 보려면 **관리 &gt; 시스템 정보**를 클릭하십시오.

보류 중인 유지보수 업데이트, 일반 시스템 정보 및 LDAP 구성 세부사항에 대한
다양한 섹션을 펼치고 볼 수 있습니다.

### 보류 중인 시스템 업데이트

업데이트 섹션에서 사용자 측의 조치가 필요한
보류 중인 업데이트 수를 볼 수 있습니다. 두 가지 유형의 유지보수 업데이트를 볼 수 있습니다.

<dl>
<dt>시스템을 중단하지 않는 업데이트</dt>
<dd>시스템을 중단하지 않는 업데이트는 사용자 환경, 실행 중인 애플리케이션 또는 애플리케이션에 대한 사용자 액세스에 영향을 주지 않습니다. 이 업데이트 유형은 케이스별 승인이 필요하지 않습니다. 이 업데이트는 시스템 업데이트 페이지에서 설정한 사전 승인된 사용 가능한 유지보수 기간에 적용됩니다.</dd>
<dt>시스템을 중단하는 업데이트</dt>
<dd>시스템을 중단하는 업데이트는 사용자 환경, 실행 중인 애플리케이션 또는 애플리케이션에 대한 사용자 액세스에 영향을 줄 수 있습니다. 중요한 비즈니스 시간 동안 업데이트가 적용되지 않도록 할당된 21일 유지보수 기간 내에서 각각의 해당 유지보수 업데이트를 스케줄하고 승인하는 기능이 있습니다. 사전 승인된 업데이트 기간을 기반으로 하는 제안된 배치 날짜 및 시간을 선택하거나 업데이트를 적용할 때 IBM이 선택할 두 개의 추가 시간 및 날짜를 선택할 수 있습니다.</dd>
</dl>

사전 승인된 유지보수 기간 설정, 유지보수에 사용할 수 없는 특정 날짜 설정 및 달력 피드 설정에 대한 자세한 정보는 [유지보수 업데이터](index.html#oc_schedulemaintenance)를 참조하십시오.

### 일반 시스템 정보

일반 정보 섹션에서 다음 정보를 볼 수 있습니다. 

- {{site.data.keyword.Bluemix_notm}} 빌드에 대한 기본 정보
- 버전, URL 지역 및 CLI 문서에 대한 링크를 포함한 API 정보
- 사용자의 시스템 및 서비스에 대한 공유 도메인 정보
- 애플리케이션, 사용자 및 조직의 총 수에 대한 통계

### LDAP 구성 세부사항

LDAP 구성 세부사항 섹션에서 LDAP 서버를 선택하면 사용자 및 그룹 맵핑에 대한 정보를 볼 수 있습니다. {{site.data.keyword.IBM}} WebID를 사용 중인 경우에는 이 섹션에 이 정보가 표시됩니다. 

## 사용량 및 보고서 보기
{: #oc_resource}

로컬 또는 전용 인스턴스와 {{site.data.keyword.Bluemix_notm}} 계정에 대한 여러 유형의 사용량 정보를 볼 수 있습니다. 또한 {{site.data.keyword.Bluemix_notm}} 인스턴스에 대한 보안 보고서 및 로그를 다운로드하고 볼 수 있습니다.

- 디스크 공간, CPU 사용량, 네트워크 사용량 및 평균 응답시간을 포함한 자원 정보. [자원 사용량](index.html#resourceusage)을 참조하십시오.
- 런타임 앱 수(사용량 포함), GB-시간 총 수 및 서비스 인스턴스 수(사용량 포함)를 포함한 조직당 계정 사용량. [계정 사용량](index.html#accountusage)을 참조하십시오.
- 조직 메모리 할당량 사용량, 사용되는 총 메모리 할당량을 기반으로 할당된 앱 메모리 및 특정 조직의 앱당 GB-시간 사용량 보기. 또한 조직 관리 페이지의 할당량 모니터링 섹션에서 모든 조직의 할당량 사용량을 볼 수 있습니다. [조직 관리](../admin/index.html#orgusage)를 참조하십시오.


### 자원 사용량
{: #resourceusage}

자원 사용량 정보를 보려면 **관리 &gt; 사용량**을 클릭하십시오.

자원 모니터링 섹션에서 다음 정보를 볼 수 있습니다.

- 사용된 메모리의 양(GB 단위) 및 디스크 공간의 양(GB 단위)과 같은 자원 사용 정보를 볼 수 있습니다. 모든 DEA(Droplet Execution Agent)에 대한
평균 CPU 사용량을 볼 수 있습니다. **CPU** 타일을 클릭하면 각 DEA에 대한 CPU 사용량을 볼 수 있습니다. 사용량이 가장 많은 DEA가
처음에 나열되며, 각각은 작업 및 IP 주소로 식별됩니다. CPU 사용량은 시스템 프로세스의 CPU 소비량,
사용자 프로세스의 CPU 소비량 및 대기 프로세스의 CPU 소비량을 포함하는 세 개의 카테고리로 구분됩니다. 
- 지난 날짜, 주 또는 월에 대해 송신 대역폭 및 수신 대역폭에 대한 네트워크 사용량 정보를 볼 수 있습니다. 표시되는 데이터는
공용 및 개인용 네트워크 둘 다의 입출력 트래픽 합계를 기반으로 합니다. 
- 지난 10분, 시간, 일에 대한 {{site.data.keyword.Bluemix_notm}}의 평균 응답 시간
- 지난 10분, 시간, 일에 대한 {{site.data.keyword.Bluemix_notm}}의 초당 평균 트랜잭션 수

### 계정 사용량
{: #accountusage}

전용 또는 로컬 환경에 대한 계정의 매월 사용량을 볼 수 있습니다. 이 데이터를 사용하여 사용량을 기반으로 특정 조직에 부과할 비용을 식별할 수 있습니다.

<ol>
<li><strong>계정 및 지원</strong> 아이콘 ![계정 및 지원](../support/images/account_support.svg) &gt; <strong>계정</strong> &gt; <strong>사용 세부사항</strong>을 클릭하십시오.</li>
<li>데이터를 보려는 조직을 선택하십시오.</li>
<li>다음 카테고리의 사용 세부사항을 볼 수 있습니다.
<ul>
<li>사용량이 포함된 런타임 앱</li>
<li>GB-시간 단위의 런타임 앱 총 사용량</li>
<li>사용량이 포함된 서비스 인스턴스</li>
</ul>
</li>
<li>선택사항: 특정 월의 데이터를 보려면 <strong>클라우드 활동</strong> 메뉴에서 원하는 월을 선택하십시오.</li>
<li>선택사항: 선택한 월의 데이터를 <code>CSV</code> 또는 <code>JSON</code> 파일로 내보내려면 <strong>데이터 내보내기</strong>를 클릭하고 <strong>CSV</strong> 또는 <strong>JSON</strong>을 선택하십시오.</li>
</ol>

또한 {{site.data.keyword.Bluemix_notm}} Public에서 신디케이트된 런타임, 앱 및 서비스의 매월 사용량 및 연관된 비용을 계정 레벨에서 볼 수 있습니다. 이 데이터를 사용하여 사용량을 기반으로 특정 조직에 부과할 비용을 식별할 수 있습니다.

<ol>
<li><strong>계정 및 지원</strong> 아이콘 ![계정 및 지원](../support/images/account_support.svg) &gt; <strong>계정</strong> &gt; <strong>사용 세부사항</strong>을 클릭하십시오.</li>
<li><strong>공용</strong>을 클릭하십시오.</li>
<li>데이터를 보려는 조직을 선택하거나, <strong>모든 조직</strong>을 선택하여 한 번에 모든 조직의 데이터를 볼 수 있습니다. </li>
<li>다음 카테고리의 사용 세부사항을 볼 수 있습니다.
<ul>
<li>사용량이 포함된 런타임 앱</li>
<li>GB-시간 단위의 런타임 앱 총 사용량</li>
<li>사용량이 포함된 서비스 인스턴스</li>
<li>신디케이트된 모든 런타임, 서비스 및 앱에 대한 비용 요약</li>
</ul>
</li>
<li>선택사항: 특정 월의 데이터를 보려면 막대 그래프에서 원하는 월을 선택하십시오. 기본적으로 현재 월의 데이터가 표시됩니다.</li>
<li>선택사항: 선택한 월의 데이터를 <code>CSV</code> 또는 <code>JSON</code> 파일로 내보내려면 <strong>데이터 내보내기</strong>를 클릭하고 <strong>CSV</strong> 또는 <strong>JSON</strong>을 선택하십시오.</li>
</ol>


### 조직 사용량
{: #orgusage}

조직당 사용량을 보려면 **관리 &gt; 조직 관리**를 클릭한 후 **조직 목록**에서 조직을 선택하십시오. 선택한 조직의 **조직 관리** 페이지에서 다음과 같은 사용 정보를 볼 수 있습니다.

- 현재 사용 중인 서비스 수
- 현재 사용 중인 라우트 수
- 할당량 중 사용되는 양 및 현재 사용 중이 아닌 양을 표시하는 메모리 할당량 그래프
- 사용되는 메모리 할당량에 포함되는 애플리케이션을 표시하는 애플리케이션 할당 그래프
- 배치된 앱당 사용된 GB-시간의 3개월 보고서를 표시하는 측정된 애플리케이션 사용량 그래프. **목록 보기**를 선택하면 지난 3개월 간의 앱당 메모리 할당 및 측정된 GB-시간 사용량을 포함하여 모든 앱에 대한 데이터를 볼 수 있습니다.

조직당 사용량 보기, 할당량 플랜 조정 및 조직 관리에 대한 자세한 정보는 [조직 관리](../admin/index.html#oc_organizations)를 참조하십시오.

### 보고서
{: #oc_report}

{{site.data.keyword.Bluemix_notm}} 인스턴스에 대한 DataPower&trade;, 방화벽 및 로그인 감사 등의
보안 보고서 및 로그를 볼 수 있습니다.보고서 및 로그를 보려면 **ADMINISTRATION &gt; REPORTS AND LOGS**를 클릭하십시오.

다음 옵션 중에서 선택하십시오.

- 필드에서 시작 및 종료 날짜를 선택하여 표시될 보고서 및 로그를 필터링할 수 있습니다.
- 탐색 분할창에서 다양한 보고서를 펼치고 볼 수 있습니다. 
- 보고서 및 로그의 콜렉션 내에서 검색할 수 있습니다. 검색은 보고서 이름과 보고서 및 로그에
포함된 텍스트 컨텐츠에 적용됩니다. 또한 **관리 이벤트**, **DataPower
보고서**, **방화벽** 및 **로그인 감사**를 기준으로 검색을 필터링할 수도 있습니다. 
- 보고서 또는 로그를 표시할 때 ![다운로드](images/icon_download.png) 아이콘을
클릭하여 이를 다운로드할 수 있습니다.

다음 표는 {{site.data.keyword.Bluemix_notm}} Local 및 {{site.data.keyword.Bluemix_notm}} Dedicated에 대해 생성되는
보안 보고서 목록을 보여줍니다.

*표 5. 보안 보고서 목록*

| **카테고리** | **보고서** | **설명** |      
|-----------------|-------------------|---------------------|
| 방화벽 | 방화벽 로그인 | Vyatta 방화벽 디바이스에 대한 관리자 로그인과 관련한 이벤트. |
| 방화벽 | 방화벽 거부 | 적용 중인 방화벽 규칙에 따라 액세스 요청이 거부되는 경우 Vyatta 방화벽 디바이스가 생성하는 이벤트. |
| {{site.data.keyword.Bluemix_notm}} 관리자 로그인 이벤트 | {{site.data.keyword.Bluemix_notm}} 관리자 로그인 | 관리자가 모든 {{site.data.keyword.Bluemix_notm}} 시스템에서 SSH 세션을 시작할 때 운영 체제가 생성하는 이벤트. |
| {{site.data.keyword.Bluemix_notm}} 애플리케이션 개발자 로그인 이벤트 | {{site.data.keyword.Bluemix_notm}} 애플리케이션 개발자 로그인 | {{site.data.keyword.Bluemix_notm}} 플랫폼 사용자가 명령행, REST API 또는 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 사용하여 세션을 시작할 때 {{site.data.keyword.Bluemix_notm}} 플랫폼 로그인 컴포넌트가 생성하는 이벤트. |
| {{site.data.keyword.Bluemix_notm}} 관리자 관리 이벤트 | {{site.data.keyword.Bluemix_notm}} 관리자 운영 체제 관리 이벤트 | 관리자가 현재 작업 세션 내에서 조치를 수행할 때 운영 체제가 생성하는 이벤트. |
| {{site.data.keyword.Bluemix_notm}} 애플리케이션 개발자 관리 이벤트 | {{site.data.keyword.Bluemix_notm}}(Cloud Foundry) 관리 이벤트 | 명령행, REST API 또는 {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스를 사용하여 {{site.data.keyword.Bluemix_notm}} 플랫폼 사용자가 수행하는 오퍼레이션과 관련된 이벤트. |
| {{site.data.keyword.Bluemix_notm}} 관리자 데이터베이스 관리 이벤트 | 데이터베이스 관리 이벤트 | {{site.data.keyword.Bluemix_notm}} 내부 데이터베이스에서 데이터베이스 관리자가 수행하는 오퍼레이션과 관련한 이벤트. |
| 관리 이벤트 | 사용자 관리 이벤트 | 관리 페이지에서 수행되는 사용자 관리 조치와 관련한 이벤트. |
| 관리 이벤트 | 카탈로그 | 서비스 카탈로그 변경과 관련한 이벤트. |
| 관리 이벤트 | 보안 보고서 관리 이벤트 | 관리 페이지에서 수행되는 보안 보고서 관리 조치와 관련한 이벤트. |
| 액세스 검토 | 액세스 검토 보고서 | 권한이 부여된 액세스에 대한 검토. |
| 변경 관리 | 소프트웨어 변경 관리 | 변경 관리 활동. |
| 키 관리 | 사용자 정의 SSL 인증서 관리 | 업로드 및 저장된 사용자 정의 SSL 인증. |
| 암호화 | 전송 중 데이터 암호화 | 구성된 전송 중 데이터 암호화. |
| 안티 바이러스 | 안티 바이러스 스캔 보고서 | 적용 중인 안티 바이러스 소프트웨어. |
| 소프트웨어 수정사항 관리 | 패치 애플리케이션 보고서 | 적용된 소프트웨어 수정사항. |
| 보안 인시던트 관리 | 보안 인시던트 조치방안 보고서 | 보안 인시던트 관리를 위한 보안 인시던트 증거. |

## 상태 보기
{: #oc_status}

{{site.data.keyword.Bluemix_notm}} 환경 및 관리 콘솔의 상태를 볼 수 있습니다.

### {{site.data.keyword.Bluemix_notm}} 환경 상태

{{site.data.keyword.Bluemix_notm}} 상태 페이지를 사용하여 {{site.data.keyword.Bluemix_notm}} 인스턴스의 상태를 모니터할 수 있습니다. **계정 및 지원** 아이콘 ![계정 및 지원](../support/images/account_support.svg)을 클릭한 후 **상태**를 선택하십시오. 

상태 페이지는 {{site.data.keyword.Bluemix_notm}}의 주요 서비스 및 {{site.data.keyword.Bluemix_notm}} 플랫폼에 영향을 미치는 주요 이벤트에 대한 알림 및 공지사항을 찾는 중심 위치입니다.알림에 대한 RSS 피드를 구독하면 따로 확인할 필요가 없습니다. 상태 페이지 및 RSS 피드 설정에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} 보기](../support/index.html#viewing-bluemix-status)를 참조하십시오.

### 관리 콘솔 상태

{{site.data.keyword.Bluemix_notm}} 환경의 초기 배치 후 환경을 관리하는 데 사용되는 컴포넌트에 대한 검증 확인이 자동으로 완료됩니다. 관리 콘솔 검증 확인 페이지로 이동하여 검증 확인이 실행된 후 컴포넌트의 상태를 확인할 수 있습니다. 페이지에 액세스하려면 <code>https://console.&lt;subdomain&gt;.bluemix.net/check</code>로 이동하십시오. 여기서 `<subdomain>`은 로컬 또는 전용 인스턴스의 이름입니다.

언제든지 검증을 실행할 수 있습니다. 검증 실행 옵션을 선택하려면 로그인해야 합니다. 사용자 추가, 조직 편집 또는 서비스 관리 중에 실패가 발생하는 경우 이 확인을 실행하여 실패하거나 연결이 끊긴 컴포넌트를 식별하십시오. 문제가 신속하게 해결되도록 확인에서 얻은 정보로 지원 티켓을 열 수 있습니다.

## 카탈로그 관리
{: #oc_catalog}

{{site.data.keyword.Bluemix_notm}} 카탈로그에서 사용자에게 표시되는 {{site.data.keyword.Bluemix_notm}} 서비스 및 스타터를 관리할 수 있습니다.**관리 &gt; 카탈로그 관리**를 클릭하십시오. 

서비스 또는 스타터 타일을 선택하여 서비스 또는 스타터 플랜 가시성을 편집하십시오. 가시성을 편집하려면 다음 옵션 중에서 선택하십시오. 

- 숨겨진 서비스 또는 스타터를 표시하여 사용자가 카탈로그에서 볼 수 있도록 하려면
**모든 플랜 사용**을 선택하십시오. 
- 서비스 또는 스타터를 {{site.data.keyword.Bluemix_notm}} 카탈로그에서
사용자에게 숨기려면 **모든 플랜 사용 안함**을 선택하십시오. 
- 개별 플랜의 가시성을 제어하려면 플랜 이름을 선택한 후 드롭 다운 메뉴를 사용하여 **모든 조직에 대해 사용**,
**모든 조직에 대해 사용 안함** 또는 **특정 조직에 대해 플랜 사용**을 선택하십시오. 

<!-- staging only start -->

### 서비스 브로커 등록
{: #servicebrokerui}

{{site.data.keyword.Bluemix_notm}} 카탈로그에 표시하려는 서비스가 있으면 서비스 브로커를 구현하고 등록해야 합니다. 브로커를 등록한 후, 로컬 또는 전용 인스턴스에서 해당 서비스에 액세스할 수 있는 조직을 선택할 수 있습니다.

서비스 브로커에 대한 작업 방법은 서비스 브로커가 관리하는 서비스 수 또는 서비스 브로커가 이미 {{site.data.keyword.Bluemix_notm}}에 등록되었는지 여부에 따라 다릅니다.

- 서비스 브로커가 하나의 서비스를 관리하는 경우, [서비스 브로커 API](http://docs.cloudfoundry.org/services/api.html){: new_window}를 구현한 후에 사용자 인터페이스를 사용하여 서비스 브로커를 등록할 수 있습니다. [하나의 서비스를 관리하는 서비스 브로커 등록](index.html#registerbrokerui)을 참조하십시오.
- 서비스 브로커가 여러 서비스를 관리하는 경우, 서비스 브로커 API를 등록한 후 서비스 브로커를 등록할 수 없습니다. 대신 cf CLI를 [{{site.data.keyword.Bluemix_notm}} 관리 CLI](../cli/plugins/bluemix_admin/index.html) 플러그인(`ba` 하위 명령)과 함께 사용하거나 [사용자 정의 서비스 API](index.html#servicebrokerapi)를 사용하십시오.
- 서비스 브로커가 이미 등록된 상태에서 서비스 브로커를 업데이트 또는 삭제하려는 경우, cf CLI를 [{{site.data.keyword.Bluemix_notm}} 관리 CLI](../cli/plugins/bluemix_admin/index.html) 플러그인(`ba` 하위 명령)과 함께 사용하거나 [사용자 정의 서비스 API](index.html#servicebrokerapi)를 사용하십시오.

#### 하나의 서비스를 관리하는 서비스 브로커 등록
{: #registerbrokerui}

다음 단계를 완료하여 서비스 브로커를 등록하십시오.

<ol>
<li><a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">Cloud Foundry 서비스 브로커 API를 구현</a>하여 사용하는 서비스와 {{site.data.keyword.Bluemix_notm}} 간의 통신을 가능하게 하십시오. 서비스 브로커 API는 {{site.data.keyword.Bluemix_notm}}에서 이용하는 REST 엔드포인트 세트입니다.<br />
<br />
<p>서비스 브로커를 구현하는 경우, <code>GET /v2/catalog</code>의 JSON 응답에서 표시하려는 서비스 정보를 포함하여 사용하는 서비스 및 서비스 플랜에 대한 정의를 제공해야 합니다. 예를 들어, Catalog (GET) 응답의 다음 샘플 JSON을 검토하십시오.</p>
<p><pre>
"services":[
   {
      "bindable":true,
      "description":"Cool Service is a data warehousing and analytics solution.",
      "id":"cool-service-id",
      "name":"coolservice",
      "tags":[
         "customer_dedicated"
      ],
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Cool company",
         "longDescription":"Cool Service is a data warehousing and analytics solution. You can quickly move your data into a next-generation columnar in-memory database and start running complex analytical queries.",
         "bullets":[
            {
               "title":"Fast and Simple",
               "description":"Cool Service uses dynamic in-memory columnar technology and innovations, such as parallel vector processing and actionable compression to rapidly scan and return relevant data."
            },
            {
               "title":"Connectivity",
               "description":"Cool Service is built to let you connect easily and to all of your services and applications. You can start analyzing your data right away with familiar tools."
            }
         ],
         "featuredImageUrl":"http://path/to/icon_64x64.png",
         "imageUrl":"http://path/to/icon_50x50.png",
         "mediumImageUrl":"http://path/to/icon_32x32.png",
         "smallImageUrl":"http://path/to/icon_24x24.png",
         "documentationUrl":"http://path/to/documentation.html",
         "instructionsUrl":"http://path/to/servicesample.md",
         "termsUrl":"http://path/to/terms_of_agreement.pdf",
         "media":[
            {
               "type":"youtube",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/youtube/video",
               "caption":"Using Cool Service in 60 Seconds"
            },
            {
               "type":"image",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/image_file.png",
               "caption":"Cool Service connects applications"
            },
            {
               "type":"video",
               "thumbnailUrl":"http://path/to/thumb.png",
               "caption":"Cool Service works with tables",
               "source":[
                  {
                     "type":"video/mp4",
                     "url":"http://path/to/video_file.mp4"
                  },
                  {
                     "type":"video/ogg",
                     "url":"http://path/to/video_file.ogg"
                  }
               ]
            }
         ]
      },
      "plans":[
         {
            "name":"smallplan",
            "description":"Dedicated schema and tablespace per service instance on a shared server. 1GB and 10GB of compressed database storage can hold up to 5GB and 50GB of uncompressed data respectively based on typical compression ratios.",
            "free":false,
            "id":"cool-service-plan-id",
            "metadata":{
               "bullets":[
                  "1 GB Min per instance. 10 GB Max per instance."
               ],
               "costs":[
                  {
                     "unitId":"INSTANCES_PER_MONTH",
                     "unit":"MONTHLY",
                     "partNumber":"D15UTLL"
                  }
               ],
               "displayName":"Small"
            }
         }
      ]
   }
]
}
</pre></p>
<p><strong>참고</strong>: 로컬 또는 전용 환경의 서비스 브로커를 작성하는 경우, 서비스 정의 JSON 파일의 "tags" 필드에 `customer_dedicated`를 지정해야 합니다.</p>
</li>
<li>서비스 브로커 API가 구현되면 <strong>관리</strong> &gt; <strong>카탈로그 관리</strong>로 이동하십시오.</li>
<li><strong>서비스 브로커 등록</strong>을 클릭하십시오.</li>
<li>다음 필드에 값을 입력하여 양식을 완료하십시오.<ul>
<li>서비스 브로커 이름</li>
<li>서비스 브로커 URL</li>
<li>서비스 브로커 사용자 이름</li>
<li>서비스 브로커 비밀번호</li>
</ul>
</li>
<li><strong>연결</strong>을 클릭하십시오.</li>
<li>사용 가능한 플랜, 아이콘 및 서비스 설명을 포함하여 서비스에 대한 정보를 검토하십시오.<br />
<p><strong>참고</strong>: 서비스에 대한 카탈로그 정보를 변경해야 하는 경우에는 서비스 브로커를 업데이트하고 양식을 채워 등록 프로세스를 다시 시작하십시오.</p>
</li>
<li><strong>등록</strong>을 클릭하십시오.</li>
<li>서비스의 모든 플랜을 사용하거나 특정 플랜만을 사용하도록 선택하십시오. 기본적으로 모든 플랜이 사용되지 않습니다.</li>
<li>모든 조직 또는 특정 조직에 대해 해당 서비스 인스턴스를 사용으로 설정하십시오.</li>
</ol>

이제 {{site.data.keyword.Bluemix_notm}} 카탈로그의 사용자 정의 서비스 카테고리에 서비스가 표시됩니다. **관리 &gt; 카탈로그 관리**로 이동하여 카탈로그에서 해당 타일을 선택하십시오. 다양한 플랜을 사용으로 설정하고 언제든지 조직에 대한 플랜 가시성을 편집할 수 있습니다.

## 조직 관리
{: #oc_organizations}

조직을 작성 및 삭제하고 조직의 관리자를 추가 또는 제거하며 할당량 사용량을 모니터링하여 비즈니스에 가장 적합한 의사결정을 내림으로써 조직을 관리할 수 있습니다.

**관리 &gt; 조직 관리**를 클릭하십시오. 

다양한 섹션을 펼치고 볼 수 있습니다. 조직에 대한 할당 플랜을 검토하고 관리할 수도 있습니다. 

### 조직 작성

새 조직을 작성하고 관리자를 추가하려면 다음 단계를 완료하십시오.

1. <strong>조직 작성</strong>을 클릭하십시오.
2. 조직의 이름을 입력하십시오.
3. 관리자로 추가할 사용자의 이름 또는 이메일을 입력하십시오. 여러 이름을 입력하고 선택하여
둘 이상의 관리자를 추가할 수 있습니다. 
4. <strong>조직 작성</strong>을 클릭하여 변경사항을 저장하고 조직을 작성하십시오. 

### 영역 작성

조직에서 영역을 작성할 수 있습니다.
예를 들어, *dev* 영역은 개발 환경으로,
*test* 영역은 테스트 환경으로, *production*
영역은 프로덕션 환경으로 작성할 수 있습니다.
그런 다음, 앱을 영역과 연관시킬 수 있습니다. 영역을 작성하려면 다음 단계를 완료하십시오.

1. **계정 및 지원** 아이콘 ![계정 및 지원 아이콘](../admin/images/account_support.svg) &gt; **조직 관리** 페이지로 이동하십시오.
2. 영역을 추가할 조직을 선택하십시오.
3. **영역 작성**을 클릭하십시오.
4. 영역 이름을 입력하십시오.
5. **작성**을 클릭하십시오.

### 할당량 모니터링

할당량 모니터링 섹션에서 해당 섹션을 펼치고
다음 정보를 볼 수 있습니다. 

- 환경 메모리 사용량. 이 섹션에는 전체 시스템 환경에 대한 메모리 사용량 세부사항이 있습니다.
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

- 조직 메모리 사용량. 이 섹션에는 조직 레벨에서 메모리 사용량의 세부사항이 있습니다. 총 할당 허용량 및
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

### 할당량 플랜 조정

조직의 할당량 플랜을 변경하려면 다음 단계를 완료하십시오.

<ol>
<li>조직 메모리 사용량 섹션의 차트에서 편집할 조직의 막대를 클릭하거나 조직 목록 섹션에서 조직의 이름을 선택하십시오. </li>
<li>조직 관리 페이지에서 할당량 플랜을 변경하고 조직의 이름을 변경하며 관리자를 추가 또는
제거할 수 있습니다. <br />
<p><strong>참고</strong>: 조직의 현재 사용량에 충분하지 않은
할당량 플랜을 선택하면 메시지가 수신됩니다. </p>
</li>
<li>조직 관리 페이지에서 변경한 사항을 저장하려면
<strong>저장</strong>을 클릭하십시오. </li>
</ol>

### 조직 목록에서 조직 관리

조직 목록 섹션에서 {{site.data.keyword.Bluemix_notm}} 환경에 있는 모든 조직을 볼 수 있으며 조직 이름을 클릭하여 개별 조직에 대해 조치를 수행할 수 있습니다.

- 조직을 삭제하려면 조치 열에서 **삭제** 아이콘 ![삭제](images/icon_trash.svg)를 클릭하십시오.
- 조직의 할당량 플랜 및 사용량을 보려면 목록에서 해당 조직의 이름을
클릭하십시오. 선택한 조직의 **조직 관리** 페이지에서 다음과 같은 사용 정보를 볼 수 있습니다.

  - 현재 사용 중인 서비스 수
  - 현재 사용 중인 라우트 수
  - 할당량 중 사용되는 양 및 현재 사용 중이 아닌 양을 표시하는 메모리 할당량 그래프
  - 사용되는 메모리 할당량에 포함되는 애플리케이션을 표시하는 애플리케이션 할당 그래프
  - 배치된 앱당 사용된 GB-시간의 3개월 보고서를 표시하는 측정된 애플리케이션 사용량 그래프. **목록 보기**를 선택하면 지난 3개월 간의 앱당 메모리 할당 및 측정된 GB-시간 사용량을 포함하여 모든 앱에 대한 데이터를 볼 수 있습니다.

- 조직의 이름을 편집하고 관리자를 추가 또는 제거하려면 목록에서 조직의 이름을 클릭하고
화면의 프롬프트를 따르십시오.

## 사용자 및 권한 관리
{: #oc_useradmin}

LDAP를 통해 회사의 사용자 레지스트리에서 {{site.data.keyword.Bluemix_notm}} 인스턴스에 사용자를 추가할 수 있습니다. 
사용자를 단독으로 또는 그룹으로 추가하고 사용자 권한을 볼 수 있습니다. 
`관리` 권한이 지정된 경우에는 다른 사용자에 대한 권한을 설정하고 관리할 수도 있습니다. **관리 &gt; 사용자 관리**를 클릭하십시오. 

사용자 관리 페이지에 로컬 또는 전용 인스턴스의 모든 사용자가 표시됩니다.
각 사용자의 권한이 표시되어 있습니다. 권한은 없음,
`관리`, `카탈로그`, `로그인`,
`보고서` 및 `사용자`일 수 있습니다. 권한을 사용으로 설정하거나
사용자에게 해당 권한의 `보기` 또는 `쓰기` 액세스(아이콘으로 표시됨)를
지정할 수 있습니다. 각 유형 및 아이콘에 대한 설명은
[권한](index.html#permissions)의 내용을 참조하십시오. 

### 사용자에 대한 작업

기존 사용자를 검색하고 사용자를 제거하고 개별 또는 그룹별로 사용자를 추가할 수 있습니다. 다음 옵션에서 선택하십시오.

* 사용자를 찾으십시오. **검색** 필드를 사용하여 테이블에서 사용자를
찾을 수 있습니다. 

* 단일 사용자를 추가합니다. `관리` 권한이나 `쓰기` 액세스가 포함된
`사용자` 권한이 있으면 사용자를 추가할 수 있습니다. 

  1. LDAP 디렉토리에서 단일 사용자를 추가하려면 **사용자 추가**를 클릭하십시오.
  2. **검색** 필드에서 사용자의 이메일 주소를 입력한 후 채워진 목록에서 사용자를 선택하십시오.
  3. 다음으로 **조직** 필드에서 조직 이름을 입력하고 채워진 목록에서 조직 이름을 선택하여 사용자를 추가할 조직을 선택하십시오.
  4. 선택한 조직에 사용자를 추가하려면 **사용자 추가**를 클릭하십시오.

  **참고**: 추가 오퍼레이션이 완료되면 사용자가 보기 및 검색이 가능하도록 테이블에 추가됩니다. 
사용자가 추가되는 경우 사용자에게는 지정된 권한이 없습니다. 

* LDAP 디렉토리에서 사용자 그룹을 추가합니다.

  1. **사용자 그룹 추가**를 클릭하십시오.
  2. **검색** 필드에서 검색할 그룹 이름을 입력하고 채워진 목록에서 그룹 이름을 선택하십시오.
  3. 다음으로 **조직** 필드에서 조직 이름을 입력하고 채워진 목록에서 조직 이름을 선택하여 사용자 그룹을 추가할 조직을 선택하십시오.
  4. 선택한 조직에 사용자 그룹을 추가하려면 **사용자 추가**를 클릭하십시오.
  **참고**: 50명이 넘는 사용자의 그룹은 백그라운드 일괄처리 작업을 통해 추가됩니다. 
추가 오퍼레이션이 완료되면 사용자 또는 그룹이 보기 및 검색이 가능하도록 테이블에 추가됩니다. 
사용자가 추가되는 경우 사용자에게는 지정된 권한이 없습니다. 

* 사용자 ID, 사용자 이메일 주소 및 사용자를 추가할 조직이 포함되어 있는 스프레드시트를 가져와서 사용자 그룹을 추가합니다.

  1. **사용자 가져오기**를 클릭하십시오.
  2. **템플리트(.CSV) 다운로드**를 클릭하여 채울 수 있는 필수 열이 있는 스프레드시트를 다운로드하거나 최소한 필수 열 헤더인 **사용자 ID**, **이메일**, **조직**을 포함하는 스프레드시트를 직접 작성하십시오.
  3. 필수 열에 사용자 값을 채우십시오. LDAP 디렉토리를 사용하지 않는 경우, 사용자 가져오기에 대해 필수 열 헤더 및 선택적 열 헤더인 **이름** 및 **성**을 사용하십시오.
  4. 파일을 저장하고 **파일 업로드**를 클릭하십시오.
 

  **참고**: 사용자 레지스트리에 사용된 값과 일치하는 사용자 ID를 입력하십시오. 스프레드시트 내에 필수 열이 모두 있으면 열 순서는 상관이 없습니다. 가져오기가 완료되면 모든 사용자가 추가되었음을 알리는 확인 메시지를 받게 됩니다. 일부 사용자에 대해서는 가져오기가 완료되었지만 다른 사용자에게는 완료되지 않은 경우 오류 메시지를 검토하여 추가할 수 없는 사용자에 대한 조치를 수행하십시오.

* 사용자 제거. `관리` 권한이 있거나 `쓰기` 액세스가 포함된
`사용자` 권한이 있으면 사용자를 제거할 수 있습니다.


    1. 사용자를 찾고 ![삭제](images/icon_trash.svg) 아이콘을 클릭하십시오.
    2. **제거**를 클릭하십시오.

### 권한
{: #permissions}

사용자에게 다음 권한을 지정할 수 있습니다. 

*표 6. 권한*

| **사용자 권한** | **설명** |       
|-----------------|-------------------|
| 관리 | `관리` 권한이 있는 사용자는 다른 사용자의 권한을 편집할 수 있습니다.  |
| 카탈로그 | `카탈로그` 권한이 있는 사용자에게는 로컬 또는 전용 인스턴스에서 사용 가능한 서비스에 대한 `보기` 또는 `쓰기`(수정) 액세스가 지정될 수 있습니다.  |  
| 로그인 | `로그인` 권한이 있는 사용자에게는 관리 페이지가 표시됩니다. 이 권한이 없는 사용자는 관리 메뉴 옵션을 볼 수 없습니다. |
| 보고서 | `보고서` 권한이 있는 사용자에게는 보안 보고서에 대한 `보기` 또는 `쓰기`(수정) 액세스가 지정될 수 있습니다.  |
| 사용자 | `사용자` 권한이 있는 사용자에게는 사용자 목록 `보기` 액세스 또는 사용자 `쓰기`(추가 또는 제거) 액세스가 지정될 수 있습니다.
이 권한은 다른 사용자에 대한 권한의 설정을 허용하지 않습니다. |


권한을 사용으로 설정하거나 사용자에게 해당 권한의 `보기` 또는 `쓰기`
액세스(다음 아이콘으로 표시됨)를 지정할 수 있습니다.

* 권한 옆의 ![사용, 선택 표시로 표시됨](images/icon_enabled.svg) 아이콘은 해당 권한을 사용함을 의미합니다.
* ![보기, 눈 모양으로 표시됨](images/icon_read.svg) 아이콘은 사용자에게 해당 권한의 `보기`(읽기 전용) 액세스가 있음을 의미합니다.
* ![쓰기, 연필로 표시됨](images/icon_write.svg) 아이콘은 사용자에게 해당 권한의 `쓰기`(편집, 추가 또는 제거) 액세스가 있음을 의미합니다.

다른 사용자의 권한 및 조직을 편집하려면 `admin` 권한이 있어야 합니다. 권한을 편집하려면 사용자를 찾고
사용자 이름을 클릭하십시오. **사용자 편집** 페이지에서 권한을 사용 또는 사용 안함으로 설정할 수 있습니다.

* 권한을 사용으로 설정하려면 목록에서 **설정**을 선택하십시오.
* 사용자에게 해당 권한의 `보기`(읽기 전용) 액세스를 허용하려면 목록에서 **읽기**를 선택하고
해당 권한의 `쓰기`(편집 또는 추가 및 제거) 액세스를 허용하려면 **쓰기**를 선택하십시오.
* 권한을 사용 안함으로 설정하려면 **해제**를 선택하십시오.

조직에서 사용자를 추가하거나 제거하려면 다음 옵션에서 선택하십시오.

* 조직에 사용자를 추가하려면 테이블에서 사용자 이름을 선택하여 **사용자 편집** 화면에 액세스하십시오. 그런 다음 검색 필드를 사용하여 조직을 찾고 목록에서 조직을 선택한 후 **저장**을 클릭하십시오.
* 조직에서 사용자를 제거하려면 테이블에서 사용자 이름을 선택하여 **사용자 편집** 화면에 액세스하십시오. 그런 다음 사용자를 제거하려는 조직에 대해 ![제거](images/icon_remove.svg)를 클릭하고 **저장**을 클릭하십시오.


## Admin REST API를 통해 사용자 관리
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

### 관리 콘솔에 로그인

`Admin` API 요청을 실행하기 전에
관리 콘솔에 로그인해야 합니다. `관리` 권한이나 `쓰기` 액세스가 포함된
`사용자` 권한이 있으면 사용자를 추가하거나 제거할 수 있습니다. 다른 사용자의 권한을 편집하려면
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

다음은 이 명령의 출력을 표시하는
예입니다.
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

### 조직 나열
{: #listingorg}

사용자를 추가할 때 조직을 지정해야 합니다. `Admin` REST API를
사용하여 모든 조직을 나열할 수 있습니다.
조직을 나열하려면 `읽기` 액세스가 있는 `사용자` 권한이
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

다음은 이 명령의 출력을 표시하는 예입니다.
```
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

### 사용자 나열
{: #listingusr}

`Admin` REST API를 사용하여 등록된 사용자를 나열함으로써
사용자가 이미 {{site.data.keyword.Bluemix_notm}}
환경에 추가되었는지 판별할 수 있습니다. 등록된 사용자를 나열하려면 `읽기` 액세스가 있는 `사용자` 권한이
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

### 사용자 추가

`Admin` REST API를 사용하여
{{site.data.keyword.Bluemix_notm}} 인스턴스에 사용자를 추가할 수 있습니다. 사용자를 추가하려면
`쓰기` 액세스가 있는 `사용자` 권한이 있어야 합니다.

한 사용자 또는 사용자 목록을 추가할 수 있습니다. 단일 조직 또는 여러 조직에
사용자를 추가할 수 있습니다. 사용자를 추가하려면 다음 정보를
제공해야 합니다. 

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
<li>JSON 파일의 컨텐츠를 다음 명령을 실행하여 사용자의 엔드포인트에 놓으십시오.
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



다음은 이 명령의 출력을 표시하는
예입니다.

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

### 사용자 제거

`Admin` REST API를 사용하여
{{site.data.keyword.Bluemix_notm}} 인스턴스에서 사용자를 제거할 수 있습니다. 사용자를 제거하려면
`쓰기` 액세스가 있는 `사용자` 권한이 있어야 합니다. 

사용자를 제거하려면 사용자의 ID를 제공해야 합니다. 다음 명령을 실행하십시오. 

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


## 사용자 정의 서비스 API
{: #servicebrokerapi}

새 서비스를 등록하거나 작성하고, 서비스를 업데이트 및 삭제할 때는 3가지 API를 사용할 수 있습니다.

모든 API는 <code>https://console.&lt;subdomain&gt;.bluemix.net/</code>를 기준으로 합니다.

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>이 값은 로컬 또는 전용 인스턴스의 이름입니다. {{site.data.keyword.Bluemix}} 인스턴스의 하위 도메인은
온보딩 중에 지정되었습니다. </dd>
</dl>

## 새 서비스 등록

새 서비스를 등록하려면 다음 API와 코드 예제를 사용하십시오.

### 라우트
{: #registerroute}

```
POST /codi/v1/serviceBrokers
```
{: screen}

### 요청
{: #registerrequest}

*표 7. 필드*

| **이름** | **설명** |
|-----------------|-------------------|
| name | 서비스 브로커의 이름입니다.  |
| auth_username | 서비스 브로커와 연결하는 데 사용하는 사용자 이름입니다.  |
| auth_password | 서비스 브로커와 연결하는 데 사용하는 비밀번호입니다.  |
| broker_url | 서비스 브로커와 연결하는 데 사용하는 URL입니다.  |
| owningOrganization | 서비스 화이트리스트를 작성하는 초기 조직입니다. |


#### 본문
{: #registerbody}

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

#### 헤더
{: #registerheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### 응답
{: #registerresponse}

#### 상태
{: #registerstatus}

```
201 Created
```
{: screen}

#### 본문
{: #registerbody2}

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

## 서비스 업데이트

서비스를 업데이트하려면 다음 API와 코드 예제를 사용하십시오.

### 라우트
{: #updateroute}

`PUT /codi/v1/serviceBrokers`
{: screen}

### 요청
{: #updaterequest}

*표 8. 필드*

| **이름** | **설명** |
|-----------------|-------------------|
| name | 서비스 브로커의 이름입니다. 서비스 작성 시 사용한 이름에서 이 이름을 변경할 수 없습니다. |
| auth_username | 서비스 브로커와 연결하는 데 사용하는 사용자 이름입니다.  |
| auth_password | 서비스 브로커와 연결하는 데 사용하는 비밀번호입니다.  |
| broker_url | 서비스 브로커와 연결하는 데 사용하는 URL입니다.  |
| owningOrganization | 서비스 화이트리스트를 작성하는 초기 조직입니다. |


#### 본문
{: #updatebody}

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

#### 헤더
{: #updateheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### 응답
{: #updateresponse}

#### 상태
{: #updatestatus}

```
201 Created
```
{: screen}

#### 본문
{: #updatebody2}

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

## 서비스 삭제

서비스를 삭제하려면 다음 API와 코드 예제를 사용하십시오.

*표 9. 매개변수*

| **이름** | **설명** |
|-----------------|-------------------|
| name | 서비스 브로커의 이름입니다. 서비스 작성 시 사용한 이름에서 이 이름을 변경할 수 없습니다. |


### 라우트

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

### 요청
{: #deleterequest}

#### 헤더
{: #deleteheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### 응답
{: #deleteresponse}

#### 상태
{: #deletestatus}

```
204 No Content
```
{: screen}

## cf CLI를 사용하여 사용자 관리
{: #usingadmincli}

{{site.data.keyword.Bluemix_notm}}
관리 CLI 플러그인과 함께 Cloud Foundry 명령행 인터페이스를 사용하여
{{site.data.keyword.Bluemix_notm}} 환경의 사용자를 관리할 수 있습니다. 예를 들어,
LDAP 레지스트리에서 사용자를 추가할 수 있습니다.

시작하기 전에 cf 명령행 인터페이스를 설치하십시오. {{site.data.keyword.Bluemix_notm}} 관리
CLI 플러그인에는 cf 버전 6.11.2 이상이 필요합니다. [Cloud Foundry 명령행 인터페이스 다운로드](https://github.com/cloudfoundry/cli/releases){: new_window}

**제한사항:** Cloud Foundry 명령행 인터페이스는
Cygwin에서는 지원되지 않습니다. Cygwin 명령행 창 외의
명령행 창에서 Cloud Foundry 명령행 인터페이스를 사용하십시오.

### {{site.data.keyword.Bluemix_notm}} 관리 CLI 플러그인 추가

cf 명령행 인터페이스가 설치된 후에 {{site.data.keyword.Bluemix_notm}}
관리 CLI 플러그인을 추가할 수 있습니다.

**참고**: 이전에 {{site.data.keyword.Bluemix_notm}} 관리 플러그인을 설치한 경우, 최신 업데이트를 가져오려면 이 플러그인을 설치 제거하고 저장소를 삭제한 후 다시 설치해야 할 수도 있습니다.

저장소를 추가하고 플러그인을 설치하려면 다음 단계를 완료하십시오.

<ol>
<li>{{site.data.keyword.Bluemix_notm}} 관리 플러그인 저장소를 추가하려면 다음 명령을 실행하십시오. <br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
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
