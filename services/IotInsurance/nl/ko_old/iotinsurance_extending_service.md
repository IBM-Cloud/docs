---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# API로 서비스 확장
{: #iot4i_extending_service}
{{site.data.keyword.iotinsurance_full}}에서는 {{site.data.keyword.iotinsurance_short}} 솔루션을 사용자 정의하고 확장하는 API를 제공합니다.
{:shortdesc}

{{site.data.keyword.iotinsurance_short}}에는 Wink 누수 센서용 기본 제공 지원이 포함되어 있습니다. 제공된 API를 사용하여 {{site.data.keyword.iotinsurance_short}} 솔루션을 사용자 정의해서 새 디바이스 유형과 공급업체를 지원할 수 있습니다. {{site.data.keyword.iotinsurance_short}}는 클라우드 대 클라우드 통신을 사용하여 디바이스에서 센서 데이터를 가져옵니다. 새 변환 마이크로서비스를 작성하여 {{site.data.keyword.iotinsurance_short}}를 사용자 정의해서 새 디바이스의 센서 데이터를 읽고 {{site.data.keyword.iot_short_notm}} 서비스를 통해 시스템의 나머지 부분에 전달한 다음 적절한 조치를 수행할 수 있습니다. 

전체 예제 코드 세트는 [API 예제 GitHub 저장소 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){: new_window}를 참조하십시오.

전체 API 정보는 [API 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){: new_window}를 참조하십시오. 
