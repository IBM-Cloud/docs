# 모바일 앱 작성
{: #mobile}

{{site.data.keyword.Bluemix_notm}} Mobile Services를 사용하여 사전 빌드되어 관리되고 확장 가능한 클라우드 서비스를 모바일 애플리케이션으로 IT 참여와 관계없이 통합할 수 있습니다. 복잡한 백엔드 인프라를 관리하는 대신
모바일 앱을 빌드하는 데 집중할 수 있습니다. 

<table><caption>표 1. Bluemix Mobile Services 표준 유형</caption>
<tr>
	<td>각 Bluemix Mobile Services는 개별적으로 사용할 수 있습니다. 함께 사용하면 이점을 극대화할 수도 있습니다. 시작하려면 Bluemix Mobile Services 표준 유형을 사용하여 앱을 작성하십시오. 이 표준 유형을 사용하면 다음을 수행할 수 있습니다.
		<ul>
			<li>템플리트 애플리케이션을 사용하여 Node.js 런타임을 작성합니다. 이 애플리케이션을 사용하여 RESTful API 및 정적 파일과 같은 서버 측 기능을 제공할 수 있습니다. 이 애플리케이션을 운영하는 데 대한 자세한 정보는 모바일 백엔드 개발 섹션에 있습니다. </li>
			<li>
각 Bluemix Mobile Services의 인스턴스를 프로비저닝하고 Node.js 애플리케이션에 서비스를 바인드합니다. </li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Bluemix mobile services" width="500"> Bluemix Mobile Services 표준 유형 </td>
</tr>
</table>

Bluemix Mobile Services 표준 유형을 사용하여 앱을 작성한 다음 각 서비스의 HelloWorld 샘플을 가져오거나 Bluemix 서비스를 사용하도록 기존 앱의 인스트루먼테이션을 시작할 수 있습니다.


## 서비스 개요
{: #services-overview}
Bluemix Mobile Services 표준 유형을 사용하여 Bluemix Mobile Services를 모두 함께 사용하거나 Bluemix 카탈로그에서 개별 서비스를 사용할 수 있습니다. 다음 다이어그램에는 Bluemix Mobile Services의 모든 컴포넌트가 개요되어 있습니다.

![Bluemix Mobile Services 아키텍처](images/bms_architecture.jpg)

<table>
<caption>표 2. Bluemix 및 엔터프라이즈 시스템</caption>
<th>Bluemix</th>
<th>엔터프라이즈 시스템</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Node.js 런타임 아이콘"><b>Node.js</b> <br/> 템플리트 앱을 호스트하는 Node.js 런타임은 Bluemix Mobile Services 표준 유형의 일부로 제공됩니다. 템플리트 애플리케이션을 사용하여 RESTful API 및 정적 파일과 같은 서버 측 기능을 제공할 수 있습니다. <br/>예를 들어, 회사의 기존 인프라에 있는 REST API와 연결하거나 사용자 정의 로직 처리를 위해 Node.js 애플리케이션을 확장할 수 있습니다. Bluemix에서 작성하는 각 앱에는 고유 앱 ID가 있습니다. 모바일 앱에서 이 ID를 SDK와 함께 사용하여 해당 애플리케이션에 연관된 서비스에 액세스할 수 있습니다. 앱 ID는 측정 및 로깅과 같은 공통 기능에 대한 컨텍스트로 플랫폼에서 사용합니다. 이 애플리케이션을 운영하는 데 대한 자세한 정보는 "모바일 백엔드 개발" 섹션에 있습니다. </td>
<td valign="top"><b>정보 제공자</b> <br/>모든 유형의 정보 제공자에 연결하기 위해 Bluemix에서 호스트하는 Node.js 런타임을 사용할 수 있습니다.
<ul>
	<li>엔터프라이즈 백엔드</li>
	<li>데이터베이스 </li>
	<li>기타 호스트된 써드파티 서비스 </li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="Mobile Client Access 서비스 아이콘"> <b>Mobile Client Access</b><br/>IBM Mobile Client Access for Bluemix 서비스를 사용하여 Bluemix에서 호스트되는 Node.js 및 Java for Liberty 애플리케이션을 보호하십시오. Mobile Client Access SDK로 모바일 앱을 인스트루먼테이션하여 사용자가 Node.js나 Bluemix Mobile Services에 액세스하려면 로그인하도록 설정할 수 있습니다. 모바일 앱 성능을 모니터하고 클라이언트 로그 및 사용 통계를 수집할 수 있도록 Mobile Client Access에서 보안 기능 외에도 분석 데이터를 수집합니다.</td>
<td valign="top"><b>사용자 ID 제공자</b> <br/>다음 ID 제공자를 사용할 수 있습니다. <ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="푸시 알림 서비스 아이콘"> <b>푸시 알림</b><br/>IBM Push Notifications for Bluemix 서비스에서는 iOS 및 Android 플랫폼을 대상으로 하는 모바일 푸시 알림을 전송하고 관리하는 통합 플랫폼을 제공합니다. 이 서비스에서는 디바이스 및 디바이스 플랫폼에 대한 애플리케이션 사용자의 맵핑을 관리하고 디바이스에 푸시 알림을 디스패치하는 작업을 처리합니다. 이 서비스를 사용하면 푸시 알림을 기반으로 모바일 애플리케이션 사용자에 브로드캐스트, 유니캐스트(userID, deviceID 기반) 및 태그(또는 주제)를 보낼 수 있습니다.</td>
<td valign="top"><b>푸시 서비스 제공자</b><ul><li>Apple Push Notifications Service</li><li>Google Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Cloudant 서비스 아이콘"><b>Cloudant NoSQLDB</b><br/> Cloudant는 NoSQL DBaaS(Database as a Service)입니다. 처음부터 글로벌하게 스케일링하고 계속 실행되며 JSON, 전체 텍스트 및 지리 공간과 같은 다양한 유형의 데이터를 처리하도록 빌드되었습니다.</td>
<td>Cloudant.com</td>
</tr>
</table>
