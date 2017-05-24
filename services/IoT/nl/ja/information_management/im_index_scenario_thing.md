---

copyright:
years: 2016, 2017
lastupdated: "2017-04-11"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# アプリケーション・インターフェースのシナリオ 2 (ベータ)
{: #scenario}

アプリケーション・インターフェースを使用すると、アプリケーションでデバイスやモノの構成を認識する必要がなくなります。例えば、1 つのデバイスを使用して部屋の温度を測定したり、複数のデバイスの読み取り値の平均を取って部屋の温度を計算したりするとします。アプリケーションには、1 つまたは複数の部屋の状態に関する情報が必要です。その情報の一要素が温度のプロパティーです。アプリケーションで受け取る温度値がどのように計算されたかは問題ではありません。

このシナリオでは、温度センサーと湿度センサーが、2 つの会議室で収集された環境データをパブリッシュします。温度と湿度のセンサー・データは 2 つのデバイス・タイプのアプリケーション・インターフェースに別々にマップされます。1 つは温度計のデバイス・タイプで、もう 1 つは湿度計のデバイス・タイプです。次に *RoomType* というモノ・タイプを作成し、*meetingroom1* と *meetingroom2* という 2 つの部屋のモノ・インスタンスを作成します。

このシナリオでは、温度計アプリケーション・インターフェースと湿度計アプリケーション・インターフェースを含む構成をセットアップしてから、正しい環境センサーを各部屋のインスタンスにマップします。例えば、*temperatureSensor1* と *humiditySensor1* を *meetingroom1* にマップします。

## 前提条件
{: #pre_req}

このシナリオは、前の[アプリケーション・インターフェースのシナリオ 1](im_index_scenario) が前提になっています。

先に進む前に、以下のことを確認してください。
- 同じ {{site.data.keyword.iot_short_notm}} 組織インスタンスとその組織用の API キーまたはトークンを使用すること。API キーやトークンの詳細については、[アプリケーションの HTTP REST API](../applications/api.html#authentication) を参照してください。
- 温度センサー用と湿度センサー用の 2 つのアプリケーション・インターフェースを作成済みであること。温度センサー用のアプリケーション・インターフェースを構成する方法については、[デバイス・タイプのアプリケーション・インターフェースのシナリオ](../information_management/im_index_scenario)を参照してください。

## このタスクについて
{: #about}

{{site.data.keyword.iot_short_notm}} では、1 つのモノを複数のデバイスとモノで構成することができます。モノ・タイプは、モノのインスタンスの構成を定義するものです｡アプリケーション・インターフェースにはモノ・タイプを関連付けることができます。この関連付けによって、モノ・タイプのインスタンスに対して生成される状態の構造が定義されます。マッピングを使用して、集約されたデバイスやモノのプロパティーをモノの状態のプロパティーにマップする方法を定義します。

このシナリオでは、2 つの温度センサーと 2 つの湿度センサーがイベントを {{site.data.keyword.iot_short_notm}} にパブリッシュします。事業所ビルの会議室 1 に、温度センサーが 1 つと湿度センサーが 1 つあります。会議室 2 に、もう 1 つの温度センサーと湿度センサーがあります。

![{{site.data.keyword.iot_short_notm}} での温度と湿度のモノとアプリケーションのマッピング。](images/Information "1 つの部屋の複数の環境センサーと {{site.data.keyword.iot_short_notm}} 上の 1 つのアプリケーションのマッピング")

*RoomType* というモノ・タイプを使用して、部屋のインスタンスの構成を定義します。アプリケーション・インターフェースに、この *RoomType* を関連付け、温度と湿度の両方を示す単一の読み取り値にインバウンド・イベントがマップされるように定義します。この単一の読み取り値が、このモノの状態です。
マッピングを使用して、温度センサーや湿度センサーのプロパティーをこのモノの状態にマップする方法を定義します。それぞれのセンサーから新しい読み取り値がパブリッシュされると、モノの状態に関連付けられているプロパティーの値が変更されます。

以下の 4 つのデバイスが含まれています。

デバイス/タイプ | イベント | イベント・ペイロード/プロパティー
------------- |  ------------- | -------------
*temperatureSensor1*/Thermometer (meetingroom1) | `iot-2/evt/`*`tevt`*`/fmt/json` | `{ “t” : 34.5 }`/ **temperature1**
*temperatureSensor2*/Thermometer (meetingroom2) | `iot-2/evt/`*`tempevt`*`/fmt/json` | `{ “temp” : 34.5 }`/ **temperature2**  
*humiditySensor1*/Hygrometer (meetingroom1) | `iot-2/evt/`*`hevt`*`/fmt/json` | `{  “h” : "75%" }`/ **humidity1**
*humiditySensor2*/Hygrometer (meetingroom2) |`iot-2/evt/`*`humevt`*`/fmt/json` | `{  “hum” : "75%"}`/ **humidity2**

モノのタイプのアプリケーション・インターフェースでは、モノの状態を以下の構造で記述します。
```
{
  “temperature” : <現在の温度の値 (摂氏)>
  "humidity" : <現在の湿度の値>
  }
```

<!--
The code that is used in this example is available in the updated {{site.data.keyword.iot_short_notm}} [[Python library ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} in GitHub, in the **thingDataTransform** sample.
-->  

以下のサンプル･シナリオを使用して独自のインターフェース環境をセットアップします。  

## 必要に応じてデバイス・タイプとデバイスを追加する  
{: #add_device}  
このシナリオでは、2 つのデバイス・タイプと 4 つのデバイス・インスタンスを使用します。デバイス・インスタンス *temperatureSensor1* と *temperatureSensor2* はデバイス・タイプ *Thermometer* と関連付けられます。デバイス・インスタンス *humiditySensor1* と *humiditySensor2* はデバイス・タイプ *Hygrometer* と関連付けられます。

REST API を使用してデバイス・タイプを追加する方法については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofThings.ibmcloud.com/swagger/v0002.html#!/Device_Types) の資料を参照してください。
  

## 手順 1: 構成スキーマ・ファイルを作成する  
{: #crt_composition_file}  
温度と湿度の各デバイス・タイプのデバイス・アプリケーション・インターフェース ID を参照する構成スキーマ・ファイルを作成します。  

*Room Type Schema* という構成スキーマ・ファイルを作成する例を以下に示します。  
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "Room Type Schema",
   "description" : "JSON Schema that defines the structure of the Room Thing Type.",
   "properties" : {
       "temperatureSensor": {
           "description": "The temperature sensor device",
           "$applicationInterfaceRef": "58c135e352faff0001198a89"
       },
       "humiditySensor": {
           "description": "The humidity sensor device",
           "$applicationInterfaceRef": "58c135ea52faff0001678f06"
       }
   },
   "required" : [
       "temperatureSensor",
       "humiditySensor"
   ]
}
```
**ヒント:** 1 つまたは複数のプロパティーを必須に指定するには、"required" パラメーターを使用します。デバイスの状態をデバイス・データで更新するには、必須プロパティーが Watson IoT Platform のデバイス・メッセージに含まれている必要があります。必須プロパティーが含まれていないメッセージは、処理されません。   
**注:** モノのタイプを作成するときには、モノのタイプのスキーマ・ファイルを作成したときに生成されたスキーマ ID を指定しなければなりません。  

## 手順 2: 構成スキーマ・リソースを作成する  
{: #crt_composition_resource}  

前の手順で生成されたモノのタイプのスキーマ・ファイルをアップロードして、スキーマ・リソースを作成します。  
以下の API を使用して、モノのタイプのスキーマ・ファイルをアップロードします。  
```
POST /schemas
```  
次のパラメーターが必要です。  
<table>
<tr>
<th>	パラメーター</th><th>	説明</th>
</tr>
<tr>
<td>	name
</td><td>	作成する構成スキーマの名前を指定します。</td>
</tr>
<tr>
<td>	schemaFile
</td><td>	ローカル構成スキーマ JSON ファイルへのパス。</td>
</tr>
</table>

詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) の資料を参照してください。  

<!-- The following example shows how to use Python to create the thing type schema resource:  
```python
roomTypeSchemaFile = open(schemasDir + "roomType.json", "r");
roomTypeSchema = roomTypeSchemaFile.read();
roomTypeSchemaFile.close();
"roomTypeSchemaId", result = api.createSchema("Room Type Schema", "roomType.json", roomTypeSchema)
```  -->

## 手順 3: モノのタイプを作成する  
{: #crt_thing_type}  

モノのタイプを使用して、モノのインスタンスをモデル化します。モノのインスタンスを作成するには、その前にモノのタイプを組織内に作成しておく必要があります。このシナリオの場合は、モノのタイプを 1 つ作成します。  
モノのタイプに関連付けるスキーマによって、モノのインスタンスを構成するためにまとめられるオブジェクトのタイプが定義されます。モノのタイプは、前の手順で作成したモノのタイプのスキーマ・リソースを参照する必要があります。  
モノのタイプを作成するには、以下の API を使用します。
```
POST /thing/types
```
次のパラメーターが必要です。  
<table>
<tr><th>パラメーター</th><th>説明</th></tr>
<tr><td>Id
</td><td>作成するモノのタイプの ID を指定します。</td></tr>
<tr><td>name
</td><td>作成するモノのタイプの名前を指定します。</td></tr>
<tr><td>schemaId
</td><td>構成スキーマ・リソース用に作成した ID。</td></tr>
</table>

詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) の資料を参照してください。  

<!-- The following example shows how to use Python to create a thing type that is called *RoomType*.
```python
result = api.createThingType(thingType, "RoomType", "roomTypeSchemaId", "The Room Thing type")

```  -->

## 手順 4: アプリケーション・インターフェース・スキーマ・ファイルを作成する  
{: #crt_ai_schema_file}
アプリケーション・インターフェースでは、モノの状態として格納するデータの構造を定義できます。このシナリオの場合、温度と湿度のプロパティーを定義するアプリケーション・インターフェースを作成します。アプリケーション・インターフェース・リソースの作成時に生成されたアプリケーション・インターフェース ID を参照して、アプリケーション・インターフェースをモノのタイプ *RoomType* と関連付けます。  
*RoomType Schema* というアプリケーション・インターフェース・スキーマ・ファイルを作成する例を以下に示します。
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "RoomType Schema",
   "description" : "JSON Schema that defines the canonical room state structure",
   "properties" : {
       "temperature" : {
           "description" : "Temperature in degrees celsius",
           "type" : "number",
           "minimum" : -273.15,
           "default" : 0.0
       },
       "humidity" : {
           "description" : "Percentage humidity",
           "type" : "number",
           "minimum" : 0,
           "maximum" : 100,
           "default" : 0.0
       }
   },
   "required" : [
       "temperature",
       "humidity"
   ]
}
```  
## 手順 5: アプリケーション・インターフェース・スキーマ・リソースを作成する  
{: #crt_ai_schema_resource}  
以下の API を使用して、前の手順で作成したアプリケーション・インターフェース・スキーマ・ファイルをアップロードします。これにより、モノのタイプのためのアプリケーション・インターフェース・スキーマ・リソースが作成されます。  
```
POST /schemas
```  
次のパラメーターが必要です。  
<table>
<tr>
<th>パラメーター</th><th>説明</th>
</tr>
<tr>
<td>name
</td><td>作成するアプリケーション・インターフェース・スキーマの名前を指定します。</td>
</tr>
<tr>
<td>schemaFile
</td><td>ローカルのアプリケーション・インターフェース・スキーマ JSON ファイルへのパス。
</td>
</tr>
</table>  

詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) の資料を参照してください。  

<!-- The following example shows how to use Python to create the thing type application interface schema resource:  
```python
roomSchemaFile = open(schemasDir + "room.json", "r");
roomSchema = roomSchemaFile.read();
roomSchemaFile.close();
"roomSchemaId", result = api.createSchema("Room Schema", "room.json", roomSchema)
```  -->

スキーマ ID を使用して、モノのタイプのためのアプリケーション・インターフェースにアプリケーション・インターフェース・スキーマ・リソースを追加します。
  

## 手順 6: モノのタイプのためのアプリケーション・インターフェースを作成する  
{: #crt_thing_ai}  
アプリケーション・インターフェースで、前の手順で作成したアプリケーション・インターフェース・スキーマ・リソースを参照する必要があります。  
アプリケーション・インターフェースを作成するには、以下の API を使用します。  
```
POST /applicationinterfaces
```  
次のパラメーターが必要です。  
<table>
<tr>
<th>	パラメーター</th><th>	説明</th>
</tr>
<tr>
<td>	name
</td><td>	作成するアプリケーション・インターフェースの名前を指定します。</td>
</tr>
<tr>
<td>	description
</td><td>	アプリケーション・インターフェースの説明を指定します。</td>
</tr>
<tr>
<td>	schemaId
</td><td>	ローカルのアプリケーション・インターフェース・スキーマ JSON ファイルへのパス。
</td>
</tr>
</table>  

詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces) の資料を参照してください。  
アプリケーション・インターフェースにアプリケーション・インターフェース・スキーマを追加する際には、前の応答で返されたスキーマ ID を使用します。  

<!-- The following example shows how to use Python to create an application interface:  
```python
"applicationInterfaceId", result = api.createApplicationInterface("IRoom", "roomSchemaId")
```  -->

デバイス・タイプにアプリケーション・インターフェースを追加する際には、アプリケーション・インターフェース ID を使用します。インバウンド・デバイス・イベントをアプリケーション・インターフェースで定義するプロパティーに対応付ける時にも、この ID を使用します。

  

## 手順 7: モノのタイプにアプリケーション・インターフェースを追加する  
{: #add_thing_ai}  
モノのタイプにアプリケーション・インターフェースを追加するには、以下の API を使用します。  
```
POST /thing/types/{thingtypeId}/applicationinterfaces
```  
次のパラメーターが必要です。  
<table>
<tr>
<th>	パラメーター</th><th>	説明</th>
</tr>
<tr>
<td>	id
</td><td>	モノのタイプ用に作成した ID。</td>
</tr>
<tr>
<td>	name
</td><td>	作成するアプリケーション・インターフェースの名前を指定します。</td>
</tr>
<tr>
<td>	schemaId
</td><td>	アプリケーション・インターフェース・リソース用に作成した ID。</td>
</tr>
<tr>
<td>	refs/schema
</td><td>	アプリケーション・インターフェース・リソースへのパス。通常: /schemas/*schemaId*	</td>
</tr>
</table>  

詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) の資料を参照してください。  
このシナリオでは、アプリケーション・インターフェースにモノのタイプ *RoomType* を関連付けます。

<!-- The following example shows how to use Python to add the thing application interface to the thing type *RoomType*:  
```python
result = api.addApplicationInterfaceToThingType(RoomType, "applicationInterfaceId", "roomSchemaId")
``` -->

## 手順 8: マッピングを定義する
{: #define_Thing_type_mappings}

モノのタイプのマッピングを定義します。これにより、集約されたデバイスまたはモノの状態のプロパティーを、モノのタイプのアプリケーション・インターフェースで定義されているプロパティーにマップする方法を記述します。

イベントをマップするには、以下の API を使用します。  
```
POST /thing/types/{thingtypeId}/mappings
```  

次のパラメーターが必要です。  
<table>
<tr>
<th>	パラメーター</th><th>	説明</th>
</tr>
<tr>
<td>	applicationInterfaceId
</td><td>	アプリケーション・インターフェース用に作成した ID。
</td>
</tr>
<tr>
<td>	propertyMappings
</td><td>	アプリケーション・インターフェースに定義されたプロパティーとデバイス・イベント・ペイロードのプロパティーをマップする有効な JSON 構造。</td>
</tr>
</table>  

詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) の資料を参照してください。

<!--  The following example shows how to use Python to add a mapping to thing type *RoomType*:

```python
mappings = {
     "humiditySensor": {
       "humidity": "$event.humidity"
     },
     "temperatureSensor": {
       "temperature": "$event.temperatureC"
     }
 }

 result = api.addMappingsToThingType(thingType, "applicationInterfaceId", mappings)
``` -->

以下の例は、propertyMappings パラメーター項目のサンプルを示しています。

```
{
  "applicationInterfaceId": "58dd849752faff0001638851",
  "propertyMappings": {
       "humiditySensor": {
         "humidity": "$event.humidity"
       },
       "temperatureSensor": {
         "temperature": "$event.temperatureC"
       }
   }
}
```

*humiditySensor* はモノのスキーマ内で定義されています。「$event.humidity」は、ID が「58c135ea52faff0001678f06」のアプリケーション・インターフェース・スキーマ内で定義されています。*temperatureSensor* はモノのスキーマ内で定義されています。「$event.temperatureC」は、ID が「58c135e352faff0001198a89」のアプリケーション・インターフェース・スキーマ内で定義されています。

## 手順 9: モノのタイプに関連付けられた構成をデプロイする  
{: #deploy_Thing_config}   
モノの各タイプのモノの状態の更新に関連した構成をデプロイします。この構成には、スキーマ、アプリケーション・インターフェース、マッピングが含まれています。

モノのタイプのインスタンスを作成する前に、モノのタイプの構成をデプロイしなければなりません。

モノのタイプの構成をデプロイするには、以下の API を使用します。

```
PATCH /thing/types/{thingtypeId}
```
詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) の資料を参照してください。<!-- The following example shows how to use Python to deploy your configuration for thing type *Room*:

```python
result = api.deployThingTypeConfiguration(thingType)
``` -->

## 手順 10: モノのタイプのインスタンスを作成する
{: #create_Thing_instances}

「モノ」とは、「モノのタイプ」のインスタンスです。モノを使用すると、デバイスやモノの 1 つ以上のインスタンスを集約して 1 つのオブジェクトにすることができます。

モノを作成するには、以下の API を使用します。

```
POST /thing/types/{thingTypeId}/things
```

次のパラメーターが必要です。  
<table>
<tr>
<th>	パラメーター</th><th>	説明</th>
</tr>
<tr>
<td>	typeId
</td><td>		事前に作成したモノのタイプの ID。</td>
</tr>
<tr>
<td>	thingId
</td><td>	作成するモノのインスタンスの名前を指定します。</td>
</tr>
</table>

詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Things) の資料を参照してください。

このシナリオでは、モノ・タイプが *RoomType* のモノ・インスタンスを 2 つ作成する必要があります。一方のモノ・インスタンスを *meetingroom1* と呼び、もう一方のモノ・インスタンスを *meetingroom2* と呼びます。

<!-- The following example shows how to use Python to create a thing instance that is called *meetingroom1*. *meetingroom1* is associated with the *temperatureSensor1* and *humiditySensor1* device instances.

```python
thingId = "meetingroom1"
 meetingroom1AggregatedObjects = {
   "temperatureSensor": {
     "type": "device",
     "typeId": "TemperatureSensor",
     "id": "temperatureSensor1"
   },
   "humiditySensor": {
     "type": "device",
     "typeId": "HumiditySensor",
     "id": "humiditySensor1"
   }
 }
 result = api.createThing(thingType, thingId, "Meeting Room 1", "The big meeting room!!!", aggregatedObjects = meetingroom1AggregatedObjects)
``` -->

作成されたモノの ID を、モノのアプリケーション・インターフェースに温度イベントを追加するときに呼び出す POST メソッドの URL で使用します。

<!-- The following example shows how to use Python to create a thing instance that is called *meetingroom2*. *meetingroom2* is associated with the *temperatureSensor2* and *humiditySensor2* device instances.

```python
thingId = "meetingroom2"
   meetingroom2AggregatedObjects = {
    "temperatureSensor": {
      "type": "device",
      "typeId": "TemperatureSensor",
      "id": "temperatureSensor2"
    },
    "humiditySensor": {
      "type": "device",
      "typeId": "HumiditySensor",
      "id": "humiditySensor2"
    }
  }
result = api.createThing(thingType, thingId, "Meeting Room 2", "The little meeting room!!!", aggregatedObjects = meetingroom2AggregatedObjects)  
``` -->

## 手順 11: マップしたデバイス・イベントがアプリケーション・インターフェースにパブリッシュされることを確認する  
{: #publish_event}  
モノ *meetingroom1* に集約されるデバイスに関する以下のイベントをパブリッシュします。  
 - *temperatureSensor1* の温度イベントをトピック `iot-2/evt/tevt/fmt/json` に  
 - *humiditySensor1* の湿度イベントをトピック `iot-2/evt/hevt/fmt/json` に  
モノ *meetingroom2* に集約されるデバイスに関する以下のイベントをパブリッシュします。  
 - *temperatureSensor2* の温度イベントをトピック `iot-2/evt/tempevt/fmt/json` に  
 - *humiditySensor2* の湿度イベントをトピック `iot-2/evt/humevt/fmt/json` に  
デバイスからインバウンド・イベントをパブリッシュする方法については、[アプリケーションの MQTT 接続](../applications/mqtt.html#publishing_device_events)を参照してください。  

## 手順 12: モノの状態が変更されたことを確認する  
{: #verify_Thing_state}  
モノの状態を確認するには、以下の API を使用します。  
```
GET /thing/types/{thingTypeId}/things/{thingId}/state/{applicationInterfaceId}
```  

次のパラメーターが必要です。  
<table>
<tr>
<th>パラメーター</th><th>	説明</th>
</tr>
<tr>
<td>thingtypeId
</td><td>モノのタイプ ID。</td>
</tr>
<tr>
<td>thingId
</td><td>	モノの ID。</td>
</tr>
<tr>
<td>applicationInterfaceId
</td><td>アプリケーション・インターフェース用に作成した ID。
</td>
</tr>
</table>  

詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) の資料を参照してください。  

<!-- The following example shows how to use Python to retrieve the current state of *meetingroom1* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom1", applicationInterfaceId)
```  
The following example shows how to use Python to retrieve the current state of *meetingroom2* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom2", applicationInterfaceId)
``` -->
