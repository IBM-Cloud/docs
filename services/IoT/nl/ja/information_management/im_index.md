---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# インターフェースを使用してデバイス・データをマップする方法 (ベータ)
{: #im_index}

{{site.data.keyword.iot_full}} のインターフェース・マッピング機能を使用して、着信/発信のデバイス・データを編成したり統合したりできます。
{:shortdesc}

**重要:** インターフェース・マッピング機能は、現時点ではベータ機能としてのみ提供されます。最終リリースの前は、ベータ版の更新によって、現行バージョンと互換性のない変更が行われる可能性があります。最終リリースになるまでは、ベータ機能を実動アプリケーションで使用しないよう強くお勧めします。このベータ版についてさらに情報を得たりフィードバックを送ったりすることを望まれる場合は、[IM ベタ・プログラムの登録 ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/software/support/trial/cst/forms/nomination.wss?id=7050){: new_window} を行って、ご意見をお寄せください。

## 概説
{: #overview}

インターフェース・マッピング機能を使用して、アプリケーション用のインターフェースを開発できます。{{site.data.keyword.iot_short_notm}} に接続するデバイスやセンサーにはさまざまなタイプや型、モデルがあり、それぞれのタイプごとに、データ・パブリッシュの形式が異なる場合もあります。インターフェース・マッピング機能を使用して、デバイスの接続方法の違いから生じる複雑な処理を切り離すことにより、着信データを正規化してアプリケーションを簡略化できます。

例えば、2 種類の温度センサーがあるとします。温度を摂氏で測定するセンサーと、華氏で測定するセンサーです。

![温度センサー・デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションのマッピング。](images/Information "温度センサー・デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションのマッピング")

温度センサー 1 は、`{ "t" : 34.5 }` という読み取り値を {{site.data.keyword.iot_short_notm}} にパブリッシュします。これは摂氏の読み取り値です。温度センサー 2 は、`{ "temp" : 72.55 }` という読み取り値を {{site.data.keyword.iot_short_notm}} にパブリッシュします。この温度センサーはタイプが異なっており、華氏の読み取り値になります。これらの読み取り値は、別々のイベントとして {{site.data.keyword.iot_short_notm}} にパブリッシュされます。

インターフェース・マッピング機能を使用すれば、これらの読み取り値を一定の形式に正規化して処理できます。温度のそれぞれの単位を取得したり変換したりするアプリケーションを作成する必要はありません。アプリケーション側では、正規化した 1 つのビューを受け取り、**t** と **temp** の両方に接続する代わりに **temperature** に接続できます。

## デバイスとアプリケーションの間のデータ・フロー
{: #mapping}

インターフェース・マッピング機能で各リソースをどのように使用するのかを以下のフロー・ダイアグラムにまとめます。

![デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションの間のフロー。](images/Information "デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションの間のフロー")

このフローでスキーマを使用する方法を以下の図にまとめます。

![デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションの間のフロー。](images/Information "デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションの間のフロー")

着信イベントと[デバイス状態](#key_concepts)の形式を定義したり検証したりするために、JSON スキーマを使用します。そのスキーマの詳細については、[スキーマ](#resources)を参照してください。

## 重要概念
{: #key_concepts}

インターフェース・マッピング機能は、[デバイス・タイプ](#resources)という現在の概念に物理インターフェース・リソースとアプリケーション・インターフェース・リソースを追加して、{{site.data.keyword.iot_short_notm}} を流れるデータの制御を強化するための拡張機能です。

デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションを[リソース](#resources)によって対応付ける論理マッピングを以下の図にまとめます。

![デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションの論理マッピング。](images/im_mapping.svg "デバイスと {{site.data.keyword.iot_short_notm}} 上のアプリケーションの論理マッピング")

インターフェース・マッピングは、デバイス状態という概念に関連しています。デバイス状態は、アプリケーション・インターフェースで定義する一連のプロパティーに基づいています。そのようなプロパティーの最新の値が {{site.data.keyword.iot_short_notm}} に格納されており、アプリケーション側では、HTTP API を使用してその値を要求できます。

インバウンド・イベントのデータを処理して、インバウンド・イベントのプロパティーをアプリケーション・インターフェースのプロパティーにマップするには、以下の情報を構成する必要があります。

- 1 つ以上のインバウンド・イベントの構造。イベント・スキーマによってこの情報を定義します。各イベント・スキーマで 1 つのインバウンド・イベントの構造を定義し、各イベント・スキーマを 1 つのイベント・タイプに関連付けます。1 つ以上のイベント・タイプを物理インターフェースでグループ化します。

    インバウンド・デバイス・イベントに含まれているデータの形式の構造は、JSON スキーマ形式のイベント・スキーマ・ファイルで定義します。POST メソッドを使用してイベント・スキーマ・ファイルを {{site.data.keyword.iot_short_notm}} にアップロードすれば、名前を設定したスキーマ・リソースを作成できます。ベータ版では、どのインバウンド・イベントも JSON 形式でなければなりません。

- 対象のデバイス状態の構造。アプリケーション・インターフェース・スキーマによってこの情報を定義します。

    デバイス状態とは、アプリケーション側が設定に基づいてデバイスから受け取るデータ構造とデータを記述したものです。デバイス状態として格納されるプロパティー値は、インバウンド・デバイス・イベントへの応答として更新されます。アプリケーション側は、HTTP API を使用してデバイス状態の最新の値を要求できます。

- インバウンド・イベントを望ましいデバイス状態にマップする方法についての情報。マッピングによってこの情報を定義します。

    インバウンド・イベントのプロパティーに含まれているデータをアプリケーション・インターフェースの該当プロパティーに対応付けるには、マッピングを作成する必要があります。そのマッピングでは、デバイスからのインバウンド・イベントへの応答として特定のアプリケーション・インターフェースのプロパティーをどのように更新するかを定義します。


## リソース
{: #resources}

REST API を使用すれば、前の図に含まれているリソースを管理できます。REST API については、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window} の資料を参照してください。

リソース                        | 説明       
------------- | ------------- | -------------  
スキーマ                         | JSON スキーマを使用して、デバイスから {{site.data.keyword.iot_short_notm}} にパブリッシュするインバウンド・イベントの構造と、望ましいデバイス状態を定義します。JSON スキーマの詳細については、[JSON スキマ ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://json-schema.org/){: new_window} を参照してください。インターフェース・マッピングでは、2 つの JSON スキーマを参照します。イベント・スキーマとアプリケーション・インターフェース・スキーマです。イベント・スキーマでは、デバイスから {{site.data.keyword.iot_short_notm}} にパブリッシュするイベントの構造を定義します。アプリケーション・インターフェースが参照するアプリケーション・インターフェース・スキーマでは、{{site.data.keyword.iot_short_notm}} に格納する [デバイス状態](#key_concepts)の構造を定義します。
イベント・タイプ                         | {{site.data.keyword.iot_short_notm}} で特定のイベントに含まれているデータを処理するために、組織内でイベント・タイプを作成しなければなりません。どのイベント・タイプもイベント・スキーマを参照する必要があります。ベータ版では、どのインバウンド・イベントも JSON 形式でなければなりません。   
物理インターフェース                         | 1 つ以上のイベント・タイプに物理インターフェースを関連付けることが可能です。物理インターフェースでは、どのイベント・タイプにどのデバイス・タイプを関連付けるかを定義します。  
デバイス・タイプ                         | Watson IoT Platform に接続するあらゆるデバイスには、デバイス・タイプが関連付けられています。デバイス・タイプとは、特性や動作を共有するデバイス・グループのことです。インターフェース・マッピングでは、デバイス・タイプを拡張して、デバイスの物理インターフェースと、デバイス状態を取得するために使用するアプリケーション・インターフェースを組み込みます。1 つのデバイス・タイプに複数のアプリケーション・インターフェースを設定することもできます。デバイス・タイプの詳細については、[デバイス・モデル](../reference/device_model.html#id_and_device_types)の「ID とデバイス・タイプ」の項を参照してください。
アプリケーション・インターフェース                         | アプリケーション・インターフェースでは、アプリケーション・インターフェース・スキーマを参照しなければなりません。デバイス状態として格納するデータの構造をアプリケーション・インターフェースで定義できます。デバイス状態とは、アプリケーション側が設定に基づいてデバイスから受け取るデータ構造とデータを記述したものです。マッピングを定義する前に、デバイス・タイプに少なくとも 1 つのアプリケーション・インターフェースを関連付ける必要があります。
マッピング                         | マッピングでは、インバウンド・イベントに関連するプロパティーを特定のアプリケーション・インターフェースで定義するプロパティーに対応付ける方法を定義します。対象のアプリケーション・インターフェースの ID をマッピングで指定し、そのアプリケーション・インターフェースをマッピングの追加対象のデバイス・タイプに関連付ける必要があります。
## ワークフローの概要
{: #workflow}



### このタスクについて

デバイス・データのインターフェース・マッピングを開始するのに必要なリソースを構成する手順を以下にまとめます。

API の詳細については、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window} の資料を参照してください。
各手順の詳細については、[サンプル・シナリオ](#scenario)を参照するか、サンプル・シナリオ内の各手順への直接リンクを使用してください。

### デバイス・データのインターフェース・マッピングを開始するための環境を構成します。

1.  必要に応じて、デバイス・タイプとデバイスを追加します。

  1. デバイス・タイプを作成します。以下の URI で REST API POST メソッドを使用してください。
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types
      ```
  2.  必要に応じて、デバイスを追加します。  
デバイス・タイプとデバイスを追加するための詳細情報については、[デバイスの接続](../iotplatform_task.html#devices)を参照してください。

2. 物理インターフェースを作成します。

  1. [イベント・スキーマ・ファイルを作成します](#step1)。イベント・スキーマ・ファイルは、インバウンド・イベントの構造と形式を定義したローカル .JSON ファイルです。

  2. [イベント・タイプのイベント・スキーマ・リソースを作成します](#step2)。以下の URI で REST API POST メソッドを使用してください。
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
      ```  

  3. [イベント・スキーマを参照するイベント・タイプを作成します](#step3)。以下の URI で REST API POST メソッドを使用してください。
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/event/types
      ```
イベント・スキーマにイベント・タイプを追加します。その際に、イベント・スキーマ・リソースの作成時に使用した POST メソッドへの応答で返されたスキーマ ID を使用してください。

  4. [物理インターフェースを作成します](#step7)。以下の URI で REST API POST メソッドを使用してください。
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces
        ```

   5. [物理インターフェースにイベント・タイプを追加します](#step8)。以下の URI で REST API POST メソッドを使用してください。
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/{physicalInterfaceId}/events
        ```

       物理インターフェースにイベント・タイプを追加します。その際に、トピックから送られてくる *eventId* と、イベント・タイプの作成時に使用した POST メソッドへの応答で返されたイベント・タイプ ID *eventTypeId* を使用してください。       

3. デバイス・タイプに物理インターフェースを追加します。       

      [デバイス・タイプを更新して物理インターフェースに接続します](#step9)。以下の URI で REST API PUT メソッドを使用してください。
     ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

4. アプリケーション・インターフェースを作成します。

  1. [アプリケーション・インターフェース・スキーマ・ファイルを作成します](#step4)。アプリケーション・インターフェース・スキーマ・ファイルは、デバイス状態を定義したローカル .JSON ファイルです。

  2. [アプリケーション・インターフェース・スキーマ・リソースを作成します](#step5)。以下の URI で REST API POST メソッドを使用してください。
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
        ```     

  3. [アプリケーション・インターフェース・スキーマを参照するアプリケーション・インターフェースを作成します](#step6)。以下の URI で REST API POST メソッドを使用してください。
         ```
         https://**orgId**.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces
         ```  

        アプリケーション・インターフェースでは、アプリケーション・インターフェース・スキーマ・リソースの作成時に使用した POST メソッドへの応答で返されたスキーマ ID を使用して、アプリケーション・インターフェース・スキーマを参照します。

  4. [デバイス・タイプにアプリケーション・インターフェースを追加します](#step10)。以下の URI で REST API POST メソッドを使用してください。
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/types/{typeId}/applicationinterfaces
        ```

        デバイス・タイプにアプリケーション・インターフェースを追加します。その際に、アプリケーション・インターフェースの作成時に使用した POST メソッドへの応答を使用してください。

5. デバイス・タイプのマッピングを定義します。

  [インバウンド・イベントのプロパティーとアプリケーション・インターフェースのプロパティーを対応付けるマッピングを定義します](#step11)。以下の URI で REST API POST メソッドを使用してください。       
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/mappings/{applicationInterfaceId}
      ```

6. デバイス・タイプに関連する構成をデプロイします。

  [構成を {{site.data.keyword.iot_short_notm}} にデプロイします](#step15)。以下の URI で REST API PATCH メソッドを使用してください。
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
      ```

7. マップしたデバイス・イベントがアプリケーション・インターフェースにパブリッシュされることを確認します。

  1. [インバウンド・デバイス・イベントをパブリッシュします](#step12)。

  2. [デバイス状態が変更されたことを確認します](#step13)。以下の URI で REST API GET メソッドを使用してください。
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
        ```

## サンプル・シナリオ
{: #scenario}

以下の情報に基づいてシナリオを作成します。そのシナリオでは、2 つの温度センサーが {{site.data.keyword.iot_short_notm}} にイベントをパブリッシュします。1 つは温度を摂氏で測定するセンサーです。もう 1 つは温度を華氏で測定するセンサーです。それぞれの読み取り値を 1 つの摂氏の読み取り値に対応付けます。それぞれのデバイスから新しい読み取り値がパブリッシュされると、デバイス状態に関連するプロパティーの値が変更されます。

### 前提条件

{{site.data.keyword.iot_short_notm}} 組織インスタンスとその組織の API キーまたはトークンが必要です。API キーやトークンの詳細については、[アプリケションの HTTP REST API](../applications/api.html#authentication) を参照してください。

### このシナリオについて

このシナリオでは、2 つのデバイスを構成します。

1 つは *TemperatureSensor1* というデバイスです。このデバイスは、摂氏で測定した温度イベントをパブリッシュします。温度イベントのパブリッシュ先は `iot-2/evt/tevt/fmt/json` というトピックであり、ペイロードは以下のようになります。
```
{
  "t" : 34.5
}
```

**注:** イベント ID は *tevt* です。この ID は、このタイプの温度イベントを物理インターフェースに追加する時と、このタイプのインバウンド・イベントに関連するプロパティーをアプリケーション・インターフェースのプロパティーに対応付けるマッピングを定義する時に必要になります。このシナリオでは、アプリケーション・インターフェースで **temperature** というプロパティーを定義します。

もう 1 つは *TemperatureSensor2* というデバイスです。このデバイスは、華氏で測定した温度イベントをパブリッシュします。温度イベントのパブリッシュ先は `iot-2/evt/tempevt/fmt/json` というトピックであり、ペイロードは以下のようになります。
```
{
  "temp" : 72.55
}
```

**注:** イベント ID は *tempevt* です。この ID は、このタイプの温度イベントを物理インターフェースに追加する時と、このタイプのインバウンド・イベントに関連するプロパティーをアプリケーション・インターフェースのプロパティーに対応付けるマッピングを定義する時に必要になります。このシナリオでは、アプリケーション・インターフェースで **temperature** というプロパティーを定義します。

アプリケーション・インターフェースも構成します。このアプリケーション・インターフェースでは、このタイプのデバイスの状態を以下の構造で記述します。
```
{
  "temperature" : <現在の温度の値 (摂氏)>
  }
```
この場合は、**temperature** に関連する値を処理するアプリケーションを構成します。**t** に関連する値を処理したり、**temp** に関連する値を摂氏に変換してから処理したりするアプリケーションを構成するわけではありません。

## 手順

以下の情報に基づいて、インターフェースを使用したサンプル・シナリオを構成します。

### 必要に応じて、デバイス・タイプとデバイスを追加します。
{: #step14}

このシナリオでは、2 つのデバイス・タイプと 2 つのデバイス・インスタンスを想定します。デバイス・インスタンス *TemperatureSensor1* は、デバイス・タイプ *EnvSensor1* に関連付けます。デバイス・インスタンス *TemperatureSensor2* は、デバイス・タイプ *EnvSensor2* に関連付けます。

HTTP API を使用してデバイス・タイプを追加する方法については、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Type_Configuration){: new_window} の資料を参照してください。

### イベント・スキーマ・ファイルを作成します。
{: #step1}

このシナリオでは、2 つのイベント・スキーマ・ファイルを作成して、それぞれのインバウンド温度イベントの構造を定義します。

*tEventSchema.json* というスキーマ・ファイルを作成する例を以下に示します。このファイルでは、温度を摂氏で測定する温度センサーから送られてくるインバウンド・イベントの構造を定義します。

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : "defines the structure of a temperature event in degrees Celsius",
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

イベント・タイプのイベント・スキーマ・リソースを作成する時には、*tEventSchema* というスキーマ・ファイル名を使用します。

*tempEventSchema.json* というスキーマ・ファイルを作成する例を以下に示します。このファイルでは、温度を華氏で測定する温度センサーから送られてくるインバウンド・イベントの構造を定義します。

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : "defines the structure of a temperature event in degrees Fahrenheit",
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

### イベント・タイプのイベント・スキーマ・リソースを作成します。
{: #step2}

イベント・スキーマ・リソースを作成するには、以下の API を使用します。

```
POST /schemas
```
詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas){: new_window} の資料を参照してください。

cURL を使用して *tEventSchema.json* というイベント・スキーマ・リソースを作成する例を以下に示します。

```
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
  "name" : "tEventSchema",
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

### イベント・スキーマを参照するイベント・タイプを作成します。
{: #step3}

各イベント・タイプでは、イベント・スキーマ・リソースの作成時に使用した POST メソッドへの応答で返されたスキーマ ID を使用して、該当するイベント・スキーマを参照します。

イベント・タイプを作成するには、以下の API を使用します。

```
POST /event/types
```

詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Event_Types){: new_window} の資料を参照してください。


cURL を使用して、摂氏で測定する温度イベントのイベント・タイプを作成する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d"}'
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
  "name" : "tempEvent",
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
物理インターフェースにイベント・タイプを追加する時には、この POST メソッドへの応答で返されたイベント・タイプ ID *5846d2846522050001db0e10* を使用します。
### 物理インターフェースを作成します。
{: #step7}

物理インターフェースを作成するには、以下の API を使用します。

```
POST /physicalinterfaces
```
詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Physical_Interfaces){: new_window} の資料を参照してください。

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

### 物理インターフェースにイベント・タイプを追加します。
{: #step8}

物理インターフェースにイベント・タイプを追加するには、以下の API を使用します。

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```
詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Physical_Interfaces){: new_window} の資料を参照してください。

このシナリオでは、以下のイベント・タイプを指定の物理インターフェースに追加します。
- 摂氏の温度イベント *tevt* を ID *5847d1df6522050001db0e1a* の物理インターフェースに追加します。その際に、トピックから送られてくる *eventId* と、イベント・スキーマ・リソースの作成時に返される *eventTypeId* を使用します。
- 華氏の温度イベント *tempevt* を ID *5847d1df6522050001db0e1b* の物理インターフェースに追加します。その際に、トピックから送られてくる *eventId* と、イベント・スキーマ・リソースの作成時に返される *eventTypeId* を使用します。


cURL を使用して、温度イベント *tevt* を ID *5847d1df6522050001db0e1a* の物理インターフェースに追加する例を以下に示します。

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
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
  "eventId" : "tempevt"
}
```

### デバイス・タイプを更新して物理インターフェースに接続します。
{: #step9}

デバイス・タイプを更新するには、以下の API を使用します。

```
PUT /device/types/{typeId}
```

詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window} の資料を参照してください。

このシナリオでは、デバイス・タイプ *EnvSensor1* を更新して物理インターフェース *5847d1df6522050001db0e1a* に接続し、デバイス・タイプ *EnvSensor2* を更新して物理インターフェース *5847d1df6522050001db0e1b* に接続します。

cURL を使用してデバイス・タイプ *EnvSensor1* を更新する例を以下に示します。

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a"}’
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
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b"}’
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
### アプリケーション・インターフェース・スキーマ・ファイルを作成します。
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

### アプリケーション・インターフェース・スキーマ・リソースを作成します。
{: #step5}

アプリケーション・インターフェース・スキーマ・リソースを作成するには、以下の API を使用します。

```
POST /schemas
```
詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas){: new_window} の資料を参照してください。cURL を使用してアプリケーション・インターフェース・スキーマを作成する例を以下に示します。

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
### アプリケーション・インターフェース・スキーマを参照するアプリケーション・インターフェースを作成します。
{: #step6}

アプリケーション・インターフェースを作成するには、以下の API を使用します。

```
POST /applicationinterfaces
```
詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces){: new_window} の資料を参照してください。

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

### デバイス・タイプにアプリケーション・インターフェースを追加します。
{: #step10}

デバイス・タイプにアプリケーション・インターフェースを追加するには、以下の API を使用します。

```
POST /device/types/{typeId}/applicationinterfaces
```
詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window} の資料を参照してください。このシナリオでは、アプリケーション・インターフェースにデバイス・タイプ *EnvSensor1* と *EnvSensor2* を関連付けます。

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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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

### インバウンド・イベントのプロパティーをアプリケーション・インターフェースのプロパティーに対応付けるためのマッピングを定義します。
{: #step11}

イベントをマップするには、以下の API を使用します。

```
POST /device/types/{typeId}/mappings
```
詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window} の資料を参照してください。このシナリオでは、デバイス・タイプ *EnvSensor1* のマッピングを定義して、インバウンド・イベント *tevt* のプロパティー **t** をアプリケーション・インターフェースのプロパティー **temperature** に対応付けます。また、デバイス・タイプ *EnvSensor2* のマッピングを定義して、インバウンド・イベント *tempevt* のプロパティー **temp** をアプリケーション・インターフェースのプロパティー **temperature** に対応付けます。

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

### 構成をデプロイします。
{: #step15}

各デバイス・タイプのデバイス状態の更新に関連した構成をデプロイします。この構成には、スキーマ、イベント・タイプ、物理インターフェース、アプリケーション・インターフェース、マッピングが含まれています。

デバイス・タイプ構成をデプロイするには、以下の API を使用します。

```
PATCH /device/types/{typeId}
```
詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window} の資料を参照してください。このシナリオでは、2 つのデバイス・タイプの構成をデプロイする必要があります。

cURL を使用してデバイス・タイプ *EnvSensor1* の構成をデプロイする例を以下に示します。

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
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

### インバウンド・デバイス・イベントをパブリッシュします。
{: #step12}

*TemperatureSensor1* からトピック `iot-2/evt/tevt/fmt/json`に温度イベントをパブリッシュし、*TemperatureSensor2* からトピック `iot-2/evt/tempevt/fmt/json` に温度イベントをパブリッシュします。

デバイスからインバウンド・イベントをパブリッシュする方法については、[アプリケションの MQTT 接続](../applications/mqtt.html#publishing_device_events)を参照してください。


### デバイス状態が変更されたことを確認します。
{: #step13}

デバイス状態を確認するには、以下の API を使用します。
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```
詳しくは、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types){: new_window} の資料を参照してください。cURL を使用して *TemperatureSensor1* の現在の状態を取得する例を以下に示します。その際に、作成したアプリケーション・インターフェースの ID を参照します。

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
