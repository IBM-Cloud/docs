---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.cloudant_short_notm}}를 사용하여 히스토리언 서비스 연결 및 구성  
{: #cloudant_main}

{{site.data.keyword.cloudantfull}} 서비스를 {{site.data.keyword.iot_full}}에 연결하면 디바이스 데이터를 저장하고 이에 액세스할 수 있습니다. 디바이스 데이터는 선택된 버킷 간격에 따라 일간, 주간 또는 월간 데이터베이스에 저장됩니다. 

{{site.data.keyword.cloudant_short_notm}}를 사용한 디바이스 데이터 저장을 시작하면 세 개의 데이터베이스가 자동으로 작성됩니다. 하나의 데이터베이스는 현재 버킷 간격에 대해 작성되고, 하나는 향후 간격에 대해 작성되며, 다른 하나는 구성 데이터베이스입니다. 디자인 문서는 구성 데이터베이스에 추가될 수 있으며 작성 시에 새 데이터베이스에 복사됩니다. 간격의 끝에 도달한 경우, 디바이스 데이터는 새 간격의 버킷 데이터베이스에 저장되며 다음 간격에 대해 새 데이터베이스가 작성됩니다. 

디바이스 데이터가 데이터베이스가 전송될 때는 두 가지 방법 중 하나로 저장됩니다. 데이터가 올바른 JSON이며 디바이스 이벤트의 형식이 `JSON`으로 설정된 경우, 디바이스 데이터는 다음 형식으로 저장됩니다. 

```json

{
  "_id": "78bf4380-3311-11e6-a747-d7b140d1a70a",
  "_rev": "2-d13912b7c089f060a4ba7369fa86e46f",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "json_payload",
  "format": "json",
  "timestamp": "2016-06-15T16:54:41.464+01",
  "data": {
    "a": 22
  }
}

```

디바이스 데이터가 올바른 JSON이 아니거나 형식이 `JSON`으로 설정되지 않은 경우, 디바이스 데이터는 다음 형식으로 `payload` 필드 아래에 base64 인코딩 문자열로 저장됩니다. 

```json

{
  "_id": "80f1ce10-3311-11e6-a747-d7b140d1a70a",
  "_rev": "1-bfcbf1e74389fe4188a9425c0cd2575a",
  "payload": "eHh4eHg=",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "non_json_payload",
  "format": "notjson",
  "timestamp": "2016-06-15T16:54:55.217+01"
}

```

## 시작하기 전에  
{: #byb}

{{site.data.keyword.cloudant_short_notm}}를 {{site.data.keyword.iot_short}} 서비스에 연결하기 전에 다음 태스크를 완료하십시오. 

- Bluemix 카탈로그를 사용하여 {{site.data.keyword.iot_short_notm}}과 동일한 Bluemix 영역에서 {{site.data.keyword.cloudant_short_notm}}를 설정하십시오.

Bluemix 조직에서 개발자 권한이 있는지와 Bluemix를 통해 사인인했는지 확인하십시오. Bluemix를 통해 사인인하지 않았거나 이 Bluemix 조직에서 개발자 권한이 없는 경우에는 {{site.data.keyword.cloudant_short_notm}} 및 {{site.data.keyword.iot_short_notm}}의 바인딩을 권한 부여하지 못할 수 있습니다. 

다음 단계를 완료하여 {{site.data.keyword.cloudant_short_notm}}에 연결하십시오. 

1. {{site.data.keyword.iot_short}} 대시보드의 탐색줄에서 **확장**을 클릭하십시오. 
2. 히스토리 데이터 스토리지 타일에서 **설정**을 클릭하십시오. 
2. {{site.data.keyword.iot_short}} 서비스와 동일한 Bluemix 영역 내에서 사용 가능한 모든 {{site.data.keyword.cloudant_short_notm}} 서비스는 히스토리 데이터 스토리지 구성 섹션에 나열됩니다.
3. 연결하고자 하는 {{site.data.keyword.cloudant_short_notm}} 서비스를 선택하십시오. 
4. {{site.data.keyword.cloudant_short_notm}} 구성 옵션을 선택하십시오. 

  a. 버킷 간격을 선택하십시오. 버킷 간격은 디바이스 데이터의 저장을 위해 새 데이터베이스가 작성되는 빈도를 제어합니다. 새 버킷은 선택된 버킷 간격을 사용하여 선택된 시간대에서 자정에 작성됩니다. 

  b. 시간대를 선택하십시오. 선택된 시간대의 시간을 사용하여 지정되어야 하는 버킷 디바이스 데이터가 판별됩니다(디바이스의 로컬 시간이 아님). {{site.data.keyword.cloudant_short_notm}}에 전송 중인 디바이스 데이터의 시간소인은 데이터가 입력될 데이터베이스를 판별할 때 선택된 시간대로 변환됩니다. 

  c. 데이터베이스 이름을 판별하는 옵션을 선택하십시오. 데이터베이스 이름은 `iotp_<orgID>_<dbname>_<bucket_name>`이며 여기서,

 +  * `<orgID>`는 조직 ID입니다.
 +  * `<dbname>`은 `데이터베이스 이름` 필드로 제어되는 데이터베이스 이름의 해당 파트에 대한 선택사항입니다.
 +  * `<bucket_name>`은 `버킷 간격` 필드에 대한 선택사항으로 판별되는 문자열입니다.
 +    * `day` 버킷 간격의 경우 `<bucket_name>`은 `yyyy-mm-dd`입니다. 예를 들어, 2016년 7월 6일의 이벤트의 경우 `2016-07-06`입니다.
 +    * `week` 버킷 간격의 경우 `<bucket_name>`은 `yyyy-'w'ww`이며 여기서 `'w'ww`는 주 수를 표시합니다. 예를 들어, 2016년 셋째 주의 이벤트의 경우 `2016-w03`입니다.
 +    * `month` 버킷 간격의 경우 `<bucket_name>`은 `yyyy-mm`입니다. 예를 들어, 2016년 7월의 이벤트의 경우 `2016-07`입니다.

5. **권한 부여**를 클릭하십시오. 
6. 권한 부여 대화 상자에서 **확인**을 클릭하십시오. 

이제 디바이스 데이터가 {{site.data.keyword.cloudant}}에 저장됩니다. 

## 히스토리언 서비스 사용에 대한 레시피  
{: #recipes}

다음 레시피는 {{site.data.keyword.iot_short}}의 히스토리언 스토리지로서 {{site.data.keyword.cloudant_short_notm}}를 사용하는 방법을 설명합니다. 

- [{{site.data.keyword.iot_short}}의 히스토리언 데이터 스토리지로서 {{site.data.keyword.cloudant_short_notm}} 구성](https://developer.ibm.com/recipes/tutorials/cloudant-nosql-db-as-historian-data-storage-for-ibm-watson-iot-parti/) 레시피는 디바이스 데이터가 {{site.data.keyword.cloudant_short_notm}}에 저장되는 방법을 설명하며 히스토리언 데이터 스토리지로서 {{site.data.keyword.cloudant_short_notm}}에서 디바이스 데이터를 구성하고 저장하는 방법을 예시합니다. 

- [{{site.data.keyword.cloudant_short_notm}}에서 {{site.data.keyword.iot_short}} 디바이스 데이터 조회 및 처리](https://developer.ibm.com/recipes/tutorials/cloudant-nosql-db-as-historian-data-storage-for-ibm-watson-iot-partii) 레시피는 {{site.data.keyword.cloudant_short_notm}}에 저장된 디바이스 데이터를 조회하고 이에 대한 데이터 처리 오퍼레이션을 수행하는 방법을 표시합니다. 

- [Cloudant NoSQL DB에 저장된 Watson IoT 디바이스 데이터 시각화](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=27327) 레시피는 선형 차트 카드와 히스토리언 데이터 스토리지 간에 링크하여 Watson IoT Platform 대시보드에 디바이스 데이터를 표시하는 방법을 표시합니다. 


## 새 디자인 문서 작성   
{: #design_docs}

새 디자인 문서는 구성 데이터베이스에 포함되어 있으며, 작성된 모든 데이터베이스에 복사됩니다. 구성 데이터베이스 이름은 `iotp_<orgid>_<choice>_configuration
`이며, 시작하기 전에 섹션의 3b단계에서 설명한 데이터베이스 이름과 동일한 매개변수를 사용합니다. 

{{site.data.keyword.iot_short_notm}} 내에 포함된 기본 디자인 문서는 요약 기능과는 별도로 현재 히스토리언에서 사용 가능한 조회를 구현합니다. 

추가적인 디자인 문서가 구성 데이터베이스에 추가될 수 있으며, 작성 시에 새 버킷 간격 데이터베이스에 복사됩니다. 디자인 문서를 구성 데이터베이스에 추가하려면 [Cloudant API 문서](https://docs.cloudant.com/document.html)를 참조하십시오. 

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant_short_notm}}](link) -->
