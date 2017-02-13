---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-19"

---

# {{site.data.keyword.mobilefirstbp}} 스타터 표준 유형에서 모바일 앱 작성
{: #try_mobile}

각각의 {{site.data.keyword.Bluemix}} 모바일 서비스를 개별적으로 사용할 수 있습니다. 또한 이점을 극대화하기 위해 {{site.data.keyword.mobilefirstbp}} 스타터 표준 유형을 사용하여 모두 함께 사용할 수도 있습니다.

시작하려면 {{site.data.keyword.mobilefirstbp}} 스타터를 사용하여 앱을 작성하십시오. 표준 유형을 통해 다음 조치를 완료할 수 있습니다.

* 템플리트 애플리케이션을 사용하여 Node.js 런타임을 작성합니다. 이 애플리케이션을 사용하여 RESTful API와 정적 파일 같은 서버 측 기능을 제공할 수 있습니다. <!-- You can read more about operating this application in the Developing Mobile Backend section.-->
* 각 {{site.data.keyword.Bluemix_notm}} 모바일 서비스의 인스턴스를 프로비저닝하고 Node.js 애플리케이션에 서비스를 바인드합니다.

<!--
<img src="images/mf_boiler_icon.png" alt="Bluemix mobile services" width="500"> {{site.data.keyword.mobilefirstbp}} Starter boilerplate
-->

{{site.data.keyword.mobilefirstbp}} 스타터 표준 유형을 사용하여 앱을 작성한 후, 각 서비스의 Hello Bluemix 샘플을 가져오거나 기존 앱에서 {{site.data.keyword.Bluemix_notm}} 서비스를 사용하도록 구성할 수 있습니다.


## 서비스 개요
{: #services-overview}
{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} 스타터 표준 유형을 사용하여 {{site.data.keyword.Bluemix_notm}} 모바일 서비스를 모두 함께 사용하거나 {{site.data.keyword.Bluemix_notm}} 카탈로그에서 개별 서비스를 사용할 수 있습니다. 다음 다이어그램은 {{site.data.keyword.Bluemix_notm}} 모바일 서비스의 컴포넌트에 대한 개요를 제공합니다.

![{{site.data.keyword.Bluemix_notm}} 모바일 서비스 아키텍처](images/bms_architecture.jpg)

<table summary="이 표는 {{site.data.keyword.Bluemix_notm}} 모바일 서비스에 대해 설명합니다.">
<caption>표 1. {{site.data.keyword.Bluemix_notm}} 및 엔터프라이즈 시스템</caption>
<th>{{site.data.keyword.Bluemix_notm}}</th>
<th>엔터프라이즈 시스템</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Node.js 런타임 아이콘"><b>Node.js</b> <br/> 템플리트 앱을 호스트하는 Node.js 런타임은 {{site.data.keyword.mobilefirstbp}} 스타터 표준 유형의 일부로 제공됩니다. 템플리트 애플리케이션을 사용하여 RESTful API 및 정적 파일과 같은 서버 측 기능을 제공할 수 있습니다. <br/>예를 들어, 회사의 기존 인프라에 있는 REST API와 연결하거나 사용자 정의 로직 처리를 위해 Node.js 애플리케이션을 확장할 수 있습니다. {{site.data.keyword.Bluemix_notm}}에 작성하는 각 앱의 앱 ID는 고유합니다. 모바일 앱에서 이 ID를 SDK와 함께 사용하여 해당 애플리케이션에 연관된 서비스에 액세스할 수 있습니다. 앱 ID는 측정과 로깅 같은 공통 기능의 컨텍스트로서 플랫폼에서 사용됩니다.
<!--You can read more about operating this application in the "Developing Mobile Backend" section.--></td>
<td valign="top"><b>정보 제공자</b> <br/>{{site.data.keyword.Bluemix_notm}}에서 호스팅되는 Node.js 런타임을 사용하여 모든 유형의 정보 제공자에 연결할 수 있습니다.
<ul>
	<li>엔터프라이즈 백엔드</li>
	<li>데이터베이스 </li>
	<li>기타 호스팅된 써드파티 서비스 </li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/authentication_icon.png" alt="{{site.data.keyword.amashort}} 서비스 아이콘"> <b>{{site.data.keyword.amashort}}</b><br/>{{site.data.keyword.amafull}} 서비스를 사용하여 {{site.data.keyword.Bluemix_notm}}에 호스팅되는 Node.js 및 Java for Liberty 애플리케이션을 보호할 수 있습니다. {{site.data.keyword.amashort}} SDK로 모바일 앱을 구성하면 Node.js 또는 {{site.data.keyword.Bluemix_notm}} 모바일 서비스에 액세스하는 사용자에게 로그인을 요구할 수 있습니다. <!-- In addition to security capabilities, {{site.data.keyword.amashort}} also gathers analytics data, so that you can monitor your mobile application performance and collect client logs and usage statistics.--> </td>
<td valign="top"><b>사용자 ID 제공자</b> <br/>다음 ID 제공자를 사용할 수 있습니다. <ul><li>Facebook</li><li>Google</li><li> 사용자 정의</li></ul></td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}} 서비스 아이콘"> <b>{{site.data.keyword.mobilepushshort}}</b><br/>{{site.data.keyword.mobilepushfull}} 서비스는 모바일(iOS 및 Android) 플랫폼 및 웹 브라우저 애플리케이션을 대상으로 하는 푸시 알림을 전송하고 관리하는 통합 플랫폼을 제공합니다. 이 서비스는 디바이스, 디바이스 플랫폼, 브라우저에 대한 애플리케이션 사용자의 맵핑을 관리하고 구독자에게 푸시 알림을 디스패치하는 작업을 처리합니다. 이 서비스를 사용하면 고객에게 푸시 알림을 기반으로 하는 태그(또는 주제), 유니캐스트(사용자 ID, 디바이스 ID 기반), 브로드캐스트를 보낼 수 있습니다. </td>
<td valign="top"><b>푸시 서비스 제공자</b><ul><li>Apple Push Notifications Service</li><li>FCM(Firebase Cloud Messaging)</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Cloudant 서비스 아이콘"><b>Cloudant NoSQLDB</b><br/> Cloudant는 NoSQL DBaaS(Database as a Service)입니다. 이는 처음부터 글로벌하게 확장 가능하고, 중단 없이 실행되며, JSON, 전체 텍스트 및 지리공간과 같은 다양한 유형의 데이터를 처리하도록 빌드되었습니다. </td>
<td>Cloudant.com</td>
</tr>
</table>
