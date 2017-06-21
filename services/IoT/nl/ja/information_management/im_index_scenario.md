---

copyright:
years: 2016, 2017
lastupdated: "2017-04-10"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# アプリケーション・インターフェースのシナリオ 1 (ベータ)
{: #scenario}

以下の情報に基づいてシナリオを作成します。そのシナリオでは、2 つの温度センサーが {{site.data.keyword.iot_short_notm}} にイベントをパブリッシュします。1 つは温度を摂氏で測定するセンサーです。もう 1 つは温度を華氏で測定するセンサーです。それぞれの読み取り値を 1 つの摂氏の読み取り値に対応付けます。それぞれのデバイスから新しい読み取り値がパブリッシュされると、デバイス状態に関連するプロパティーの値が変更されます。

## 前提条件

{{site.data.keyword.iot_short_notm}} 組織インスタンスとその組織の API キーまたはトークンが必要です。API キーやトークンの詳細については、[アプリケーションの HTTP REST API](../applications/api.html#authentication) を参照してください。

## このタスクについて

このシナリオでは、2 つのデバイスを構成します。

1 つは *TemperatureSensor1* というデバイスです。このデバイスは、摂氏で測定した温度イベントをパブリッシュします。温度イベントのパブリッシュ先は `iot-2/evt/tevt/fmt/json` というトピックであり、ペイロードは以下のようになります。
```
{
  “t” : 34.5
}
```

**注:** イベント ID は *tevt* です。この ID は、このタイプの温度イベントを物理インターフェースに追加する時と、このタイプのインバウンド・イベントに関連するプロパティーをアプリケーション・インターフェースのプロパティーに対応付けるマッピングを定義する時に必要になります。このシナリオでは、アプリケーション・インターフェースで **temperature** というプロパティーを定義します。

もう 1 つは *TemperatureSensor2* というデバイスです。このデバイスは、華氏で測定した温度イベントをパブリッシュします。温度イベントのパブリッシュ先は `iot-2/evt/tempevt/fmt/json` というトピックであり、ペイロードは以下のようになります。
```
{
  “temp” : 72.55
}
```

**注:** イベント ID は *tempevt* です。この ID は、このタイプの温度イベントを物理インターフェースに追加する時と、このタイプのインバウンド・イベントに関連するプロパティーをアプリケーション・インターフェースのプロパティーに対応付けるマッピングを定義する時に必要になります。このシナリオでは、アプリケーション・インターフェースで **temperature** というプロパティーを定義します。

アプリケーション・インターフェースも構成します。このアプリケーション・インターフェースでは、このタイプのデバイスの状態を以下の構造で記述します。
```
{
  “temperature” : <現在の温度の値 (摂氏)>
  }
```
この場合は、**temperature** に関連する値を処理するアプリケーションを構成します。**t** に関連する値を処理したり、**temp** に関連する値を摂氏に変換してから処理したりするアプリケーションを構成するわけではありません。

![温度センサー・デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションのマッピング。](images/Information "温度センサー・デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションのマッピング")  

以下のサンプル･シナリオを使用して独自のインターフェース環境をセットアップします。

## 必要に応じて、デバイス・タイプとデバイスを追加します。
{: #step14}

このシナリオでは、2 つのデバイス・タイプと 2 つのデバイス・インスタンスを想定します。デバイス・インスタンス *TemperatureSensor1* は、デバイス・タイプ *EnvSensor1* に関連付けます。デバイス・インスタンス *TemperatureSensor2* は、デバイス・タイプ *EnvSensor2* に関連付けます。

REST API を使用してデバイス・タイプを追加する方法については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types) の資料を参照してください。

## 手順 1: イベント・スキーマ・ファイルを作成する
{: #step1}

このシナリオでは、2 つのイベント・スキーマ・ファイルを作成して、それぞれのインバウンド温度イベントの構造を定義します。

**重要:** 構造化された [JSON ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](http://json-schema.org/){:new_window} イベント・ペイロードを使用する場合は、各ネスト・レベルを `"properties"` エントリーで正しくラップしてください。例えば、ペイロードが `{"d":{"t":<temp>}}` の場合は、次のようにします。
```
 "properties" : {
    "d" : {
      "properties" : {
        "t" : {
          "description" : "Temperature in degrees Celsius",
          "type" : "number",
          "minimum" : -273.15,
          "default" : 0.0
        }
      },
      "required" : ["t"]
    }
  },
  "required" : ["d"]
```

*tEventSchema.json* というスキーマ・ファイルを作成する例を以下に示します。このファイルでは、温度を摂氏で測定する温度センサーから送られてくるインバウンド・イベントの構造を定義します。

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : “defines the structure of a temperature event in degrees Celsius",
  "properties" : {
    "t" : {
          "description" : "temperature in degrees Celsius",
      "type" : "number",
      "minimum" : -273.15,
      "default" : 0.0
    }
  },
      "required" : ["t"]
    }
  ```
**ヒント:** 1 つまたは複数のプロパティーを必須に指定するには、"required" パラメーターを使用します。デバイスの状態をデバイス・データで更新するには、必須プロパティーが Watson IoT Platform のデバイス・メッセージに含まれている必要があります。必須プロパティーが含まれていないメッセージは、処理されません。   

イベント・タイプのイベント・スキーマ・リソースを作成する時には、*tEventSchema* というスキーマ・ファイル名を使用します。

*tempEventSchema.json* というスキーマ・ファイルを作成する例を以下に示します。このファイルでは、温度を華氏で測定する温度センサーから送られてくるインバウンド・イベントの構造を定義します。

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : “defines the structure of a temperature event in degrees Fahrenheit",
  "properties" : {
    "temp" : {
      "description" : "temperature in degrees Fahrenheit",
      "type" : "number",
      "minimum" : −459.67,
      "default" : 0.0
    }
  },
  "required" : ["temp"]
}
  ```
イベント・タイプのイベント・スキーマ・リソースを作成する時には、*tempEventSchema* というスキーマ・ファイル名を使用します。   

## 手順 2: イベント・タイプのイベント・スキーマ・リソースを作成する
{: #step2}

イベント・スキーマ・リソースを作成するには、以下の API を使用します。

```
POST /schemas
```

次のパラメーターが必要です。  

パラメーター	|	説明  
------	|	-----  
name	|	作成するイベント・スキーマの名前を入力します。  
schemaFile	|	ローカルのイベント・スキーマ JSON ファイルへのパス。  



詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) の資料を参照してください。



cURL を使用して *tEventSchema.json* というイベント・スキーマ・リソースを作成する例を以下に示します。

```curl
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=tEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tEventSchema.json'
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "name" : “tEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "contentType" : "application/octet-stream",
  "updated" : "2016-12-06T14:38:52Z",
  "schemaFileName" : "tEventSchema.json",
  "created" : "2016-12-06T14:38:52Z",
  "id" : "5846cd7c6522050001db0e0d",
  "refs" : {
      "content" : "/schemas/5846cd7c6522050001db0e0d/content"
  },
  "schemaType" : "json-schema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
イベント・タイプにイベント・スキーマを追加する時には、この POST メソッドへの応答で返されたスキーマ ID *5846cd7c6522050001db0e0d* が必要になります。

cURL を使用して *tempEventSchema.json* というイベント・スキーマ・リソースを作成する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: multipart/form-data’ \
  --form name=tempEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tempEventSchema.json"'
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "schemaType" : "json-schema",
  "schemaFileName" : "tempEventSchema.json",
  "updated" : "2016-12-06T14:44:51Z",
  "name" : "tempEventSchema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "created" : "2016-12-06T14:44:51Z",
  "id" : "5846cee36522050001db0e0e",
  "refs" : {
      "content" : "/schemas/5846cee36522050001db0e0e/content"
  },
  "contentType" : "application/octet-stream",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```
イベント・タイプにイベント・スキーマを追加する時には、この POST メソッドへの応答で返されたスキーマ ID *5846cee36522050001db0e0e* が必要になります。

## 手順 3: イベント・スキーマを参照するイベント・タイプを作成する
{: #step3}

各イベント・タイプでは、イベント・スキーマ・リソースの作成時に使用した POST メソッドへの応答で返されたスキーマ ID を使用して、該当するイベント・スキーマを参照します。

イベント・タイプを作成するには、以下の API を使用します。

```
POST /event/types
```

次のパラメーターが必要です。  

パラメーター	|	説明
------	|	-----
name	|	作成するイベント・タイプの名前を入力します。
schemaId	|	イベント・スキーマ・リソース用に作成した ID。


詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types) の資料を参照してください。



cURL を使用して、摂氏で測定する温度イベントのイベント・タイプを作成する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d”}'
```

イベント・タイプにイベント・スキーマを追加する時には、このスキーマ ID *5846cd7c6522050001db0e0d* を使用します。この ID は、イベント・スキーマ・リソース *tEventSchema.json* の作成時に使用した POST メソッドへの応答で返された ID です。

この POST メソッドに対する応答の例を以下に示します。

```
{
  "updated" : "2016-12-06T14:53:49Z",
  "schemaId" : "5846cd7c6522050001db0e0d",
  "refs" : {
    "schema" : "/schemas/5846cd7c6522050001db0e0d"
  },
  "name" : "tEvent",
  "created" : "2016-12-06T14:53:49Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846d0fd6522050001db0e0f",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

物理インターフェースにイベント・タイプを追加する時には、この POST メソッドへの応答で返されたイベント・タイプ ID *5846d0fd6522050001db0e0f* を使用します。

cURL を使用して、華氏で測定する温度イベントのイベント・タイプを作成する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
イベント・タイプにイベント・スキーマを追加する時には、このスキーマ ID *5846cee36522050001db0e0e* を使用します。この ID は、イベント・スキーマ・リソース *tempEventSchema.json* の作成時に使用した POST メソッドへの応答で返された ID です。この POST メソッドに対する応答の例を以下に示します。

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "schemaId" : "5846cee36522050001db0e0e",
  "created" : "2016-12-06T15:00:20Z",
  "id" : "5846d2846522050001db0e10",
  "updated" : "2016-12-06T15:00:20Z",
  "name" : “tempEvent”,
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
物理インターフェースにイベント・タイプを追加する時には、この POST メソッドへの応答で返されたイベント・タイプ ID *5846d2846522050001db0e10* を使用します。
## 手順 4: 物理インターフェースを作成する
{: #step7}

物理インターフェースを作成するには、以下の API を使用します。

```
POST /physicalinterfaces
```

次のパラメーターが必要です。  

パラメーター	|	説明
------	|	-----
name	|	作成する物理インターフェースの名前を入力します。


詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) の資料を参照してください。


このシナリオでは、イベント・タイプごとに 1 つずつ、合計で 2 つの物理インターフェースが必要です。

cURL を使用して最初の物理インターフェースを作成する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 1"}'
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
          },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Env sensor physical interface 1",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

摂氏で測定する温度イベントを物理インターフェースに追加する時に呼び出す POST メソッドの URL では、この応答で返された物理インターフェース ID *5847d1df6522050001db0e1a* を使用します。

cURL を使用して 2 番目の物理インターフェースを作成する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 2"}'
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1b/events"
  },
  "id" : "5847d1df6522050001db0e1b",
  "name" : "Env sensor physical interface 2",
  "created" : "2016-12-07T09:19:51Z",
  "updated" : "2016-12-07T09:19:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

華氏で測定する温度イベントを物理インターフェースに追加する時に呼び出す POST メソッドの URL では、この応答で返された物理インターフェース ID *5847d1df6522050001db0e1b* を使用します。   

## 手順 5: 物理インターフェースにイベント・タイプを追加する
{: #step8}

物理インターフェースにイベント・タイプを追加するには、以下の API を使用します。

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```

次のパラメーターが必要です。  

パラメーター	|	説明
------	|	-----
eventId	|	デバイスのイベント・ペイロードのイベント名を入力します。
eventTypeId	|	イベント・タイプ用に作成した ID。


詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) の資料を参照してください。


このシナリオでは、以下のイベント・タイプを指定の物理インターフェースに追加します。
- 摂氏の温度イベント *tevt* を ID *5847d1df6522050001db0e1a* の物理インターフェースに追加します。その際に、トピックから送られてくる *eventId* と、イベント・スキーマ・リソースの作成時に返される *eventTypeId* を使用します。
- 華氏の温度イベント *tempevt* を ID *5847d1df6522050001db0e1b* の物理インターフェースに追加します。その際に、トピックから送られてくる *eventId* と、イベント・スキーマ・リソースの作成時に返される *eventTypeId* を使用します。


cURL を使用して、温度イベント *tevt* を ID *5847d1df6522050001db0e1a* の物理インターフェースに追加する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : “tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

cURL を使用して、温度イベント *tempevt* を ID *5847d1df6522050001db0e1b* の物理インターフェースに追加する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1b/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tempevt", "eventTypeId" : "5846d2846522050001db0e10"}'
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "eventTypeId" : "5846d2846522050001db0e10",
  "eventId" : “tempevt"
}
```

## 手順 6: 物理インターフェースを接続するためにデバイス・タイプを更新する
{: #step9}

デバイス・タイプを更新するには、以下の API を使用します。

```
PUT /device/types/{typeId}
```

次のパラメーターが必要です。  

パラメーター	|	説明
------	|	-----
physicalInterfaceId	|	物理インターフェース用に作成した ID。


詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) の資料を参照してください。


このシナリオでは、デバイス・タイプ *EnvSensor1* を更新して物理インターフェース *5847d1df6522050001db0e1a* に接続し、デバイス・タイプ *EnvSensor2* を更新して物理インターフェース *5847d1df6522050001db0e1b* に接続します。

cURL を使用してデバイス・タイプ *EnvSensor1* を更新する例を以下に示します。

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a”}’
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1a",
  "updatedDateTime" : "2016-12-07T09:49:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor1/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor1/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1a"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
物理インターフェースとアプリケーション・インターフェースを追加する時に、デバイス ID *EnvSensor1* が必要になります。
cURL を使用してデバイス・タイプ *EnvSensor2* を更新する例を以下に示します。

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b”}’
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1b",
  "updatedDateTime" : "2016-12-07T09:59:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor2/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor2/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1b"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
