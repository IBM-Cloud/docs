---

copyright:
  years: 2015, 2016

---
# {{site.data.keyword.mobileanalytics_short}}를 사용하여 앱 모니터링
{: #monitoringapps}
*마지막 업데이트 날짜: 2016년 5월 6일*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}}는 모바일 애플리케이션에 대한 모니터링 및 분석을 제공합니다. 클라이언트 로그를 기록하고 {{site.data.keyword.mobileanalytics_short}} 클라이언트 SDK를 사용하여 데이터를 모니터링할 수 있습니다. 개발자는 이 데이터를 {{site.data.keyword.mobileanalytics_short}} 서비스에 전송할 시기를 제어할 수 있습니다. 데이터가 {{site.data.keyword.mobileanalytics_short}}에 전달될 때 {{site.data.keyword.mobileanalytics_short}} 대시보드를 사용하여 모바일 애플리케이션, 디바이스 및 클라이언트 로그에 대한 분석 통찰을 가져올 수 있습니다.
{: shortdesc}

<!--

## Visualizing data with custom charts
{: #custom-charts}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for client logs
{: #custom-charts-client-logs}

You can create a custom chart for client logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use client log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

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
  * Event Type: Client Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your app name
7. Click **Save**

### Exporting custom data
{: #export-custom-data}

You can export the data from each custom chart into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom}

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

활동을 더 잘 모니터링하기 위해 {{site.data.keyword.mobileanalytics_short}} 콘솔에서 경보 정의의 임계값을 설정할 수 있습니다.

초과되는 경우, {{site.data.keyword.mobileanalytics_short}} 콘솔 모니터를 알리기 위한 경보를 트리거하는 임계값을 구성할 수 있습니다. 트리거되는 경보가 콘솔에서 시각화되거나 경보가 사용자 정의 Webhook에 의해 처리될 수 있습니다. 이 기능은 클라이언트 로그 오류, 서버 로그 오류, 네트워크 대기 시간의 확장 기간 및 인증 실패를 발견하는 능동적인 방법을 제공합니다. 반응성 임계값 및 경보를 사용하면 사용자가 데이터를 이동하고 넓은 범위의 세분성 임계값을 설정할 필요가 없습니다.

### 클라이언트 로그에 대한 경보 정의 작성
{: #alert-def-client-logs}

클라이언트 로그를 기반으로 하는 경보 정의를 작성할 수 있습니다.

이 예에서는 클라이언트 로그 데이터를 사용하여 경보 정의를 작성할 수 있습니다. 경보는 마지막 5분 내에 수신된 모든 클라이언트 로그를 모니터링하며 경보 정의가 사용할 수 없게 되거나 삭제될 때까지 매5분마다 계속 확인합니다. 경보는 동일한 앱 이름 및 버전을 가진 세 개 이상의 클라이언트 오류 로그를 전송하는 각 디바이스에 대해 트리거됩니다.

1. {{site.data.keyword.mobileanalytics_short}} 콘솔에서 종 아이콘을 클릭하여 **경보 로그** 페이지로 이동하십시오.
2. **경보 관리** 페이지로 이동하여 **경보 작성**을 클릭하십시오.
3. 다음 값을 제공하십시오.
	* 경보 이름: 클라이언트 로그에 대한 경보
	* 메시지: 오류 메시지 경보
	* 조회 빈도: 5분
	* 이벤트 유형: 클라이언트 로그
		* 특성: 로그 레벨
			* 값: 오류
			* 임계값
				* 임계값 유형: 애플리케이션 인스턴스에 대한 총계

					**참고**: 애플리케이션 옵션에 대한 평균을 선택하면 클라이언트 로그가 디바이스 수 기준으로 평균이 됩니다. 예를 들어, 두 개의 디바이스가 있으며 한 디바이스가 여섯 개의 클라이언트 로그를 전송하고 다른 디바이스가 세 개의 클라이언트 로그를 전송하는 경우, 평균은 4.5 클라이언트 로그입니다.
				* 연산자: 3 이상
<!-- insert alert definition tab image? -->

4. **다음** 또는 **분산 방법** 탭을 클릭하고 다음 값을 제공하십시오.
	* 방법: 분석 콘솔 전용

		참고: 사용자 정의된 URL에 JSON 페이로드가 있는 POST 메시지를 추가적으로 전송하려면 분석 콘솔 및 네트워크 게시 옵션을 선택하십시오. 이 옵션을 선택하는 경우 다음 필드가 사용 가능합니다.
		* 네트워크 게시 URL
        * 헤더
        * 인증 유형
5. **저장**을 클릭하십시오. 

클라이언트 로그의 수가 세 개 이상의 오류 로그인 임계값에 도달한 경우, 각 5분 간격의 끝에 경보를 트리거하도록 경보 정의를 작성했습니다.

### 앱 충돌에 대한 경보 정의 작성
{: #alert-def-app-crash}

앱 충돌을 기반으로 하는 경보 정의를 작성할 수 있습니다.

이 예에서는 앱 충돌 데이터를 사용하여 경보 정의를 작성할 수 있습니다. 경보는 마지막 2분 내의 모든 앱 충돌을 모니터링하며 경보 정의가 사용할 수 없게 되거나 삭제될 때까지 매2분마다 계속 확인합니다. 경보는 다섯 번 이상 충돌한 각 앱에 대해 트리거됩니다. 앱 충돌에 대한 자세한 정보는 [앱 충돌](app_crash/c_op_analytics_crashes.html)을 참조하십시오.

1. {{site.data.keyword.mobileanalytics_short}} 콘솔에서 **경보** 아이콘을 클릭하십시오. 이 조치는 경보 로그 페이지를 가져옵니다.
2. **경보 관리** 탭을 클릭하여 **경보 작성**을 클릭하십시오.
3. 다음 값을 제공하십시오.
	* 경보 이름: 앱 충돌에 대한 경보
	* 메시지: 앱 충돌 경보
	* 조회 빈도: 애플리케이션 충돌
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
{: #managing-alert-definitions}

이 예에서는 경보 관리 페이지에서 경보 정의를 관리합니다.

1. {{site.data.keyword.mobileanalytics_short}} 콘솔에서 **경보** 아이콘을 클릭하십시오. 이 조치는 경보 로그 페이지를 엽니다.
2. **경보 관리** 탭을 클릭하십시오.
3. 선택사항: **사용** 열 아래의 선택란을 토글하여 특정 경보 정의를 사용하거나 사용하지 마십시오.
4. 선택사항: 경보 정의의 사본을 작성하고 일부 값을 변경하려면 **중복** 아이콘을 클릭하십시오.
5. 선택사항: 경보 정의를 편집하려면 **연필** 아이콘을 클릭하십시오.
6. 선택사항: 경보 정의를 삭제하려면 **휴지통** 아이콘을 클릭하십시오.

### 경보 세부사항 보기
{: #viewing-alert-details}

이 예에서는 경보 로그 페이지에서 트리거된 경보의 세부사항을 볼 수 있습니다.

1. {{site.data.keyword.mobileanalytics_short}} 콘솔에서 **경보** 아이콘을 클릭하십시오. 이 조치는 경보 로그 페이지를 가져옵니다.
2. 임의의 경보에 대해 **+** 아이콘을 클릭하십시오. 이 조치는 **경보 정의** 및 **경보 인스턴스** 섹션을 표시합니다.

    **참고**: 해당 경보 정의가 삭제되거나 수정되지 않은 경우, **경보 편집**을 클릭하여 경보 정의를 편집할 수 있습니다. 그렇지 않으면 **경보 편집** 단추가 사용 불가능하거나 다음 메시지가 표시됩니다.

    `This alert definition has since been modified or deleted.`

3. 선택사항: 경보를 선택하고 **휴지통** 아이콘을 클릭하여 경보를 삭제하십시오.

## 앱 충돌
{: #monitor-app-crash}

앱을 더 잘 모니터링하고 문제를 해결하기 위해 {{site.data.keyword.mobileanalytics_short}} 콘솔에서 앱 충돌에 대한 정보를 볼 수 있습니다.

### 앱 충돌 모니터링
{: #app-crash}

{{site.data.keyword.mobileanalytics_short}} 콘솔의 **대시보드** 섹션에서 앱 충돌에 대한 정보를 더 빠르게 볼 수 있습니다.

**대시보드** 섹션의 **개요** 페이지에서 **충돌** 막대 그래프는 시간 경과에 따른 충돌 히스토그램을 표시합니다.

두 가지 방법으로 데이터를 표시할 수 있습니다.

1. 충돌 비율 표시: 시간 경과에 따른 충돌 비율 표시
2. 총 충돌 표시: 시간 경과에 따른 충돌 총계


### 앱 충돌 문제점 해결
{: #app-crash-troubleshooting}

앱을 더 잘 관리하기 위해 {{site.data.keyword.mobileanalytics_short}} 콘솔의 **애플리케이션** 섹션에서 **충돌** 페이지를 볼 수 있습니다.

**충돌 개요** 표에는 다음 데이터 열이 표시됩니다.

* 앱: 앱 이름
* 충돌: 해당 앱에 대한 충돌 총계
* 총 사용: 사용자가 해당 앱을 열고 닫은 총 횟수
* 충돌 비율: 사용당 충돌 백분율

**충돌 요약** 표는 정렬 가능하며 다음 데이터 열을 포함합니다.

* 충돌
* 디바이스
* 최근 충돌
* 앱
* OS
* 메시지

임의의 항목 옆의 + 아이콘을 클릭하여 다음 열을 포함하는 **충돌 세부사항** 표를 표시할 수 있습니다.

* 충돌한 시간
* 앱 버전
* OS 버전
* 디바이스 모델
* 디바이스 ID
* 다운로드: 충돌을 발생시킨 로그를 다운로드하기 위한 링크

**충돌 세부사항** 표의 임의의 항목을 펼쳐서 스택 추적을 포함한 더 많은 세부사항을 가져올 수 있습니다.

**참고**: **충돌 요약** 표에 대한 데이터는 심각한 레벨 클라이언트 로그를 조회하여 채워집니다. 앱이 심각한 클라이언트 로그를 수집하지 않은 경우, 사용 가능한 데이터가 없습니다.


