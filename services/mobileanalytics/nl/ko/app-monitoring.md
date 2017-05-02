---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobileanalytics_short}}를 사용하여 애플리케이션 모니터링
{: #monitoringapps}

{{site.data.keyword.mobileanalytics_full}}는 모바일 애플리케이션에 대한 모니터링 및 분석을 제공합니다. {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 사용하여 애플리케이션 로그와 모니터 데이터를 기록할 수 있습니다. 개발자는 이 데이터를 {{site.data.keyword.mobileanalytics_short}} 서비스에 전송할 시기를 제어할 수 있습니다. 데이터가 {{site.data.keyword.mobileanalytics_short}}에 전달될 때 {{site.data.keyword.mobileanalytics_short}} 콘솔을 사용하여 모바일 애플리케이션, 디바이스, 애플리케이션 로그에 대한 분석 통찰을 얻을 수 있습니다.
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts notoc}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for app logs
{: #custom-charts-client-logs notoc}

You can create a custom chart for app logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use app log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

* Specific data
  * Log level
* Message data
  * Timestamp
* Device OS contextual data
  * Application name
  * Application version
  * Device OS
* Device contextual data
  * Device ID
  * Device model
  * Device OS version


1. Make sure that you have an application that is collecting device logs or gathering analytics.
2. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab on the **Dashboard** page. You can create a chart that is based on the analytics messages that were sent to the server.
3. Click **Create Chart** to create a new custom chart and provide the following values:
  * Chart Title: Application and Log Levels
  * Event Type: App Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your application name
7. Click **Save**

### Exporting custom data
{: #export-custom-data notoc}

You can export the data from each custom chart into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom notoc}

You can import and export custom chart definitions programmatically or manually in the {{site.data.keyword.mobileanalytics_short}} Dashboard.

Ensure that you have at least one custom chart in the {{site.data.keyword.mobileanalytics_short}} Dashboard.
In this example, you manually export and import custom chart definitions.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab in the **Dashboard** page.
2. To export the custom chart definitions, click **Export Charts**. This action displays a dialog to save a `customChartsDefinition.json` file.
3. Choose a location to save the file.
4. Click the **Delete Chart** icon next to each custom chart to delete all custom charts.
5. To import a custom chart definition, click **Import Charts**. This action displays a dialog to choose a file.
6. Choose the `customChartsDefinition.json` file that you previously exported to open.

You can also export and import custom chart definitions programmatically by using your HTTP client of choice (for example, CURL or postman):
* The GET endpoint for export is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* The POST endpoint for import is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Note**: If you import a custom chart definition that exists, you end up with duplicate definitions, which also means that the {{site.data.keyword.mobileanalytics_short}} Dashboard shows duplicate custom charts.

-->

## 경보 설정
{: #alerts}

활동을 보다 잘 모니터하기 위해 {{site.data.keyword.mobileanalytics_short}} 콘솔에서 경보 정의에 임계값을 설정할 수 있습니다. 

임계값이 초과되는 경우 {{site.data.keyword.mobileanalytics_short}} 콘솔 모니터에 알리도록 경보를 트리거하는 임계값을 구성할 수 있습니다. 트리거되는 경보가 콘솔에서 시각화되거나 경보가 사용자 정의 웹훅에 의해 처리될 수 있습니다. <!-- This feature provides a proactive means of detecting app log errors, server log errors, extended periods of network latency, and authentication failures.-->이 기능은 애플리케이션 로그 오류와 애플리케이션 충돌 서버 로그 오류를 발견하는 사전 예방 수단을 제공합니다. 반응성 임계값 및 경보를 사용하면 사용자가 데이터를 이동하고 넓은 범위의 세분성 임계값을 설정할 필요가 없습니다.

### 애플리케이션 로그에 대한 경보 정의 작성
{: #alert-def-client-logs notoc}

애플리케이션 로그를 기반으로 하는 경보 정의를 작성할 수 있습니다. 

이 예에서는 애플리케이션 로그 데이터를 사용하여 경보 정의를 작성합니다. 경보는 마지막 5분 내에 수신된 모든 애플리케이션 로그를 모니터링하며 경보 정의가 사용할 수 없게 되거나 삭제될 때까지 5분마다 계속 확인합니다. 경보는 애플리케이션 이름과 버전이 동일한 세 개 이상의 애플리케이션 오류 로그를 전송하는 각 디바이스에 대해 트리거됩니다. 

1. {{site.data.keyword.mobileanalytics_short}} 콘솔에서 **정의**를 클릭하여 경보 정의 페이지로 이동하십시오. 
2. **경보 작성**을 클릭하여 경보를 작성하십시오. 
3. 다음 값을 제공하십시오.
	* 경보 이름: 앱 로그에 대한 경보
	* 메시지: 오류 메시지 경보
	* 조회 빈도: 5분
	* 이벤트 유형: 앱 로그
		* 특성: 로그 레벨
			* 값: 오류
			* 임계값
				* 임계값 유형: 애플리케이션 인스턴스에 대한 총계

					**참고**: 애플리케이션의 평균 옵션을 선택하면 디바이스 수에 따라 앱 로그의 평균을 구합니다. 예를 들어, 두 개의 디바이스가 있으며 한 디바이스가 여섯 개의 앱 로그를 전송하고 다른 디바이스가 세 개의 앱 로그를 전송하는 경우, 평균은 4.5 앱 로그입니다.
				* 연산자: 3 이상
	<!-- insert alert definition tab image? -->

4. **다음**을 클릭하고 다음 값을 제공하십시오.
	* 방법: 분석 콘솔 전용

		**참고**: 사용자 정의된 URL에 JSON 페이로드가 있는 POST 메시지를 추가적으로 전송하려면 분석 콘솔 및 네트워크 게시 옵션을 선택하십시오. 이 옵션을 선택하는 경우 다음 필드가 사용 가능합니다.
		* 네트워크 게시 URL
        * 헤더
        * 인증 유형
5. **저장**을 클릭하십시오. 

오류 로그의 수가 세 개 이상의 오류 로그인 임계값에 도달한 경우, 각 5분 간격의 끝에 경보를 트리거하도록 경보 정의를 작성했습니다.

### 애플리케이션 충돌에 대한 경보 정의 작성
{: #alert-def-app-crash notoc}

애플리케이션 충돌을 기반으로 하는 경보 정의를 작성할 수 있습니다. 

이 예에서는 애플리케이션 충돌 데이터를 사용하여 경보 정의를 작성합니다. 경보는 마지막 2분 내의 모든 애플리케이션 충돌을 모니터링하며 경보 정의가 사용할 수 없게 되거나 삭제될 때까지 2분마다 계속 확인합니다. 경보는 다섯 번 이상 충돌한 각 애플리케이션에 대해 트리거됩니다. 애플리케이션 충돌에 대한 자세한 정보는 [애플리케이션 충돌](#app_crash)을 참조하십시오. 

1. {{site.data.keyword.mobileanalytics_short}} 콘솔에서 **정의**를 클릭하여 경보 정의 페이지를 표시하십시오. 
2. **경보 작성**을 클릭하십시오.
3. 다음 값을 제공하십시오.
	* 경보 이름: 애플리케이션 충돌에 대한 경보
	* 메시지: 앱 충돌 경보
	* 조회 빈도: 애플리케이션 충돌
		* 조회 빈도: 2분
	* 이벤트 유형: 애플리케이션 충돌
		* 애플리케이션 이름: 임의의 애플리케이션
		* 애플리케이션 버전: 임의의 버전
    * 임계값
      * 임계값 유형: 충돌 개수
      * 연산자: 3 이상
4. **분산 방법** 탭을 클릭하고 다음 값을 제공하십시오.
  * 방법: 분석 콘솔 전용

    **참고**: 사용자 정의된 URL에 JSON 페이로드가 있는 POST 메시지를 추가적으로 전송하려면 **분석 콘솔 및 네트워크 게시** 옵션을 선택하십시오. 이 옵션을 선택하는 경우 다음 필드가 사용 가능합니다.
      * 네트워크 게시 URL(필수)
      * 헤더(선택사항)
      * 인증 유형(필수)
5. **저장**을 클릭하십시오. 

### 경보 정의 관리
{: #managing-alert-definitions notoc}

이 예에서는 경보 관리 페이지에서 경보 정의를 관리합니다.

1. {{site.data.keyword.mobileanalytics_short}} 콘솔에서 **로그**를 클릭하십시오. 이 조치는 경보 로그 페이지를 엽니다. 
2. 선택사항: **사용** 열 아래의 선택란을 토글하여 특정 경보 정의를 사용하거나 사용하지 마십시오.
3. 선택사항: 경보 정의의 사본을 작성하고 일부 값을 변경하려면 **중복** 아이콘을 클릭하십시오.
4. 선택사항: 경보 정의를 편집하려면 **연필** 아이콘을 클릭하십시오.
5. 선택사항: 경보 정의를 삭제하려면 **휴지통** 아이콘을 클릭하십시오.

### 경보 세부사항 보기
{: #viewing-alert-details notoc}

이 예에서는 경보 로그 페이지에서 트리거된 경보의 세부사항을 볼 수 있습니다.

1. {{site.data.keyword.mobileanalytics_short}} 콘솔에서 **로그**를 클릭하십시오. 이 조치는 경보 로그 페이지를 가져옵니다.
2. 임의의 경보에 대해 **+** 아이콘을 클릭하십시오. 이 조치는 **경보 정의** 및 **경보 인스턴스** 섹션을 표시합니다.

    **참고**: 해당 경보 정의가 삭제되거나 수정되지 않은 경우, **경보 편집**을 클릭하여 경보 정의를 편집할 수 있습니다. 그렇지 않으면 **경보 편집** 단추가 사용 불가능하거나 다음 메시지가 표시됩니다.

    `This alert definition has since been modified or deleted.`

3. 선택사항: 경보를 선택하고 **휴지통** 아이콘을 클릭하여 경보를 삭제하십시오.

## 애플리케이션 충돌 모니터링
{: #monitor-app-crash}

애플리케이션을 보다 잘 모니터하고 문제점을 해결할 수 있도록 {{site.data.keyword.mobileanalytics_short}} 콘솔에서 애플리케이션 충돌에 대한 정보를 볼 수 있습니다. 

### 애플리케이션 충돌 모니터링
{: #app-crash notoc}

**충돌** 페이지에서 **충돌 개요** 테이블에 다음 데이터 열이 표시됩니다.

* 애플리케이션: 애플리케이션 이름
* 충돌: 해당 앱에 대한 충돌 총계
* 총 사용: 사용자가 해당 앱을 열고 닫은 총 횟수
* 충돌 비율: 사용에 따른 충돌 백분율

**충돌** 표에서 애플리케이션 충돌에 대한 정보를 빨리 볼 수 있습니다. <!--In the **Overview** page of the **Dashboard** section,--> **충돌** 막대 그래프에 시간 경과에 따른 충돌 히스토그램이 표시됩니다.

다음 두 가지 방법으로 충돌 데이터를 표시할 수 있습니다.

1. 충돌 비율 표시: 시간 경과에 따른 충돌 비율 표시
2. 충돌 총계 표시: 시간 경과에 따른 충돌 총계

### 앱 충돌 문제점 해결
{: #app-crash-troubleshooting notoc}

**문제점 해결** 페이지(<!-- **Applications** section of the --> {{site.data.keyword.mobileanalytics_short}} 콘솔의)에는 **충돌 요약** 테이블을 통해 앱 충돌의 세부 보기가 제공됩니다.

**충돌 요약** 표는 정렬 가능하며 다음 데이터 열을 포함합니다.

* 충돌
* 디바이스
* 최근 충돌
* 애플리케이션
* OS
* 메시지

항목 옆에 있는 + 아이콘을 클릭하여 다음 열을 포함하는 **충돌 세부사항** 표를 표시하십시오.

* 충돌한 시간
* 애플리케이션 버전
* OS 버전
* 디바이스 모델
* 디바이스 ID
* 다운로드: 충돌을 발생시킨 로그를 다운로드하기 위한 링크

**충돌 세부사항** 표에서 항목을 펼쳐 스택 추적을 포함한 추가 세부사항을 가져오십시오.

**참고**: **충돌 요약** 표에 대한 데이터는 심각한 레벨 앱 로그를 조회하여 채워집니다. 애플리케이션이 심각한 애플리케이션 로그를 수집하지 않은 경우에는 사용할 수 있는 데이터가 없습니다. 

## 네트워크 요청 모니터링
{: #monitor-network-requests}


{{site.data.keyword.mobileanalytics_short}} 콘솔에서 애플리케이션의 네트워크 요청 데이터를 표시하십시오. 

다음과 같은 측정에 데이터를 사용할 수 있습니다.
	
* 라운드트립 시간 - 앱에서 네트워크 요청을 수행하는 데 소요되는 시간(ms)을 정의합니다.
* 요청 개수 - 앱에서 네트워크 요청을 수행하는 빈도를 표시합니다. 데이터는 평균으로도 표시됩니다.

## dashDB에 데이터 내보내기
{: #dashdb}

{{site.data.keyword.mobileanalytics_short}} 콘솔에서 보는 메트릭은 모바일 데이터에서 얻을 수 있는 Insights의 샘플뿐입니다. 분석을 사용자 정의하고, 다른 공용 및 개인용 데이터 소스로 데이터를 집계하고, 비즈니스를 이해하고 끌어가는 데 도움이 되도록 심도 있고 상세한 통찰력을 파생하기 위해 첨단 기술의 분석을 적용할 수 있는 {{site.data.keyword.IBM}} dashDB 데이터 웨어하우스에 모바일 데이터를 자동으로 파이핑할 수 있습니다. 

**내보내기** 페이지에서 **DashDB**를 클릭하여 {{site.data.keyword.mobileanalytics_short}} 콘솔에서 dashDB를 설정하십시오. 설정을 완료하고 나면 {{site.data.keyword.mobileanalytics_short}}로 전송된 새 데이터도 1-2시간 내에 dashDB로 전달됩니다.  

<!--
If you have existing DashDB instances, those instances will no longer accept new data because the incoming data no longer matches the schema. Manually add columns for the new data to resume incoming data. Modifying {{site.data.keyword.mobileanalytics_short}} collection tables by adding new columns also breaks the stream of incoming data.
-->

