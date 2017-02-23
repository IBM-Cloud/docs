---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}}에서 게이트웨이 개발
{: #gw_dev_index}

디바이스에서 인터넷에 직접 연결할 수 없으면 게이트웨이 디바이스를 빌드하여 데이터를 검색하고 {{site.data.keyword.iot_full}} 조직의 애플리케이션에 보낼 수 있습니다.
{{site.data.keyword.iot_short_notm}} 조직 및 애플리케이션에 디바이스 게이트웨이를 연결하는 데 도움이 되는 클라이언트 라이브러리, 샘플 및 정보가 제공됩니다.
{:shortdesc}

## 연결 프로토콜
게이트웨이는 MQTT 메시징 프로토콜을 사용하여 {{site.data.keyword.iot_short_notm}}에 연결합니다. HTTP 메시징을 사용하여 {{site.data.keyword.iot_short_notm}}에 게이트웨이를 연결하는 것은 지원되지 않습니다. HTTP 메시징을 사용하여 연결할 수 있는 것은 디바이스뿐입니다. 

## 클라이언트 라이브러리
{{site.data.keyword.iot_short_notm}}에 연결할 수 있는 게이트웨이를 개발하기 위한 클라이언트 라이브러리는 다음 언어로 제공됩니다. 

|클라이언트 라이브러리 |라이브러리 및 추가 문서에 대한 링크
|:---|:---
|C++| https://github.com/ibm-watson-iot/iot-cpp
|C#| https://github.com/ibm-watson-iot/iot-csharp
|Embedded C| https://github.com/ibm-watson-iot/iot-embeddedc
|Java™|https://github.com/ibm-watson-iot/iot-java
|mBed C++|https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/
|Node.js|https://github.com/ibm-watson-iot/iot-nodejs
|Node-RED|https://github.com/ibm-watson-iot/iot-nodered
|Python|https://github.com/ibm-watson-iot/iot-python

사용 가능한 클라이언트 라이브러리에 대한 링크 및 자세한 정보는 [{{site.data.keyword.iot_short_notm}} 개발용 클라이언트 라이브러리](../iot_platform_client_lib.html)를 참조하십시오. 