物理インターフェースとアプリケーション・インターフェースを追加する時に、デバイス ID *EnvSensor2* が必要になります。
## 手順 7: アプリケーション・インターフェース・スキーマ・ファイルを作成する
{: #step4}

*envSensor.json* というアプリケーション・インターフェース・スキーマ・ファイルを作成する例を以下に示します。

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "type" : "object",
    "title" : "Environment Sensor Schema",
    "description" : "Schema to represent a canonical environment sensor device",
    "properties" : {
        "temperature" : {
           "description" : "temperature in degrees Celsius",
            "type" : "number",
            "minimum" : -273.15,
            "default" : 0.0
        }
    },
    "required" : ["temperature"]
}
```

## 手順 8: アプリケーション・インターフェース・スキーマ・リソースを作成する
{: #step5}

アプリケーション・インターフェース・スキーマ・リソースを作成するには、以下の API を使用します。

```
POST /schemas
```

次のパラメーターが必要です。  

パラメーター	|	説明
------	|	-----
name	|	作成するアプリケーション・インターフェース・スキーマの名前を指定します。
schemaFile	|	ローカルのアプリケーション・インターフェース・スキーマ JSON ファイルへのパス。


詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) の資料を参照してください。


cURL を使用してアプリケーション・インターフェース・スキーマを作成する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=temperatureEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/envSensor.json"'
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "created" : "2016-12-06T16:51:14Z",
  "name" : "temperatureEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "updated" : "2016-12-06T16:51:14Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "schemaType" : "json-schema",
  "contentType" : "application/octet-stream",
  "schemaFileName" : "envSensor.json",
  "refs" : {
    "content" : "/schemas/5846ec826522050001db0e11/content"
  },
  "id" : "5846ec826522050001db0e11"
}
```
アプリケーション・インターフェースにアプリケーション・インターフェース・スキーマを追加する時には、POST メソッドへの応答で返されたスキーマ ID *5846ec826522050001db0e11* を使用します。
## 手順 9: アプリケーション・インターフェース・スキーマを参照するアプリケーション・インターフェースを作成する
{: #step6}

アプリケーション・インターフェースを作成するには、以下の API を使用します。

```
POST /applicationinterfaces
```

次のパラメーターが必要です。  

パラメーター	|	説明
------	|	-----
name	|	作成するアプリケーション・インターフェースの名前を指定します。
schemaId	|	アプリケーション・インターフェース・スキーマ・リソース用に作成した ID。


詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces) の資料を参照してください。


