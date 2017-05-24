---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-20"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 게이트웨이 액세스 제어
{: #gateway-access-control}

게이트웨이 디바이스에는 기타 디바이스를 대신해서 작동할 수 있는 권한이 있습니다. 게이트웨이 리소스 그룹은 각 게이트웨이가 대신 작동할 수 있는 조직 내의 디바이스를 정의합니다. 게이트웨이에는 *표준 게이트웨이* 역할이 지정될 수 있습니다. 표준 게이트웨이는 해당 리소스 그룹의 디바이스 대신 메시지를 공개하거나 이를 구독할 수만 있습니다.
{: #shortdesc}


API를 사용하여 게이트웨이 디바이스에서 이벤트 공개에 대한 정보는 [게이트웨이 디바이스용 HTTP Messaging API](../gateways/gw_intro_api.html)를 참조하십시오. 

## 게이트웨이에 역할 지정
{: #gw_roles}

게이트웨이가 리소스 그룹을 보유하려면 반드시 게이트웨이에 역할을 지정해야 합니다. 리소스 그룹이 없는 게이트웨이는 조직의 모든 디바이스 대신 작동할 수 있습니다. *표준 게이트웨이* 역할을 지정하면 게이트웨이에 대해 새 리소스 그룹이 자동으로 작성됩니다. 일단 게이트웨이가 리소스 그룹에 지정된 경우, 이는 해당 역할이 변경되어도 자신과 해당 리소스 그룹의 디바이스 대신으로만 작동할 수 있습니다. 

게이트웨이에 역할을 지정하려면 다음 API를 사용하십시오. 

```
PUT /authorization/devices/{deviceId}/roles
```

요청 스키마의 세부사항은 [{{site.data.keyword.iot_full}} Limited Gateway API 문서 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles){: new_window}를 참조하십시오. 

## 리소스 그룹에 디바이스 추가 및 리소스 그룹에서 디바이스 제거
{: #devices_groups}

*표준 게이트웨이* 역할이 있는 게이트웨이가 디바이스 대신 작동할 수 있으려면 우선 해당 디바이스가 게이트웨이에 지정된 리소스 그룹의 멤버여야 합니다. 동시에 리소스 그룹에 많은 디바이스를 추가하려면 다음 API를 사용하십시오. 

```
 PUT /bulk/devices/{groupId}/add
```

디바이스를 추가할 그룹은 요청의 경로에 지정되어야 하며, 추가되는 디바이스는 요청의 본문에 지정되어야 합니다. 요청 스키마 및 응답에 대한 자세한 정보는 [{{site.data.keyword.iot_short_notm}} Limited Gateway API 문서 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_add){: new_window}를 참조하십시오. 

리소스 그룹에서 여러 디바이스를 제거하려면 다음 API를 사용하십시오. 

```
PUT /bulk/devices/{groupId}/remove
```

요청의 본문에 지정된 디바이스가 요청의 경로에 지정된 그룹에서 제거됩니다. 요청 스키마 및 응답에 대한 자세한 정보는 [{{site.data.keyword.iot_short_notm}} Limited Gateway API 문서 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_remove){: new_window}를 참조하십시오. 

## 리소스 그룹 찾기
{: #finding_groups}

리소스 그룹에는 연관된 검색 태그가 있을 수 있습니다. 검색 태그를 사용하면 다음 API를 사용하여 리소스 그룹의 세부사항을 검색할 수 있습니다. 

```
GET /groups
```

이 API는 사용된 검색 태그와 연관된 리소스 그룹을 리턴합니다. 검색 태그가 지정되지 않으면 모든 리소스 그룹이 리턴됩니다. <!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

리소스 그룹의 ID는 다음 API를 사용하여 찾을 수 있습니다.

```
GET /authorization/devices/{deviceId}
```

이 API는 이 디바이스가 해당 멤버인 리소스 그룹의 고유 ID를 리턴합니다. 이 API에 대한 자세한 정보는 [{{site.data.keyword.iot_short_notm}} Limited Gateway API 문서 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_authorization_devices_deviceId){: new_window}에서 찾을 수 있습니다. 


## 리소스 그룹 조회
{: #querying_groups}

다양한 매개변수 내에서 리소스 그룹을 조회하여 그룹에 있는 모든 디바이스의 전체 특성, 그룹에 있는 모든 디바이스의 고유 ID 또는 리소스 그룹의 특성을 리턴할 수 있습니다. 

지정된 리소스 그룹에 있는 모든 디바이스의 전체 특성을 리턴하려면 다음 API를 사용하십시오. 

```
GET /bulk/devices/{groupId}
```

이 API는 지정된 리소스 그룹의 모든 멤버에 대한 전체 특성 목록을 리턴합니다. 요청 스키마, 응답, 그리고 결과 페이지를 넘겨보는 방법에 대한 자세한 정보는 [{{site.data.keyword.iot_short_notm}} Limited Gateway API 문서 ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_bulk_devices_groupId){: new_window}를 참조하십시오. 

리소스 그룹의 멤버에 대한 고유 ID만 리턴하려면 다음 API를 사용하십시오. 

```
GET /bulk/devices/{groupId}/ids
```

이 API는 리소스 그룹의 멤버인 모든 디바이스의 고유 ID를 리턴합니다. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

리소스 그룹의 특성을 리턴하려면 다음 API를 사용하십시오. 

```
GET /groups/{groupId}
```

이 API는 경로에 지정된 리소스 그룹의 특성(이름, 설명, 검색 태그 및 고유 ID)을 리턴하지만, 리소스 그룹의 멤버의 목록은 리턴하지 않습니다. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## 리소스 그룹 작성 및 삭제. 
{: #crt_del_groups}

리소스 그룹은 연결 중인 게이트웨이와 무관하게 작성되고 삭제될 수 있습니다. 리소스 그룹을 작성하려면 다음 API를 사용하십시오. 

```
POST /groups
```

이 API는 리소스 그룹을 작성하고 그룹 세부사항을 리턴합니다. <!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

리소스 그룹을 삭제하려면 다음 API를 사용하십시오. 

```
DELETE /groups/{groupId}
```

이 API는 지정된 리소스 그룹을 삭제합니다. 그룹의 멤버인 디바이스는 그룹에서 제거되지만, 디바이스 자체에는 별다른 영향이 없습니다. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## 그룹 특성 업데이트
{: #update_groups}

  - /groups/{groupId}
    - PUT: 지정된 그룹의 특성을 업데이트합니다. 

## 디바이스 특성의 검색 및 업데이트. 
{: #fdevice_group_props}

API를 사용하여 디바이스 특성을 검색하는 여러 방법이 있으며, 각각의 API는 서로 다른 정보를 리턴합니다. {{site.data.keyword.iot_short_notm}} 조직에 연결된 모든 디바이스의 디바이스 특성을 검색하려면 다음 API를 사용하십시오. 

```
GET /authorization/devices

```

이 API는 액세스 제어 관련 특성(역할, 상태, 만기 날짜)을 포함하여 조직에 연결된 모든 디바이스의 특성을 리턴합니다. <!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

액세스 제어 관련 정보를 검색하지 않고 디바이스 특성을 검색하려면 다음 API를 사용하십시오.

```
GET /authorization/devices/{deviceId}
```

이 API는 액세스 제어 정보의 리턴 없이 지정된 디바이스의 모든 디바이스 특성을 리턴합니다. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

특정 디바이스의 액세스 제어 정보를 검색하려면 다음 API를 사용하십시오.

```
GET /authorization/devices/{deviceId}/roles
```

이 API는 기타 디바이스 특성의 리턴 없이 지정된 디바이스에 대한 액세스 제어 관련 정보를 검색합니다. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

디바이스 특성은 두 가지 방법으로 업데이트가 가능합니다. 액세스 제어 특성의 변경 없이 특성을 업데이트하거나, 액세스 제어 특성을 직접 업데이트할 수 있습니다. 

액세스 제어 특성에 영향을 주지 않고 디바이스 특성을 업데이트하려면 다음 API를 사용하십시오. 

```
PUT /authorization/devices/{deviceId}
```

이 API는 액세스 제어와 연관되지 않은 디바이스의 특성만 업데이트합니다. <!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

지정된 디바이스의 액세스 제어 특성만 업데이트하려면 다음 API를 사용하십시오.

```
PUT /authorization/devices/{deviceId}/withroles
```

이 API는 지정된 디바이스의 액세스 제어 특성만 업데이트합니다. <!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
