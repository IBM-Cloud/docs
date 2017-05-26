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

# ゲートウェイ・アクセス制御
{: #gateway-access-control}

ゲートウェイ・デバイスは他のデバイスの代理として動作する権限を持ちます。ゲートウェイ・リソース・グループは、各ゲートウェイが組織内のどのデバイスの代理として動作するのかを定義します。ゲートウェイには*標準ゲートウェイ*役割を割り当てることができます。標準ゲートウェイは、リソース・グループ内のデバイスの代理としてメッセージのパブリッシュまたはサブスクライブのみを行うことができます。
{: #shortdesc}


API を使用してゲートウェイ・デバイスからイベントをパブリッシュする方法については、[ゲートウェイ・デバイス用の HTTP Messaging API](../gateways/gw_intro_api.html) を参照してください。

## ゲートウェイへの役割の割り当て
{: #gw_roles}

ゲートウェイがリソース・グループを持つためには、ゲートウェイに役割を割り当てる必要があります。リソース・グループを持たないゲートウェイは、組織内のすべてのデバイスの代理として動作することができます。*標準ゲートウェイ*役割を割り当てると、そのゲートウェイの新しいリソース・グループが自動的に作成されます。ゲートウェイがリソース・グループに割り当てられると、その役割が変更されても、ゲートウェイ自体とそのリソース・グループ内のデバイスの代理としてのみ動作できます。

ゲートウェイに役割を割り当てるには、以下の API を使用します。

```
PUT /authorization/devices/{deviceId}/roles
```

要求スキーマの詳細については、[{{site.data.keyword.iot_full}} 限定版ゲートウェイ API の資料![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles){: new_window}を参照してください。

## リソース・グループのデバイスの追加と削除
{: #devices_groups}

*標準ゲートウェイ*役割を持つゲートウェイがデバイスの代理として動作するには、そのデバイスがゲートウェイに割り当てられたリソース・グループのメンバーである必要があります。リソース・グループに複数のデバイスを同時に追加するには、以下の API を使用します。

```
 PUT /bulk/devices/{groupId}/add
```

デバイスを追加するグループは、要求のパス内に指定されている必要があります。また、追加するデバイスは、要求の本文に指定されている必要があります。要求スキーマと応答の詳細については、[{{site.data.keyword.iot_short_notm}} 限定版ゲートウェイ API の資料![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_add){: new_window}を参照してください。

リソース・グループから複数のデバイスを除去するには、以下の API を使用します。

```
PUT /bulk/devices/{groupId}/remove
```

要求の本文に指定されているデバイスが、要求のパス内に指定されているグループから除去されます。要求スキーマと応答の詳細については、[{{site.data.keyword.iot_short_notm}} 限定版ゲートウェイ API の資料![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_remove){: new_window}を参照してください。

## リソース・グループの検索
{: #finding_groups}

リソース・グループに検索タグを関連付けることができます。以下の API によって、検索タグを使用してリソース・グループの詳細を取得できます。

```
GET /groups
```

この API によって、使用された検索タグに関連付けられたリソース・グループが返されます。検索タグを指定しない場合は、すべてのリソース・グループが返されます。 <!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

リソース・グループの ID を検索するには、以下の API を使用します。

```
GET /authorization/devices/{deviceId}
```

この API によって、このデバイスが所属するリソース・グループの固有 ID が返されます。この API の詳細については、[{{site.data.keyword.iot_short_notm}} 限定版ゲートウェイ API の資料![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_authorization_devices_deviceId){: new_window}を参照してください。


## リソース・グループの照会
{: #querying_groups}

さまざまなパラメーターでリソース・グループを照会して、グループ内のすべてのデバイスの完全なプロパティー、グループ内のすべてのデバイスの固有 ID、またはリソース・グループのプロパティーを返すことができます。

指定のリソース・グループ内のすべてのデバイスの完全なプロパティーを返すには、以下の API を使用します。

```
GET /bulk/devices/{groupId}
```

この API によって、指定のリソース・グループのすべてのメンバーの完全なプロパティー・リストが返されます。要求スキーマ、応答、結果のページ送りの詳細については、[{{site.data.keyword.iot_short_notm}} 限定版ゲートウェイ API の資料![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_bulk_devices_groupId){: new_window}を参照してください。

リソース・グループのメンバーの固有 ID のみを返すには、以下の API を使用します。

```
GET /bulk/devices/{groupId}/ids
```

この API によって、リソース・グループのメンバーであるすべてのデバイスの固有 ID が返されます。<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

リソース・グループのプロパティーを返すには、以下の API を使用します。

```
GET /groups/{groupId}
```

この API によって、パス内に指定したリソース・グループのプロパティー (名前、説明、検索タグ、固有 ID) が返されますが、リソース・グループのメンバー・リストは返されません。<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## リソース・グループの作成と削除
{: #crt_del_groups}

リソース・グループは、接続先のゲートウェイとは独立して作成し、削除できます。リソース・グループを作成するには、以下の API を使用します。

```
POST /groups
```

この API によって、リソース・グループが作成され、グループの詳細が返されます。<!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

リソース・グループを削除するには、以下の API を使用します。

```
DELETE /groups/{groupId}
```

この API によって、指定されたリソース・グループが削除されます。グループのメンバーであったデバイスはグループから除去されますが、デバイスそのものは影響を受けません。<!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## グループ・プロパティーの更新
{: #update_groups}

  - /groups/{groupId}
    - PUT: 指定されたグループのプロパティーを更新します。

## デバイス・プロパティーの取得と更新
{: #fdevice_group_props}

API を使用してデバイス・プロパティーを取得する方法はいくつかあります。API によって返される情報が異なります。{{site.data.keyword.iot_short_notm}} 組織に接続されたすべてのデバイスのデバイス・プロパティーを取得するには、以下の API を使用します。

```
GET /authorization/devices

```

この API によって、アクセス制御関連のプロパティー (役割、状況、有効期限) など、組織に接続されたすべてのデバイスのプロパティーが返されます。<!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

アクセス制御関連の情報を取得せずにデバイス・プロパティーを取得するには、以下の API を使用します。

```
GET /authorization/devices/{deviceId}
```

この API によって、指定されたデバイスのすべてのデバイス・プロパティーが返され、アクセス制御情報は返されません。<!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

指定のデバイスのアクセス制御情報を取得するには、以下の API を使用します。

```
GET /authorization/devices/{deviceId}/roles
```

この API によって、指定のデバイスのアクセス制御関連の情報が返され、他のデバイス・プロパティーは返されません。<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

デバイス・プロパティーを更新する方法は 2 つあります。アクセス制御プロパティーを変更せずにプロパティーを更新する方法と、アクセス制御プロパティーを直接更新する方法です。

アクセス制御プロパティーに影響を与えずにデバイス・プロパティーを更新するには、以下の API を使用します。

```
PUT /authorization/devices/{deviceId}
```

この API によって、アクセス制御に関連付けられていないデバイス・プロパティーのみ更新されます。<!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

指定のデバイスのアクセス制御プロパティーのみを更新するには、以下の API を使用します。

```
PUT /authorization/devices/{deviceId}/withroles
```

この API によって、指定のデバイスのアクセス制御プロパティーのみ更新されます。<!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