このシナリオでは、アプリケーション・インターフェースにアプリケーション・インターフェース・スキーマを追加する時に、前の応答で返されたスキーマ ID *5846ec826522050001db0e11* を使用します。

cURL を使用してアプリケーション・インターフェースを作成する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "environment sensor interface", "schemaId" : "5846ec826522050001db0e11"}'
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "schemaId" : "5846ec826522050001db0e11",
  "created" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846ed076522050001db0e12",
  "updated" : "2016-12-06T16:53:27Z",
  "name" : "environment sensor interface"
}
```
このシナリオでは、デバイス・タイプにアプリケーション・インターフェースを追加する時に、この POST メソッドへの応答で返されたアプリケーション・インターフェース ID *5846ed076522050001db0e12* を使用します。インバウンド・デバイス・イベントをアプリケーション・インターフェースで定義するプロパティーに対応付ける時にも、この ID を使用します。

## 手順 10: デバイス・タイプにアプリケーション・インターフェースを追加する
{: #step10}

デバイス・タイプにアプリケーション・インターフェースを追加するには、以下の API を使用します。

```
POST /device/types/{typeId}/applicationinterfaces
```

次のパラメーターが必要です。  

パラメーター	|	説明
------	|	-----
id	|	アプリケーション・インターフェース用に作成した ID。
name	|	デバイス・タイプの名前。
schemaId	|	アプリケーション・インターフェース・リソース用に作成した ID。


refs/schema	|	アプリケーション・インターフェース・リソースへのパス。通常: /schemas/*schemaId*


詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) の資料を参照してください。


このシナリオでは、アプリケーション・インターフェースにデバイス・タイプ *EnvSensor1* と *EnvSensor2* を関連付けます。

cURL を使用して、アプリケーション・スキーマ ID *5846ec826522050001db0e11* を参照するアプリケーション・インターフェース *5846ed076522050001db0e12* をデバイス・タイプ *EnvSensor1* に追加する例を以下に示します。

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface”
        }'
```

