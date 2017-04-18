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

# サポートされるデバイスとベンダー
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} は、複数のクラウド・ベンダーやデバイスとの統合をサポートしています。
{: shortdesc}

## ベンダー別に列挙したサポート・デバイス
{: #supportedvendors}
以下の表では、{{site.data.keyword.iotinsurance_short}} でサポートされるベンダーとデバイスをリストし、統合タイプについて説明します。使用できる統合タイプは次のとおりです。

  - **{{site.data.keyword.iot_short_notm}}** - デバイスまたはハブは、センサー・イベントを {{site.data.keyword.iot_short_notm}} で直接発行します。{{site.data.keyword.iotinsurance_short}} はセンサー・イベントを、直接処理するか、または {{site.data.keyword.iotinsurance_short}} 変換プログラムでいくらか変更してから処理することができます。

  - **クラウド・トゥー・クラウド** - デバイスまたはハブは、センサー・イベントをサード・パーティーのクラウドで発行します。{{site.data.keyword.iotinsurance_short}} 変換プログラムは、サード・パーティーのクラウドからのそれらのイベントを読み取り、{{site.data.keyword.iot_short_notm}} でそれらを発行します。

<table>
<thead>
<tr>
<th>ベンダー名</th>
<th>統合タイプ</th>
<th>検証済みのデバイス</th>
<th>ベンダー情報</th>
</tr>
</thead>
<tbody>
<tr>
<td>Bosch E-Call</td>
<td>{{site.data.keyword.iot_short_notm}}.  
統合の検証のためにゲートウェイ・アプリを作成しました。</td>
<td>Bosch Retrofit E-Call</td>
<td>[ベンダー Web サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg)](http://www.bosch-connectivity.com/en/what_we_offer/products_and_solutions_1/retrofit_ecall/connected_devices_3){: new_window}</td>
</tr>
<tr>
<td>EnOcean</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>ボタン</li>
<li>接点</li>
<li>温度</li>
</ul>
</td>
<td>[ベンダー Web サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://www.enocean.com/en/</td>){: new_window}
</tr>
<tr>
<td>WiButler (iExergy)</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>煙探知器</li>
<li>ボタン</li></td>
</ul>
<td>[ベンダー Web サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://www.wibutler.com/en_GB){: new_window}</td>
</tr>
<tr>
<td>Wink</td>
<td>クラウド・トゥー・クラウド</td>
<td>水漏れ</td>
<td>[ベンダー Web サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://www.wink.com/){: new_window}</td>
</tr>
<tr>
<td>Yanzi</td>
<td>{{site.data.keyword.iot_short_notm}} とクラウド・トゥー・クラウド</td>
<td>検証したセンサーはありません。</td>
<td>[ベンダー Web サイト ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://ibm.ent.box.com/notes/126680846739){: new_window}</td>
</tr>
</tbody>
</table>

## デバイスとベンダー・クラウドを統合する
{: #integratingdevices}
デバイスとベンダー・クラウドを {{site.data.keyword.iotinsurance_short}} に統合することができます。以下のセクションでは、統合手順とサンプル・ユーザー・レコードをベンダーごとに示します。

センサーとデバイスの統合について詳しくは、[デバイス・ツールキット](iotinsurance_device_toolkit.html)を参照してください。


### EnOcean
#### 統合手順
  1. {{site.data.keyword.iotinsurance_short}} に接続されている {{site.data.keyword.iot_short_notm}} インスタンスに、ゲートウェイを作成します。
  2. EnOcean ハブを {{site.data.keyword.iot_short_notm}} ゲートウェイに接続します。
  3. {{site.data.keyword.iotinsurance_short}} でユーザー・レコードにゲートウェイ ID を追加します。

#### サンプル・ユーザー・レコード

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

### WiButler (iExergy)

#### 統合手順
WiButler データとの統合は現時点で、PoC (概念検証) またはテクニカル・プレビューとしてのみサポートされます。実動用としての使用を意図したものではありません。データを {{site.data.keyword.iot_short_notm}} に流すには、WiButler ハードウェアのファームウェア更新が必要です。

#### サンプル・ユーザー・レコード

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

#### 統合手順

**オプション 1**
  1. [Wink 許可トークン ![外部リンク・アイコン](../../icons/launch-glyph.svg)](http://docs.winkapiv2.apiary.io/#){: new_window} を取得します。
  2. {{site.data.keyword.iotinsurance_short}} API を使用して、許可トークンを、{{site.data.keyword.iotinsurance_short}} システムでの対応するユーザーに追加します。

**オプション 2**  
モバイル・アプリを使用して統合します (非推奨)。この方式は、{{site.data.keyword.iotinsurance_short}} のバージョン 1.0 でのみ機能します。

#### サンプル・ユーザー・レコード

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
#### 統合手順
**オプション 1**  
Yanzi クラウドの資格情報を、変換プログラム・リポジトリーのプロバイダーのディレクトリーにある yanzi-config.json 内に追加します。「yanziCloud」オブジェクトは、資格情報の正しい場所です。  

**オプション 2**  
Yanzi は、Yanzi クラウドと {{site.data.keyword.iot_short_notm}} の間のクラウド・トゥー・クラウド統合を使用します。この統合では、Yanzi クラウド内で権限が付与されます。権限付与が完了すると、Yanzi クラウドはイベントを {{site.data.keyword.iot_short_notm}} に送信します。また、「iotfCredentials」オブジェクトを使用して、{{site.data.keyword.iot_short_notm}} インスタンスの資格情報を、変換プログラム・リポジトリーのプロバイダーのディレクトリーにある yanzi-config.json 内に追加することも必要です。

#### サンプル・ユーザー・レコード

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

### Weather Company データ
#### 統合手順
Weather Company データとの統合は現時点で、PoC (概念検証) またはテクニカル・プレビューとしてのみサポートされます。実動用としての使用を意図したものではありません。

特定の場所における現在の天候 (外気温) 状態を Weather Company から取得するために、住所を指定します。



#### サンプル・ユーザー・レコード

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
