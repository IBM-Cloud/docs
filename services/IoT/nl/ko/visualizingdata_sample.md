---

copyright:
  years: 2016, 2017
lastupdated: "2016-06-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 디바이스 데이터 시각화
{: #visualizingdata_data}

이 샘플을 사용하면 {{site.data.keyword.iot_full}} 조직의 등록된 디바이스에서 실시간 데이터와 히스토리 데이터를 시각화할 수 있습니다.
{:shortdesc}

## 시작하기 전에
{: #byb}

데이터를 시각화하려면 다음 조치를 취해야 합니다.

- {{site.data.keyword.iot_short_notm}} 조직에 디바이스를 등록합니다.
- 디바이스에서 {{site.data.keyword.iot_short_notm}}에 이벤트를 전송하는지 확인합니다.
- github 저장소에서 [시각화 샘플 다운로드](https://github.com/ibm-messaging/iot-visualization/archive/v0.2.0.zip)를 수행하고 .zip 파일의 압축을 풉니다.
- {{site.data.keyword.Bluemix_notm}}에서 [cf 명령행 도구 설치](../../starters/install_cli.html)를 수행합니다.

## {{site.data.keyword.Bluemix_notm}}에서 샘플 실행
{: #running_sample}

1. Node.js SDK를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 애플리케이션을 작성합니다. 애플리케이션의 이름과 호스트 이름을 기록해 두십시오. 이 정보는 {{site.data.keyword.Bluemix_notm}}에 애플리케이션을 업로드하는 데 필요합니다.
2. 다음 단계를 완료하여 {{site.data.keyword.Bluemix_notm}}의 {{site.data.keyword.iot_short_notm}} 인스턴스에 node.JS 애플리케이션을 바인드합니다.

  a. {{site.data.keyword.Bluemix_notm}} 대시보드에서 작성한 Node.JS 애플리케이션을 클릭하십시오.

  b. **서비스 또는 API 바인드**를 클릭한 다음 {{site.data.keyword.iot_short_notm}} 서비스를 선택하고 **추가**를 클릭합니다.
3. cf 명령행 도구를 사용하여 디렉토리를 추출된 시각화 샘플 패키지로 변경하고 다음 명령을 실행하여 {{site.data.keyword.Bluemix_notm}}에 연결합니다.
```
cf api https://api.ng.bluemix.net
```
4. 다음을 사용하여 {{site.data.keyword.Bluemix_notm}}에 로그인합니다.
```
cf login -u <your_bluemix_login_id>
```
기본 조직과 영역을 사용하지 않는 경우 다음을 사용할 수 있습니다.
```
cf target-o <your_bluemix_org> -s dev
```

5. `manifest.yml` 파일을 편집하고 다음 형식을 사용하여 호스트와 애플리케이션 이름을 업데이트합니다.
```
applications:
 - disc quota: 1024M
   host: <your_bluemix_hostname>
   name: <your_bluemix_appname>
   command: node ap.js
   path:
   domain: mybluemix.net
   instances: 1
   memory: 128M
```
6. 다음 명령을 사용하여 사용자의 시각화 샘플을 배치합니다.
```
cf push <your_application_name>
```
7. 브라우저에서 다음 URL을 입력합니다.
```
http://<your_application_name>.mybluemix.net
```

조직의 모든 디바이스가 디바이스 드롭다운 메뉴에 나열됩니다. 선택하면 디바이스에서 {{site.data.keyword.iot_short_notm}} 서비스에 전송 중인 데이터의 실시간 시각화가 표시되어야 합니다. 히스토리 데이터를 보려면 **히스토리 데이터** 단추를 클릭하십시오.

## 샘플 사용자 정의
{: #customize_sample}

이 샘플 애플리케이션은 node.js 프레임워크에 작성된 독립형 웹 애플리케이션입니다. 이 샘플은 {{site.data.keyword.iot_short_notm}}에서 등록된 디바이스가 전송한 이벤트를 시각화합니다. 샘플에서는 다음 도구를 사용합니다.

- Express: Node.js 웹 애플리케이션 프레임워크
- JQuery: UI 및 Ajax 호출
- Rickshaw: 그래픽 시각화 도구
- Paho: MQTT 클라이언트

샘플 애플리케이션은 다음 디렉토리로 구조화됩니다.

- Public
- CSS: 스타일시트
- Images
- JS: 기본 JavaScript 로직 파일
- Historian: 히스토리언 시각화 코드
- Realtime: 실시간 시각화 코드
- Uicontroller.js: 사용자 인터페이스 제어 코드
- Routes: 라우팅 로직 및 웹 애플리케이션
- Utils: HTTP 호출에 사용하는 유틸리티 함수
- Views: Jade로 작성된 사용자 인터페이스 파일
- Rickshaw 차트 작성 라이브러리는 실시간의 히스토리 데이터에 대한 그래프를 작성하는 데 사용합니다.

## 실시간 데이터 표시 사용자 정의
{: #customize_real_time_display}

실시간 데이터의 그래픽 시각화 코드를 포함하는 디렉토리는 `public/ja/realtime`입니다. 그래프 작성 로직은 `public/js/historian/realtimeGraph.js`를 편집하여 사용자 정의할 수 있습니다.

디바이스 주제에 등록하고 {{site.data.keyword.iot_short_notm}}에서 디바이스 이벤트를 받기 위해 Paho MQTT 라이브러리를 참조하는 파일은 `public/js/historian/realtime.js`에 있습니다.

디바이스 이벤트는 그래프를 작성하기 위해 `realtimeGraph.js` 파일에 전달됩니다.

## 히스토리 데이터 표시 사용자 정의
{: #customize_historical_display}

히스토리 디바이스 데이터의 그래픽 시각화 코드를 포함하는 디렉토리는 `public/js/historian`입니다. 그래프 작성 로직은 `public/js/historian/historianGraph.js`를 편집하여 사용자 정의할 수 있습니다.

히스토리 디바이스 데이터를 수집하기 위해 ReST API 호출을 제어하는 파일은 `public/js/historian/historian.js`입니다.

히스토리 데이터는 그래프를 작성하기 위해 `historianGraph.js` 파일에 전달됩니다.

자세한 개발자 안내서는 Github iot-visualization 위키에 있습니다.
