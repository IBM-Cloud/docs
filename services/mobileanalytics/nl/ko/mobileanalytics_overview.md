---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# {{site.data.keyword.mobileanalytics_short}} 정보  
{: aboutmobileanalytics}
마지막 업데이트 날짜: 2016년 8월 29일
{: .last-updated}

{: shortdesc}
{{site.data.keyword.mobileanalytics_full}} 서비스는 모바일 앱 개발자 및 소유자를 위한 핵심적인 앱 사용 및 성능 통찰을 제공합니다. 앱 소유자 및 개발자는 {{site.data.keyword.mobileanalytics_short}}를 사용하여 사용자 측에서 발생한 상황을 이해할 수 있으며 이 통찰을 사용하여 사용자와 밀접하게 관련되었으며 모바일 앱의 세계에서 돋보이는 더 나은 앱을 빌드할 수 있습니다. 

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
	<!--<dt>Collect any data you want</dt>-->
		<!--<dd>Instrument apps with custom events, discover how users are interacting with your app, track purchases, and monitor app activity.  
</dd>-->
<dt>한 눈에 모든 앱에 대한 메트릭 보기</dt>
	<dd>{{site.data.keyword.mobileanalytics_short}} 콘솔은 조회를 작성할 필요 없이 <!-- both -->이미 만들어진 차트<!--and custom-->를 제공합니다.</dd>
<dt>중요한 사항에 집중</dt>
	<dd>시간, 어댑터, 앱, 앱 버전, OS, OS 버전 또는 디바이스 모델 기준으로 메트릭을 필터링하십시오.</dd>
<dt>신속한 문제 발견</dt>
	<dd>충돌 상태를 모니터링하십시오. 중요한 메트릭에 대한 경보 트리거를 설정하고 모든 REST 엔드포인트에 경보를 라우트하십시오. </dd>
<dt>문제의 근본 원인 해결</dt>
	<dd>앱 내의 사용자 정의 로깅을 사용하여 로그를 자동으로 업로드하고 콘솔에서 검색하십시오. 충돌 이벤트를 드릴다운하여 스택 추적을 참조하십시오.</dd>
</dl>
 

