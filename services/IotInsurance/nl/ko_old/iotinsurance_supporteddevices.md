---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 지원되는 디바이스 및 공급업체
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}}는 다중 클라우드 공급업체 및 디바이스와의 통합을 지원합니다.
{: shortdesc}

## 공급업체별 지원되는 디바이스
{: #supportedvendors}
다음 표에 {{site.data.keyword.iotinsurance_short}}에서 지원되는 디바이스 및 공급업체의 목록이 나열되며 통합 유형에 대해 설명합니다. 다음과 같은 통합 유형을 사용할 수 있습니다. 

  - **{{site.data.keyword.iot_short_notm}}** - 디바이스 또는 허브가 {{site.data.keyword.iot_short_notm}}에 직접 센서 이벤트를 공개합니다. {{site.data.keyword.iotinsurance_short}}는 센서 이벤트를 직접 처리하거나 {{site.data.keyword.iotinsurance_short}} Transformer에서 조금 수정한 후에 처리할 수 있습니다. 

  - **클라우드 대 클라우드** - 디바이스 또는 허브가 써드파티 클라우드에서 센서 이벤트를 공개합니다. {{site.data.keyword.iotinsurance_short}} Transformer는 써드파티 클라우드에서 해당 이벤트를 읽고 {{site.data.keyword.iot_short_notm}}에 공개합니다. 

<table>
<thead>
<tr>
<th>공급업체 이름</th>
<th>통합 유형</th>
<th>테스트한 디바이스</th>
<th>공급업체 정보</th>
</tr>
</thead>
<tbody>
<tr>
<td>Bosch E-Call</td>
<td>{{site.data.keyword.iot_short_notm}}.  
통합을 테스트하기 위해 게이트웨이 앱이 작성되었습니다. </td>
<td>Bosch Retrofit E-Call</td>
<td>[공급업체 웹 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](http://www.bosch-connectivity.com/en/what_we_offer/products_and_solutions_1/retrofit_ecall/connected_devices_3){: new_window}</td>
</tr>
<tr>
<td>EnOcean</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>단추</li>
<li>컨택트</li>
<li>온도</li>
</ul>
</td>
<td>[공급업체 웹 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://www.enocean.com/en/</td>){: new_window}
</tr>
<tr>
<td>WiButler(iExergy)</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>연기 탐지기</li>
<li>단추</li></td>
</ul>
<td>[공급업체 웹 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://www.wibutler.com/en_GB){: new_window}</td>
</tr>
<tr>
<td>Wink</td>
<td>클라우드 대 클라우드</td>
<td>누수</td>
<td>[공급업체 웹 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://www.wink.com/){: new_window}</td>
</tr>
<tr>
<td>Yanzi</td>
<td>{{site.data.keyword.iot_short_notm}} 및 클라우드 대 클라우드</td>
<td>센서를 테스트하지 않았습니다.</td>
<td>[공급업체 웹 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://ibm.ent.box.com/notes/126680846739){: new_window}</td>
</tr>
</tbody>
</table>

## 디바이스 및 공급업체 클라우드 통합
{: #integratingdevices}
디바이스 및 공급업체 클라우드를 {{site.data.keyword.iotinsurance_short}}와 통합할 수 있습니다. 다음 섹션에서 각 공급업체에 대한 샘플 사용자 레코드 및 통합 프로시저가 제공됩니다. 

센서 및 디바이스 통합에 대한 자세한 정보는 [디바이스 툴킷](iotinsurance_device_toolkit.html)을 참조하십시오.


### EnOcean
#### 통합 프로시저
  1. {{site.data.keyword.iotinsurance_short}}에 연결된 {{site.data.keyword.iot_short_notm}} 인스턴스에서 게이트웨이를 작성하십시오. 
  2. EnOcean 허브를 {{site.data.keyword.iot_short_notm}} 게이트웨이에 연결하십시오.
  3. {{site.data.keyword.iotinsurance_short}}에서 사용자 레코드에 게이트웨이 ID를 추가하십시오.

#### 샘플 사용자 레코드

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "digital-concepts-gateway1"
    ],
    ...
}
```

### WiButler(iExergy)

#### 통합 프로시저
WiButler 데이터와의 통합은 현재 개념 증명 또는 기술적 미리보기로서만 지원되며 프로덕션 사용을 위한 것은 아닙니다. {{site.data.keyword.iot_short_notm}}에 데이터를 스트리밍하려면 WiButler 하드웨어의 펌웨어를 업데이트해야 합니다.

#### 샘플 사용자 레코드

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "Wibutler-Gateway-ID"
    ],
    ...
}
```

### Wink

#### 통합 프로시저

**옵션 1**
  1. [Wink 인증 토큰 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](http://docs.winkapiv2.apiary.io/#){: new_window}을 확보하십시오.
  2. {{site.data.keyword.iotinsurance_short}} API를 사용하여 {{site.data.keyword.iotinsurance_short}} 시스템에서 해당하는 사용자에 인증 토큰을 추가하십시오. 

**옵션 2**  
모바일 앱을 사용하여 통합하십시오(더 이상 사용되지 않음). 이 방법은 {{site.data.keyword.iotinsurance_short}}의 버전 1.0에서만 작동합니다.

#### 샘플 사용자 레코드

```
{
  "username": "user@example.com",
  "password": "",
  ....
  "deviceID": "528DB5CA-7F3D-4478-A4EB-994E7F118B6B",
  "assets": [
    {
      "name": "default",
      "providers": [
        {
          "name": "wink",
          "tokens": {
            "data": {
              "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
              "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
              "token_type": "bearer",
              "token_endpoint": "https://api.wink.com/oauth2/token",
              "scopes": "full_access"
            },
            "errors": [],
            "pagination": {},
            "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
            "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
            "token_type": "bearer",
            "token_endpoint": "https://api.wink.com/oauth2/token",
            "scopes": "full_access"
          }
        }
      ]
    }
  ]
}

```

### Yanzi
#### 통합 프로시저
**옵션 1**  
  Yanzi 클라우드의 신임 정보를 Transformer 저장소의 제공자 디렉토리에 있는 yanzi-config.json으로 추가하십시오. "yanziCloud" 오브젝트가 신임 정보의 올바른 위치입니다.  

**옵션 2**  
  Yanzi는 Yanzi 클라우드와 {{site.data.keyword.iot_short_notm}} 사이의 클라우드 대 클라우드 통합을 사용합니다. 이 통합에 대한 권한 부여가 Yanzi 클라우드 내에서 발생합니다. 권한 부여가 완료된 후에 Yanzi 클라우드는 {{site.data.keyword.iot_short_notm}}에 이벤트를 전송합니다. {{site.data.keyword.iot_short_notm}} 인스턴스의 신임 정보를 "iotfCredentials" 오브젝트를 사용하여 Transformer 저장소의 제공자 디렉토리에 있는 yanzi-config.json으로 추가해야 합니다. 

#### 샘플 사용자 레코드

```
{
  "yanziCloud": {
      "cirrusHost": "wss://",
      "username": "",
      "password": "",
      "locationId": "",
      "unitDid": ""
  },
  "iotfCredentials": {
      "org": "",
      "apiKey": "",
      "apiToken": "",
      "type": "shared",
      "mqtt_host": "gbdprt.messaging.internetofthings.ibmcloud.com",
      "domain": "internetofthings.ibmcloud.com"
  }
}
```

### Weather Company 데이터
#### 통합 프로시저
Weather Company 데이터와의 통합은 현재 개념 증명 또는 기술적 미리보기로서만 지원되며 프로덕션 사용을 위한 것은 아닙니다. 

특정 위치에 대해 Weather Company에서 현재 날씨(외부 온도) 조건을 검색하기 위한 주소를 제공하십시오. 



#### 샘플 사용자 레코드

```
{ "username": "johndoe",
   "fullname": "John Doe",
    "firstname": "John",
    "lastname": "Doe",
    "password": "",
     "accessLevel": 13,
     "address": "Mies-van-der-Rohe-Straße 6, 80807 München, Germany",
     ...
}

```
