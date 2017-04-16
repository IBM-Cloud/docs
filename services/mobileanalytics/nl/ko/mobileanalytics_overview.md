---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}} 정보  
{: aboutmobileanalytics}

{: shortdesc}
{{site.data.keyword.mobileanalytics_full}} 서비스는 모바일 애플리케이션 개발자 및 애플리케이션 소유자에게 중요한 애플리케이션의 사용 및 성능에 관한 통찰을 제공합니다. {{site.data.keyword.mobileanalytics_short}}를 사용하면 애플리케이션 소유자 및 개발자는 사용자 측에서 발생하는 상황을 이해할 수 있으며 이러한 통찰을 사용하여 사용자와 밀접하게 관련되어 있고 엄청난 수의 모바일 애플리케이션 중에서 차별화되는 보다 나은 애플리케이션을 빌드할 수 있습니다. 

{: #overview}  
이 서비스에는 개발자 및 애플리케이션 소유자가 모바일 애플리케이션 성능을 모니터링하고 사용 통계를 보며 디바이스 로그를 검색할 수 있는 {{site.data.keyword.mobileanalytics_short}} 콘솔이 있습니다. {{site.data.keyword.mobileanalytics_short}}에서는 iOS 8+(Swift 전용) 및 Android 4+용 클라이언트 SDK를 제공합니다.

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
		<dd>{{site.data.keyword.Bluemix}}에서 서비스 인스턴스를 작성하고 프로젝트에 SDK를 추가하며 두 개의 코드 행을 애플리케이션에 붙여넣으면 다수의 사전 정의된 메트릭을 수집할 준비가 된 것입니다.</dd>
	<dt>원하는 데이터 수집</dt>
		<dd>사용자 정의 이벤트로 앱을 구성하고 앱과 상호 작용하는 방법을 검색하고 구매를 추적하고 앱 활동을 모니터하십시오.  
</dd>
<dt>한 눈에 모든 애플리케이션에 대한 메트릭 보기</dt>
	<dd>{{site.data.keyword.mobileanalytics_short}} 콘솔은 조회를 작성할 필요 없이 <!-- both -->이미 만들어진 차트<!--and custom-->를 제공합니다.</dd>
<dt>중요한 사항에 집중</dt>
	<dd>시간, 어댑터, 애플리케이션, 애플리케이션 버전, OS, OS 버전 또는 디바이스 모델을 기준으로 메트릭을 필터링하십시오.</dd>
<dt>신속한 문제 발견</dt>
	<dd>충돌 상태를 모니터링하십시오. 중요한 메트릭에 대한 경보 트리거를 설정하고 모든 REST 엔드포인트에 경보를 라우트하십시오. </dd>
<dt>문제의 근본 원인 해결</dt>
	<dd>애플리케이션에서 사용자 정의 로깅을 사용하여 로그를 자동으로 업로드하고 콘솔에서 로그를 검색하십시오. 충돌 이벤트를 드릴다운하여 스택 추적을 참조하십시오.</dd>
</dl>
 

## 메트릭 및 이벤트 사용
{: #usingmetrics}

**사전 정의된 메트릭**을 사용하여 다음과 같은 질문에 응답할 수 있습니다.

* 얼마나 많은 새 사용자가 있습니까?  
* 얼마나 많은 사용자가 내 애플리케이션을 적극적으로 사용하고 있습니까?  
* 사용자가 내 애플리케이션을 얼마나 자주 사용하고 있습니까? 
* 사용자가 하루 중 언제 내 애플리케이션을 사용합니까?  
* 내 사용자가 선호하는 디바이스 모델은 무엇입니까? 
* 레거시 운영 체제에 대한 지원을 중지해야 하는 시기는 언제입니까? 
* 어느 애플리케이션에 성능 문제가 있습니까?  

자체 **사용자 정의 이벤트**를 추가함으로써 다음과 같은 질문에 응답할 수 있습니다.  

* 가장 많이 사용되는 기능과 가장 적게 사용되는 기능은 무엇입니까?   
* 사용자가 맵에 들어가고 맵을 나가는 위치는 어디입니까?  
* 사용자가 가장 많이 보는 활동은 무엇입니까?  
* 사용자가 앱에서 워크플로우를 완료합니까(예: 변환 퍼널)?   

클라이언트 측 로그 및 사용법 데이터는 자동으로 수집되며 Mobile Analytics 서비스에 On-Demand로 전송됩니다. 개발자 및 관리자는 클라이언트 SDK에 의해 수집된 데이터를 보기 위해 {{site.data.keyword.mobileanalytics_short}} 서비스 대시보드를 사용할 수 있습니다.

## 데이터 시각화
{: data-visualization}

분석 서비스에 의해 수집된 모든 데이터는 IBM {{site.data.keyword.mobileanalytics_short}} 서비스 타일 인스턴스를 클릭하여 {{site.data.keyword.Bluemix_notm}} 대시보드로부터 액세스 가능한 {{site.data.keyword.mobileanalytics_short}} 대시보드를 통해 시각화될 수 있습니다. <!--You can also create custom charts, based on data that is collected by the analytics service in the dashboard.--> 모바일 분석 둘러보기 외에도 분석 기능에는 클라이언트 로그, 캡처된 클라이언트 충돌 데이터 및 {{site.data.keyword.mobileanalytics_short}} 서비스에 피드하는 클라이언트 API 기능 호출을 통해 명시적으로 제공하는 추가 데이터에 대한 원시 검색을 수행하는 기능이 포함됩니다. 

## {{site.data.keyword.mobileanalytics_short}} 자주 묻는 질문 
{: #faq}

<dl>
	<dt>{{site.data.keyword.mobileanalytics_full}}란 무엇입니까?</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}}는 모바일 애플리케이션의 성능과 사용 실태에 대한 실시간 통찰 및 히스토리 기반 통찰을 제공하는 서비스입니다. {{site.data.keyword.mobileanalytics_short}}를 사용하면 애플리케이션 개발자와 애플리케이션 소유자는 활성 사용자, 세션, 모바일 플랫폼, 애플리케이션 충돌의 상태동향을 모니터하여 데이터 중심의 의사결정을 내릴 수 있습니다. 사용자는 푸시 서비스 또는 내부 메시징 서비스를 포함하여, 한 번 트리거되면 모든 REST 엔드포인트에 메시지를 전송하는 선택된 메트릭에 경보를 설정할 수 있습니다. </dd>
	<dt>{{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}로 어떤 작업을 할 수 있습니까?</dt>
		<dd>모바일 애플리케이션 제품 관리자는 얼마나 많은 사용자가 본인의 애플리케이션을 사용하는지(사용자 메트릭)와 그러한 사용자가 언제 애플리케이션을 사용하는지(세션 메트릭)를 확인할 수 있습니다. 이 정보는 시계열로 제공되고 실시간으로 업데이트되므로 애플리케이션에 대한 변경사항이 미치는 영향을 볼 수 있습니다. 특정 애플리케이션 버전 또는 운영 체제를 표시하도록 필터링하여 지원중단 및 우선순위에 관한 결정을 내릴 수 있습니다. </dd>
		<dd>모바일 애플리케이션 마케팅 담당자는 사용자 및 세션 메트릭을 사용하여 시간 경과에 따른 변화를 관찰하고 이벤트 날짜와 연관시킴으로써 고객 참여를 모니터하고 고객 이탈을 관리하며 모바일 애플리케이션 마케팅 노력의 효율성을 평가할 수 있습니다. </dd>
		<dd>모바일 애플리케이션 개발자는 모바일 애플리케이션 성능 문제로 인해 사용자가 불편을 겪고 애플리케이션의 평판에 피해가 가기 전에 충돌 메트릭을 사용하여 그러한 문제를 발견하고 해결할 수 있습니다. Analytics 콘솔에서 충돌 개수 및 충돌 비율을 모두 모니터링할 수 있으며 가장 많은 사용자에게 영향을 주는 충돌을 우선 순위 지정할 수 있습니다. 충돌이 주어진 임계값을 초과할 때 자동화된 조치를 취하거나 알림을 보내도록 경보를 설정할 수 있으며, 충돌 인스턴스에서 드릴 다운하여 디바이스 로그와 애플리케이션 스택 추적을 확인함으로써 문제를 해결할 수 있습니다. </dd>
	<dt>Mobile Analytics를 사용하려면 데이터 분석가 스킬이 필요합니까?</dt>
		<dd>아니오, {{site.data.keyword.mobileanalytics_short}}는 비즈니스 이해 당사자와 애플리케이션 개발자를 위한 바로 사용이 가능한 Analytics 콘솔을 제공합니다. 조회 스킬도 필요하지 않습니다. </dd>
	<dt>분석 데이터에서 사용자 정의 조회를 실행할 수 있습니까?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}}에서 사용자 정의 조회를 할 수 없지만 향후 이 기능을 사용할 수 있도록 검토 중입니다. </dd>
	<dt>내 애플리케이션을 어떻게 {{site.data.keyword.mobileanalytics_short}}에 연결합니까?</dt>
		<dd>[iOS 또는 Android용 오픈 소스 SDK를 다운로드하거나](install-client-sdk.html) 기타 플랫폼용 {{site.data.keyword.mobileanalytics_short}} [REST API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/)를 사용하십시오. </dd>
	<dt>어느 Bluemix 리젼에서 {{site.data.keyword.mobileanalytics_short}}를 사용할 수 있습니까?</dt>
		<dd>현재 Mobile Analytics는 미국 남부와 영국에서 사용할 수 있습니다. 다른 지역에서도 제공할 계획이지만 아직 시기가 정해지지 않았습니다. </dd>
	<dt>이 서비스의 요금은 얼마입니까?</dt>
		<dd>매달 수집되는 처음 1억 개의 이벤트는 무료이므로 이벤트 가격은 1억 개당 $1입니다.</dd>
	<dt>이벤트란 무엇입니까?</dt>
		<dd>현재 보고되는 이벤트에는 애플리케이션 세션 시작, 애플리케이션 세션 종료(애플리케이션 충돌 포함), 경보 알림 및 로그 입력이 있습니다. </dd>
	<dt>월별 서비스 비용을 어떻게 산정할 수 있습니까?</dt>
		<dd>클라이언트 계정별로 서비스에 전송되는 이벤트 수에 따라 가격이 책정되므로 가격 산정은 이벤트 수의 산정을 의미합니다.   