## 메트릭 및 이벤트 사용
{: #usingmetrics}

**사전 정의된 메트릭**을 사용하여 다음과 같은 질문에 응답할 수 있습니다.

* 얼마나 많은 새 사용자가 있습니까?  
* 얼마나 많은 사용자가 내 앱을 적극적으로 사용하고 있습니까?  
* 사용자가 내 앱을 얼마나 자주 사용하고 있습니까? 
* 사용자가 언제 내 앱을 사용합니까?  
* 내 사용자가 선호하는 디바이스 모델은 무엇입니까? 
* 레거시 운영 체제에 대한 지원을 중지해야 하는 시기는 언제입니까? 
* 어떤 앱에 성능 문제가 있습니까?  

<!--By adding your own **custom events** you can answer questions like:--> 

<!--* What features are used most and least?-->  
<!--* Where are users entering and leaving my app?-->  
<!--* What activities are users viewing most? --> 
<!--* Are users completing workflows in the app (for example, conversion funnels)? -->  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

## {{site.data.keyword.mobileanalytics_short}} 자주 묻는 질문 
{: #faq}

<dl>
	<dt>{{site.data.keyword.mobileanalytics_full}}란 무엇입니까?</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}}는 모바일 앱의 성능과 사용 실태에 대한 실시간 및 히스토리 통찰을 제공하는 서비스입니다. {{site.data.keyword.mobileanalytics_short}}를 사용하여 앱 개발자와 앱 소유자는 활성 사용자, 세션, 모바일 플랫폼, 앱 충돌에서 상태동향을 모니터링함으로써 데이터 중심의 의사결정을 내릴 수 있습니다. 사용자는 푸시 서비스 또는 내부 메시징 서비스를 포함하여, 한 번 트리거되면 모든 REST 엔드포인트에 메시지를 전송하는 선택된 메트릭에 경보를 설정할 수 있습니다. </dd>
	<dt>{{site.data.keyword.Bluemix_notm}}용 {{site.data.keyword.mobileanalytics_short}} beta로 어떤 작업을 할 수 있습니까? </dt>
		<dd>모바일 앱 제품 관리자라면 얼마나 많은 사람들의 귀하의 앱을 사용하는지(사용자 메트릭)와 이를 언제 사용하는지(세션 메트릭)를 확인할 수 있습니다.이 정보는 시계열로 제공되고 실시간으로 업데이트되므로 앱을 변경했을 때 영향을 볼 수 있습니다. 특정 앱 버전 또는 운영 체제를 보도록 필터링하여 지원중단 및 우선순위 결정을 내릴 수 있습니다. </dd>
		<dd>모바일 앱 마케터라면 사용자 및 세션 메트릭을 사용하여, 시간 경과에 따른 변화를 관찰하고 이벤트 날짜를 연관시켜 모바일 앱 마케팅의 효과를 평가하고 참여를 모니터하며 이탈을 관리할 수 있습니다. </dd>
		<dd>모바일 앱 개발자라면 충돌 메트릭을 사용하여 모바일 앱 성능 문제로 인해 사용자가 불편을 겪고 앱의 평판에 피해가 가기 전에 그러한 문제를 발견하여 해결할 수 있습니다. Analytics 콘솔에서 충돌 개수 및 충돌 비율을 모두 모니터링할 수 있으며 가장 많은 사용자에게 영향을 주는 충돌을 우선 순위 지정할 수 있습니다. 충돌이 주어진 임계값을 초과할 때 자동화된 조치를 취하거나 알림을 보내도록 경보를 설정하고 디바이스 로그와 앱 스택 추적을 보기 위해 충돌 인스턴스를 세부적으로 파악하여 문제를 해결할 수 있습니다. </dd>
	<dt>Mobile Analytics를 사용하려면 데이터 분석가 스킬이 필요합니까?</dt>
		<dd>아니오, {{site.data.keyword.mobileanalytics_short}}는 비즈니스 이해 당사자와 앱 개발자를 위한 바로 사용이 가능한 Analytics 콘솔을 제공합니다. 조회 스킬도 필요하지 않습니다. </dd>
	<dt>분석 데이터에서 사용자 정의 조회를 실행할 수 있습니까?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} beta에서는 사용자 정의 조회를 할 수 없지만 향후 이 기능에 대해 고려하고 있습니다. </dd>
	<dt>내 앱을 어떻게 {{site.data.keyword.mobileanalytics_short}}에 연결합니까?</dt>
		<dd>[iOS 또는 Android용 오픈 소스 SDK를 다운로드하거나](install-client-sdk.html) 기타 플랫폼용 {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.stage1.ng.bluemix.net/analytics-service/)를 사용하십시오. </dd>
	<dt>어느 Bluemix 리젼에서 {{site.data.keyword.mobileanalytics_short}}를 사용할 수 있습니까?</dt>
		<dd>이 글을 쓰는 현재 Mobile Analytics는 남미와 영국에서 사용 가능합니다. 다른 리젼의 사용 가능성은 계획되어 있지만 시간 범위는 아직 결정되지 않았습니다. </dd>
	<dt>이 서비스의 요금은 얼마입니까?</dt>
		<dd>베타 서비스는 무료입니다. </dd>
	<dt>얼마나 오랫동안 분석 데이터를 유지할 수 있습니까?</dt>
		<dd>베타의 경우 데이터가 최소 30일 보관됩니다. </dd>
	<dt>데이터를 {{site.data.keyword.mobileanalytics_short}} 콘솔에 표시하는 데 얼마나 시간이 걸립니까?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} 콘솔의 데이터는 거의 실시간이며 이는 데이터가 실제 이벤트 발생 후 몇 초 내에 표시됨을 의미합니다.  </dd>
	<dt>MobileFirst Platform Foundation에서 발견된 Mobile Analytics와 {{site.data.keyword.mobileanalytics_full}} 사이의 차이점은 무엇입니까?</dt>
		<dd>두 콘솔에서 사용자 및 세션은 매우 유사하지만 MobileFirst Platform Foundation에서 제공하는 분석은 클라이언트가 사내 구축형 자체 분석 클러스터를 관리할 수 있는 추가 메트릭 및 설정을 포함합니다. 또한 MobileFirst Platform Foundation 분석 콘솔은 어댑터와 어댑터 프로시저에 대한 메트릭에서 벗어나지만 {{site.data.keyword.mobileanalytics_short}} 서비스에서는 이러한 메트릭을 {{site.data.keyword.mobileanalytics_short}} 서비스(베타 이후)의 네트워크 요청 차트와 테이블로 통합할 계획입니다. </dd>
	<dt>사내 구축형 MobileFirst Platform Foundation을 앱 개발에 사용 중이지만 자체 분석 클러스터를 호스트할 의향이 없습니다. 대신 {{site.data.keyword.mobileanalytics_full}}를 사용해도 됩니까?</dt>
		<dd>예. 다음과 같이 두 개의 옵션이 있습니다. MobileFirst Platform Foundation 7.x 또는 8.0을 사용하고 사용자의 앱이 MobileFirst Platform SDK로 인스트루먼트된 경우에는 {{site.data.keyword.Bluemix_notm}}용 {{site.data.keyword.mobileanalytics_short}}에 분석 데이터를 보고하기 위해 MobileFirst 서버를 구성할 수 있습니다. [Mobile Analytics 및 Mobile Foundation Bluemix 서비스 구성](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/) 블로그 포스트에서 세부사항을 읽으십시오. 또는, {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} SDK를 사용하여 앱을 인스트루먼트하고 보고서를 {{site.data.keyword.mobileanalytics_short}} 서비스에 직접 보고할 수 있습니다. </dd>
	<dt>{{site.data.keyword.mobileanalytics_short}}를 사용하려고 시도하고 있는데 내 차트가 있어야 할 영역이 공백으로 표시됩니다. 어떻게 된 일입니까?</dt>
		<dd>가장 큰 이유는 {{site.data.keyword.Bluemix_notm}}용 클래식 뷰 인터페이스를 사용하기 때문입니다. 클래식 뷰는 더 이상 사용되지 않으며 {{site.data.keyword.mobileanalytics_short}} beta는 새로운 {{site.data.keyword.Bluemix_notm}} 인터페이스에서 실행됩니다. 클래식 뷰를 사용하면 "새 {{site.data.keyword.Bluemix_notm}} 시도"라는 {{site.data.keyword.Bluemix_notm}} 헤더의 링크를 보게 됩니다. 링크를 클릭하여 새 인터페이스를 사용하십시오. </dd>
</dl>


# 관련 링크
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)  
* [iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  

<!-- {:elementKind="article" id="rellinks"} -->
