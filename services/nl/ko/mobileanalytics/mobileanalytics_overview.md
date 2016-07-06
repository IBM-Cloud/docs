---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# {{site.data.keyword.mobileanalytics_short}} 정보  
{: aboutmobileanalytics}
*마지막 업데이트 날짜: 2016년 4월 21일*
{: .last-updated}

{: shortdesc}
{{site.data.keyword.mobileanalytics_full}} 서비스는 모바일 앱 개발자 및 소유자를 위한 핵심적인 앱 사용 및 성능 통찰을 제공합니다. 앱 소유자 및 개발자는 {{site.data.keyword.mobileanalytics_short}}를 사용하여 "사용자 측"에서 발생한 상황을 이해할 수 있으며 이 통찰을 사용하여 사용자와 밀접하게 관련되었으며 모바일 앱의 세계에서 돋보이는 더 나은 앱을 빌드할 수 있습니다. 

{: #overview}  
서비스에는 개발자 및 앱 소유자가 모바일 애플리케이션 성능을 모니터링하고 사용 통계를 보고 디바이스 로그를 검색할 수 있는 {{site.data.keyword.mobileanalytics_short}} 콘솔이 포함됩니다. {{site.data.keyword.mobileanalytics_short}}에서는 iOS 8+(Swift 전용) 및 Android 4+용 클라이언트 SDK를 제공합니다.

<!-- Mobile Analytics Server SDKs - set of server SDKs to protect resources that are-->
<!--hosted on {{site.data.keyword.Bluemix_notm}}. Currently supported runtimes are-->
<!--Node.js and Java for Liberty.-->

{{site.data.keyword.mobileanalytics_short}} 서비스를 사용하여 다음을 수행할 수 있습니다.
<!-- and includes the following capabilities: -->
<!-- * Near real-time analytics for client activity. Exp -->
<!--* Network latency analytics. GA only -->
<!-- * Client log search and download. Exp -->
<!--* Server log search and download. GA only -->
<!-- Crash and stack trace search. Exp -->

<dl>
	<dt>즉각적 통찰 얻기</dt>
		<dd>실시간으로 성능 및 사용 메트릭 보기</dd>
	<dt>신속한 구현</dt>
		<dd>{{site.data.keyword.Bluemix}}에서 서비스 인스턴스를 작성하고 SDK를 프로젝트에 추가하고 코드의 두 라인을 사용자의 앱에 붙여넣으면 수많은 사전 정의된 메트릭을 수집할 준비가 된 것입니다.</dd>
	<dt>원하는 데이터 수집</dt>
		<dd>사용자 정의 이벤트를 사용하여 앱을 인스트루먼트하고 사용자가 앱과 상호작용하는 방법을 검색하고 구매를 추적하고 앱 활동을 모니터링하십시오.  
</dd>
<dt>한 눈에 모든 앱에 대한 메트릭 보기</dt>
	<dd>{{site.data.keyword.mobileanalytics_short}} 콘솔은 조회를 작성할 필요 없이 이미 만들어진 차트 및 사용자 정의 차트 둘 다를 제공합니다.</dd>
<dt>중요한 사항에 집중</dt>
	<dd>시간, 어댑터, 앱, 앱 버전, OS, OS 버전 또는 디바이스 모델 기준으로 메트릭을 필터링하십시오.</dd>
<dt>신속한 문제 발견</dt>
	<dd>충돌 상태를 모니터링하십시오. 중요한 메트릭에 대한 경보 트리거를 설정하고 모든 REST 엔드포인트에 경보를 라우트하십시오. </dd>
<dt>문제의 근본 원인 해결</dt>
	<dd>앱 내의 사용자 정의 클라이언트 로깅을 사용하여 로그를 자동으로 업로드하고 콘솔에서 검색하십시오. 충돌 이벤트를 드릴다운하여 스택 추적을 참조하십시오.</dd>
</dl>
 

## 메트릭 및 이벤트 사용
{: #usingmetrics}

**사전 정의된 메트릭**을 사용하여 다음과 같은 질문에 응답할 수 있습니다.

*얼마나 많은 새 사용자가 있습니까?*  
*얼마나 많은 사용자가 내 앱을 적극적으로 사용하고 있습니까?*  
*사용자가 내 앱을 얼마나 자주 사용하고 있습니까?*  
*사용자가 언제 내 앱을 사용합니까?*  
*내 사용자가 선호하는 디바이스 모델은 무엇입니까?*  
*레거시 운영 체제에 대한 지원을 중지해야 하는 시기는 언제입니까?*  
*어느 앱에 성능 문제가 있습니까?*  

자신의 **사용자 정의 이벤트**를 추가하여 다음과 같은 질문에 응답할 수 있습니다.  

*가장 많이, 가장 최근에 사용된 기능은 무엇입니까?*  
*사용자가 어디에서 내 앱을 시작하고 중지합니까?*  
*사용자가 가장 많이 보는 활동은 무엇입니까?*  
*앱에서 워크플로우가 경쟁하고 있습니까?(예: 단계별 변환)*  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

># 관련 링크 {:class="linklist"}
<!-->## 학습서 및 샘플 {:id="samples"}-->
<!-->* [Link1](https://github.com/)-->
>
># 관련 링크 {:class="linklist"}
>## 관련 링크 {:id="general"}
## SDK
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core )  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  
>
>{:elementKind="article" id="rellinks"}