<p>
청구되는 가격은 {{site.data.keyword.mobileanalytics_short}}에 연결한 모든 애플리케이션의 이벤트 합계입니다. 하나의 애플리케이션의 경우, 이벤트 수는 애플리케이션 내에서 구현한 인스트루먼테이션 등급, 사용자 수 및 사용자의 적극성 정도에 따라 달라집니다.    
</p>
<p>
사용량을 산정하려면 다음 공식을 사용하십시오.
앱당 월별 이벤트 수 = (일별 사용자 수)(일별 사용자당 세션 수)(월별 일 수)(세션당 이벤트 수)
</p>
<p>
세션당 이벤트 수는 개발자가 애플리케이션에 구성한 경보 정의, 로그 캡처, 사용자 정의 분석 및 네트워크 호출 대상에 따라 2개에서 수백 개까지 매우 광범위할 수 있습니다.
</p>
	<dt>얼마나 오랫동안 분석 데이터를 유지할 수 있습니까?</dt>
		<dd>데이터는 30일 이상 보관됩니다. </dd>
	<dt>데이터를 {{site.data.keyword.mobileanalytics_short}} 콘솔에 표시하는 데 얼마나 시간이 걸립니까?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} 콘솔의 데이터는 거의 실시간이며 이는 데이터가 실제 이벤트 발생 후 몇 초 내에 표시됨을 의미합니다.  </dd>
	<dt>MobileFirst Platform Foundation에서 발견된 Mobile Analytics와 {{site.data.keyword.mobileanalytics_full}} 사이의 차이점은 무엇입니까?</dt>
		<dd>두 콘솔에서 사용자 및 세션은 매우 유사하지만 MobileFirst Platform Foundation에서 제공하는 분석은 클라이언트가 자체 분석 클러스터 온프레미스를 관리할 수 있는 추가 메트릭 및 설정을 포함합니다. 또한 MobileFirst Platform Foundation 분석 콘솔에서는 어댑터와 어댑터 프로시저에 대한 메트릭을 세분화할 수 있는 반면, {{site.data.keyword.mobileanalytics_short}} 서비스에서는 이러한 메트릭이 네트워크 요청 차트와 테이블로 통합됩니다. </dd>
	<dt>MobileFirst Platform Foundation 온프레미스를 앱 개발에 사용 중이지만 자체 분석 클러스터를 호스트할 의향이 없습니다. 대신 {{site.data.keyword.mobileanalytics_full}}를 사용해도 됩니까?</dt>
		<dd>예. 다음과 같은 몇 개의 옵션이 있습니다. MobileFirst Platform Foundation 7.x 또는 8.0을 사용하고 앱이 MobileFirst Platform SDK로 인스트루먼트된 경우에는 {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}에 분석 데이터를 보고하도록 MobileFirst 서버를 구성할 수 있습니다. [Mobile Analytics 및 Mobile Foundation Bluemix 서비스 구성 ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/){: new_window} 블로그 포스트에서 세부사항을 읽으십시오. 또는, {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} SDK를 사용하여 앱을 인스트루먼트하고 보고서를 {{site.data.keyword.mobileanalytics_short}} 서비스에 직접 보고할 수 있습니다. </dd>
	<!-- <dt>My instance of  {{site.data.keyword.mobileanalytics_short}} does not look like the screen shots in the catalog. What's going on?</dt> -->
		<!-- <dd>Most likely you are using the Classic view interface for {{site.data.keyword.Bluemix_notm}}. Classic view is deprecated, so {{site.data.keyword.mobileanalytics_short}} runs best in the new {{site.data.keyword.Bluemix_notm}} interface. If you are in Classic view, you will see a link in the {{site.data.keyword.Bluemix_notm}} header that says <strong>Try the new {{site.data.keyword.Bluemix_notm}}</strong>. Click that link to use the new interface.</dd> -->
</dl>


# 관련 링크
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [Android SDK ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window} 
* [iOS SDK ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}

<!-- {:elementKind="article" id="rellinks"} -->