この POST メソッドに対する応答の例を以下に示します。

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

cURL を使用して、アプリケーション・スキーマ ID *5846ec826522050001db0e11* に関連するアプリケーション・インターフェース *5846ed076522050001db0e12* をデバイス・タイプ *EnvSensor2* に追加する例を以下に示します。

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface”
        }'
```


この POST メソッドに対する応答の例を以下に示します。

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

## 手順 11: インバウンド・イベントのプロパティーをアプリケーション・インターフェースのプロパティーにマップするためのマッピングを定義する
{: #step11}

イベントをマップするには、以下の API を使用します。

```
POST /device/types/{typeId}/mappings
```

次のパラメーターが必要です。  

パラメーター	|	説明
------	|	-----
applicationInterfaceId	|	アプリケーション・インターフェース用に作成した ID。
propertyMappings	|	アプリケーション・インターフェースに定義されたプロパティーとデバイス・イベント・ペイロードのプロパティーをマップする有効な JSON 構造。以下の例を参照してください。


詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) の資料を参照してください。


このシナリオでは、デバイス・タイプ *EnvSensor1* のマッピングを定義して、インバウンド・イベント *tevt* のプロパティー **t** をアプリケーション・インターフェースのプロパティー **temperature** に対応付けます。また、デバイス・タイプ *EnvSensor2* のマッピングを定義して、インバウンド・イベント *tempevt* のプロパティー **temp** をアプリケーション・インターフェースのプロパティー **temperature** に対応付けます。

cURL を使用してデバイス・タイプ *EnvSensor1* にマッピングを追加する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tevt" : {
               "temperature" : "$event.t"
              }
            }
          }'
```

