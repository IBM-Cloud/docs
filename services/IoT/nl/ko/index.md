---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 시작하기
{: #gettingstartedtemplate}
마지막 업데이트 날짜: 2016년 8월 26일
{: .last-updated}

{{site.data.keyword.iot_full}} for {{site.data.keyword.Bluemix_notm}}에서는 게이트웨이 디바이스, 디바이스 관리 및 강력한 애플리케이션 액세스를 포함하는 다용도 툴킷을 제공합니다. {{site.data.keyword.iot_short_notm}}을 사용하면 연결된 디바이스 데이터를 수집하고 조직의 실시간 데이터에 대한 분석을 수행할 수 있습니다.
{:shortdesc}

## 시작하기 전에
{: #byb}

디바이스를 연결하고 데이터를 이용하기 전에 {{site.data.keyword.iot_short_notm}} 서비스의 인스턴스가 {{site.data.keyword.Bluemix_notm}} 조직에 있어야 합니다. [Bluemix Services Catalog의 {{site.data.keyword.iot_short_notm}} 페이지](https://console.{DomainName}/catalog/services/internet-of-things-platform/)에서 직접 작성할 수 있습니다.  

## 1단계: 디바이스 연결
{: #up_and_running}

서비스를 시작하고 실행하려면 상황에 따라 다음 옵션을 탐색하십시오.

   |   서비스가 배치됨 | 서비스가 배치되지 않음
  ------------- | -------------
  **I 연결할 디바이스가 있음** | [{{site.data.keyword.iot_short_notm}}에 디바이스 연결](iotplatform_task.html#iotplatform_task).| [조직 데모 실행](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window}에서 디바이스 연결 탐색.
  **I 연결할 디바이스가 없음** | [Node-RED 디바이스 시뮬레이터 작성 및 연결](nodereddevice_sample.html){:new_window}. | [Watson IoT Platform Starter](https://new-console.stage1.ng.bluemix.net/docs/starters/IoT/iot500.html){:new_window} 시작하기.
특정 디바이스 유형을 {{site.data.keyword.iot_short_notm}}에 연결하는 방법에 대한 자세한 정보는 [developerWorks recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}를 참조하십시오.  

디바이스 연결 개발자 문서는 다음을 참조하십시오.
- [디바이스용 MQTT 연결](devices/mqtt.html).
- [게이트웨이용 MQTT 연결](gateways/mqtt.html).

## 2단계: 디바이스 데이터 분석
{: #analyzing_data}

디바이스에서 {{site.data.keyword.iot_short_notm}}에 보내는 실시간 데이터 탐색을 시작합니다.

{{site.data.keyword.iot_short_notm}}에는 다음 분석 도구가 있습니다.  
- 실시간 디바이스 데이터를 시각화하는 [보드 및 카드](data_visualization.html).
- 실시간 디바이스 데이터에서 트리거하는 [규칙 및 조치](analytics.html).

빨리 시작하기 예는 [Using Rules and Actions with IBM Watson IoT Platform Cloud Analytics](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window} developerWorks 참조서를 확인하십시오.

## 3단계: 디바이스 데이터를 이용하는 애플리케이션 작성
{: #develop_applications}

실시간 및 히스토리안 디바이스 데이터를 이용하기 위해 고유 애플리케이션을 작성하고 연결하여 {{site.data.keyword.iot_short_notm}}의 데이터 분석 기능을 확장합니다.

자세한 정보는 다음 주제를 참조하십시오.   
- [애플리케이션 개발자 문서](applications/api.html) 및 [{{site.data.keyword.iot_short_notm}} API 문서](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}를 탐색하십시오.
- 디바이스와 애플리케이션을 통합하고 연결하는 코드를 빌드하고 개발하기 위한 도구와 파일을 제공하는 [{{site.data.keyword.iot_short_notm}} 클라이언트 라이브러리](iot_platform_client_lib.html)를 탐색합니다.
- [히스토리 디바이스 데이터를 저장하기 위해 {{site.data.keyword.cloudantfull}} 서비스](cloudant_connector.html)를 {{site.data.keyword.iot_short_notm}}에 연결합니다.




# 관련 링크
{: #rellinks}
## 튜토리얼 및 샘플
{: #samples}
* [디바이스 연결 참조서](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [{{site.data.keyword.iot_short_notm}} 재생 조직](https://play.internetofthings.ibmcloud.com/){:new_window}
* [Intel Galileo를 {{site.data.keyword.iot_short_notm}}에 연결](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [ARM® mbed™ IoT Starter Kit 연결](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [Raspberry Pi를 {{site.data.keyword.iot_short_notm}}에 연결](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## API 참조서
{: #api}
* [{{site.data.keyword.iot_short_notm}} API 문서](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}
* [개발자 문서](developer_doc_overview.html)
