---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}}에서 게이트웨이 개발
{: #gw_dev_index}

디바이스에서 인터넷에 직접 연결할 수 없으면 게이트웨이 디바이스를 빌드하여 데이터를 검색하고 {{site.data.keyword.iot_full}} 조직의 애플리케이션에 보낼 수 있습니다. {{site.data.keyword.iot_short_notm}} 조직 및 애플리케이션에 디바이스 게이트웨이를 연결하는 데 도움이 되는 클라이언트 라이브러리, 샘플 및 정보가 제공됩니다.
{:shortdesc}

## 연결 프로토콜
게이트웨이는 MQTT 메시징 프로토콜을 사용하여 {{site.data.keyword.iot_short_notm}}에 연결합니다. HTTP 메시징을 사용하여 {{site.data.keyword.iot_short_notm}}에 게이트웨이를 연결하는 것은 지원되지 않습니다. HTTP 메시징을 사용하여 연결할 수 있는 것은 디바이스뿐입니다. 

## 클라이언트 라이브러리
{{site.data.keyword.iot_short_notm}}에 연결할 수 있는 게이트웨이를 개발하기 위한 클라이언트 라이브러리는 다음 언어로 제공됩니다. 

|클라이언트 라이브러리 |라이브러리 및 추가 문서에 대한 링크
|:---|:---
|C++|[https://github.com/ibm-watson-iot/iot-cpp ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-cpp){: new_window}
|C#|[https://github.com/ibm-watson-iot/iot-csharp ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-csharp){: new_window}
|Embedded C| [https://github.com/ibm-watson-iot/iot-embeddedc ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-embeddedc){: new_window}
|Java™|[https://github.com/ibm-watson-iot/iot-java ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-java){: new_window}
|mBed C++|[https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/ ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window}
|Node.js|[https://github.com/ibm-watson-iot/iot-nodejs ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window}
|Node-RED|[https://github.com/ibm-watson-iot/iot-nodered ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-nodered){: new_window}
|Python|[https://github.com/ibm-watson-iot/iot-python ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-watson-iot/iot-python){: new_window}

사용 가능한 클라이언트 라이브러리에 대한 링크 및 자세한 정보는 [{{site.data.keyword.iot_short_notm}} 개발용 클라이언트 라이브러리](../iot_platform_client_lib.html)를 참조하십시오. 

## 에지 분석
{: #eaa_community}

{{site.data.keyword.iot_short_notm}} Edge Analytics 기능을 사용하면 게이트웨이 디바이스에서 {{site.data.keyword.iot_short_notm}} Analytics를 실행할 수 있습니다. Edge Analytics를 사용하여 네트워크의 에지에 수집된 데이터를 분석하고 응답할 수 있는 분석을 가져오십시오. 또한 추가 분석 처리, 대시보드 시각화를 위한 {{site.data.keyword.iot_short_notm}}에 디바이스 데이터를 다른 분석에 대한 입력으로 또는 클라우드 기반 히스토리언 저장소에 저장하도록 전송할 수 있습니다.

[IBM Edge Analytics 커뮤니티 페이지 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){: new_window}에서 Edge Analytics SDK를 다운로드할 수 있습니다. SDK에는 SDK JAR 파일, javadoc, 샘플 코드, 레시피 링크 및 README 파일이 포함됩니다. 커뮤니티에서 비디오를 보고 Edge Analytics를 시작하고 실행할 수 있으며 커뮤니티 포럼을 사용하여 질문할 수 있습니다.