**重要:** 構造化された [JSON ![外部リンクのアイコン](../../../icons/launch-glyph.svg "外部リンクのアイコン")](http://json-schema.org/){:new_window} イベント・ペイロードを使用する場合は、$event.*property* 項目をプロパティーの JSON 構造と正確に一致させてください。例えば、ペイロードが `{"d":{"t":<temp>}}` の場合は、`$event.d.t` を使用します。

アプリケーション・インターフェースの作成時に使用した POST メソッドへの応答で返されたアプリケーション・インターフェース ID *5846ed076522050001db0e12* と、デバイス・タイプ *EnvSensor1* を指定します。

この POST メソッドに対する応答の例を以下に示します。

```
{
  "propertyMappings" : {
            "tevt" : {
               "temperature" : "$event.t"
    }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```
cURL を使用してデバイス・タイプ *EnvSensor2* にマッピングを追加する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
            }
          }
          }'
```

アプリケーション・インターフェースの作成時に使用した POST メソッドへの応答で返されたアプリケーション・インターフェース ID *5846ed076522050001db0e12* と、デバイス・タイプ *EnvSensor2* を指定します。変換を適用して、華氏の測定値を摂氏の測定値に変更します。


この POST メソッドに対する応答の例を以下に示します。

```
{
  "propertyMappings" : {
            "tempevt" : {
      "temperature" : "($event.temp - 32) / 1.8"
            }
          },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```

## 手順 12: 構成をデプロイする
{: #step15}

各デバイス・タイプのデバイス状態の更新に関連した構成をデプロイします。この構成には、スキーマ、イベント・タイプ、物理インターフェース、アプリケーション・インターフェース、マッピングが含まれています。

デバイス・タイプ構成をデプロイするには、以下の API を使用します。

```
PATCH /device/types/{typeId}
```

次のパラメーターが必要です。  

パラメーター	|	説明
------	|	-----
typeId	|	デバイス・タイプ ID

詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) の資料を参照してください。


このシナリオでは、2 つのデバイス・タイプの構成をデプロイする必要があります。

cURL を使用してデバイス・タイプ *EnvSensor1* の構成をデプロイする例を以下に示します。

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy-configuration"
          }'
```

この PATCH メソッドに対する応答の例を以下に示します。

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor1' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor1"]
  },
 "failures": []
}
```

cURL を使用してデバイス・タイプ *EnvSensor2* の構成をデプロイする例を以下に示します。

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

この PATCH メソッドに対する応答の例を以下に示します。

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor2' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor2"]
  },
 "failures": []
}
```

## 手順 13: インバウンド・デバイス・イベントをパブリッシュする
{: #step12}

*TemperatureSensor1* からトピック `iot-2/evt/tevt/fmt/json`に温度イベントをパブリッシュし、*TemperatureSensor2* からトピック `iot-2/evt/tempevt/fmt/json` に温度イベントをパブリッシュします。

デバイスからインバウンド・イベントをパブリッシュする方法については、[アプリケーションの MQTT 接続](../applications/mqtt.html#publishing_device_events)を参照してください。


## 手順 14: デバイス状態が変更されたことを確認する
{: #step13}

デバイス状態を確認するには、以下の API を使用します。
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```

次のパラメーターが必要です。  

パラメーター	|	説明
------	|	-----
typeId	|	デバイス・タイプ ID
deviceId	|	デバイス ID。
applicationInterfaceId	|	アプリケーション・インターフェース用に作成した ID。
詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) の資料を参照してください。


cURL を使用して *TemperatureSensor1* の現在の状態を取得する例を以下に示します。その際に、作成したアプリケーション・インターフェースの ID を参照します。

```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

この GET メソッドでは、アプリケーション・インターフェース ID *5846ed076522050001db0e12* を使用しています。この ID は、アプリケーション・インターフェースの作成時に使用した POST メソッドへの応答で返された ID です。
この GET メソッドに対する応答の例を以下に示します。
```
{
  "temperature":34.5
}
```
cURL を使用して *TemperatureSensor2* の現在の状態を取得する例を以下に示します。その際に、作成したアプリケーション・インターフェースの ID を参照します。
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

この GET メソッドでは、アプリケーション・インターフェース ID *5846ed076522050001db0e12* を使用しています。この ID は、アプリケーション・インターフェースの作成時に使用した POST メソッドへの応答で返された ID です。
この GET メソッドに対する応答の例を以下に示します。
```
{
  "temperature":22.5
}
```
返された読み取り値は、華氏ではなく摂氏の温度です。

アプリケーションでは、この正規化データを処理できます。構成で温度のそれぞれの単位を取得したり変換したりする必要はありません。


**注:** デプロイされた最新の構成を取得するには、以下の API を使用します。

```
GET /device/types/<typeId>/deployedconfiguration
```
この API を使用すると、最後に正常に完了した PATCH デプロイ操作でデプロイされた構成を取得できます。変更されたけれどもデプロイされていないリソースの構成を取得したい場合は、通常の GET メソッドに、照会するリソースを関連付けて使用してください。
詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) の資料を参照してください。


次の例は、デプロイされた最新の構成を cURL を使用して取得する方法を示しています。
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/deployedconfiguration \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```
この GET メソッドに対する応答の例を以下に示します。
```
{
    "schemas": [
        {
          "name" : “tEventSchema",
          "createdBy" : "a-8x7nmj-9iqt56kfil",
          "contentType" : "application/octet-stream",
          "updated" : "2016-12-06T14:38:52Z",
          "schemaFileName" : "tEventSchema.json",
          "created" : "2016-12-06T14:38:52Z",
          "id" : "5846cd7c6522050001db0e0d",
          "refs" : {
              "content" : "/schemas/5846cd7c6522050001db0e0d/content"
          },
          "schemaType" : "json-schema",
          "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "content": "ew0KICAiJHNjaGVtYSI6ICJodHRwOi8vanNvbi1zY2hlbWEub3JnL2RyYWZ0LTA0L3NjaGVtYSMiLA0KICAidHlwZSIgOiAib2JqZWN0IiwNCiAgInRpdGxlIiA6ICJFbnZTZW5zb3IxIHRFdmVudCBTY2hlbWEiLA0KICAiZGVzY3JpcHRpb24iIDog4oCcZGVmaW5lcyB0aGUgc3RydWN0dXJlIG9mIGEgdGVtcGVyYXR1cmUgZXZlbnQgaW4gZGVncmVlcyBDZWxzaXVzIiwNCiAgInByb3BlcnRpZXMiIDogew0KICAgICJ0IiA6IHsNCiAgICAgICJkZXNjcmlwdGlvbiIgOiAidGVtcGVyYXR1cmUgaW4gZGVncmVlcyBDZWxzaXVzIiwNCiAgICAgICJ0eXBlIiA6ICJudW1iZXIiLA0KICAgICAgIm1pbmltdW0iIDogLTI3My4xNSwNCiAgICAgICJkZWZhdWx0IiA6IDAuMA0KICAgIH0NCiAgfSwNCiAgInJlcXVpcmVkIiA6IFsidCJdDQp9"
        }
    ],
    "eventTypes": [
        {
          "updated" : "2016-12-06T14:53:49Z",
  "schemaId" : "5846cd7c6522050001db0e0d",
  "refs" : {
    "schema" : "/schemas/5846cd7c6522050001db0e0d"
  },
  "name" : "tEvent",
  "created" : "2016-12-06T14:53:49Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846d0fd6522050001db0e0f",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
},
        {
          "createdBy" : "a-8x7nmj-9iqt56kfil",
          "schemaId" : "5846cee36522050001db0e0e",
          "created" : "2016-12-06T15:00:20Z",
          "id" : "5846d2846522050001db0e10",
          "updated" : "2016-12-06T15:00:20Z",
          "name" : “tempEvent”,
          "refs" : {
            "schema" : "/schemas/5846cee36522050001db0e0e"
          },
          "updatedBy" : "a-8x7nmj-9iqt56kfil"
        }
    ],
    "physicalInterface": {
          "events":[
            {
                  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
},
            {
                "eventTypeId" : "5846d2846522050001db0e10",
                "eventId" : “tempevt"
            }
          ],
        "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "refs" : {
            "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
          },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Env sensor physical interface 1",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
},
    "applicationInterfaces": [
        {
          "createdBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
          "schemaId" : "5846ec826522050001db0e11",
          "created" : "2016-12-06T16:53:27Z",
          "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "id" : "5846ed076522050001db0e12",
          "updated" : "2016-12-06T16:53:27Z",
          "name" : "environment sensor interface"
        }
    ],
    "mappings": [
        {
          "propertyMappings" : {
            "tevt" : {
               "temperature" : "$event.t"
            },
            "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
            }
          },
          "applicationInterfaceId" : "5846ed076522050001db0e12"
        }
    ]
}
```
