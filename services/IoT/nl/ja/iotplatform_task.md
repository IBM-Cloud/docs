---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# デバイスの接続
{: #iotplatform_task}

IoT デバイスからデータを受信する操作を開始するには、その前にデバイスを {{site.data.keyword.iot_full}} に接続する必要があります。デバイスを {{site.data.keyword.iot_short_notm}} に接続するには、まずデバイスを {{site.data.keyword.iot_short_notm}} に登録してから、登録情報を使用してデバイスを {{site.data.keyword.iot_short_notm}} に接続するための構成を行います。
{:shortdesc}

## 始めに
{: #byb}

接続プロセスを開始する前に、デバイスが {{site.data.keyword.iot_short_notm}} と通信するための以下の要件を満たしていることを確認する必要があります。

- デバイスは、HTTP プロトコルまたは MQTT プロトコルを使用して通信できるようでなければなりません。
- デバイス・メッセージは、{{site.data.keyword.iot_short_notm}} のメッセージ・ペイロードの要件に準拠していなければなりません。

詳細については、[Watson IoT Platform でのデバイスの開発](https://console.ng.bluemix.net/docs/services/IoT/devices/device_dev_index.html)を参照してください。

デバイスを {{site.data.keyword.iot_short_notm}} に接続するには、以下の手順を実行します。

## 手順 1: デバイスを {{site.data.keyword.iot_short_notm}} に登録する  
{: #iotplatform_subtask1}

デバイスを登録するには、デバイスをデバイス・タイプごとに分類し、デバイスに名前を付けて、デバイス情報を指定します。その後、接続トークンを指定するか、{{site.data.keyword.iot_short_notm}} によって生成されるトークンを受け入れます。

{{site.data.keyword.iot_short_notm}} ダッシュボードを使用する場合は、一度に 1 つずつデバイスを追加します。[{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/post_bulk_devices_add) を使用する場合は、一度に 1 つ以上のデバイスを追加できます。

{{site.data.keyword.iot_short_notm}} ダッシュボードからデバイスを追加するには、以下のようにします。

1. {{site.data.keyword.Bluemix}} ダッシュボードで {{site.data.keyword.iot_short_notm}} サービスのタイルをクリックしてサービスのダッシュボードを開くか、次の URL を使用してダッシュボードに直接アクセスします。

 `https://org_id.internetofthings.ibmcloud.com/dashboard/#/overview `

    *org_id* は、{{site.data.keyword.Bluemix}} 組織の ID です。

2. サービスのページで**「ダッシュボードを起動」**をクリックして、{{site.data.keyword.iot_short_notm}} 組織の管理作業を開始します。

3. 「概要」ダッシュボードのメニュー・ペインから**「デバイス」**を選択し、**「デバイスの追加」**をクリックします。
5. 追加するデバイスのデバイス・タイプを選択するか作成します。
  
{{site.data.keyword.iot_short_notm}} に接続する各デバイスには、デバイス・タイプを関連付ける必要があります。デバイス・タイプとは、共通の特性を共有するデバイス・グループのことです。  
最初のデバイスを {{site.data.keyword.iot_short_notm}} 組織に追加する時点では、**「デバイス・タイプ」**メニューにデバイス・タイプが表示されません。まずデバイス・タイプを作成する必要があります。
 1. **「デバイス・タイプの作成」**をクリックします。
 2. デバイス・タイプ名 (`my_device_type` など) とそのデバイス・タイプの説明を入力します。
   
 **重要:** デバイス・タイプ名は 36 文字以下でなければなりません。以下の文字だけを含めることができます。
 <ul>
  <li>英数字 (a-z、A-Z、0-9)</li>
  <li>ハイフン (-)</li>
  <li>下線 (&lowbar;)</li>
  <li>ピリオド (.)</li>
  </ul>
 3. オプション: デバイス・タイプの属性やメタデータを入力します。
     
 **ヒント:** 属性とメタデータは、後で追加したり編集したりすることもできます。
 4. **「作成」**をクリックして、新しいデバイス・タイプを追加します。
10. **「次へ」**をクリックして、選択したデバイス・タイプのデバイスを追加するプロセスを開始します。
11. デバイス ID を入力します (`my_first_device` など)。
  
デバイス ID は、{{site.data.keyword.iot_short_notm}} ダッシュボードでデバイスを識別するために使用され、デバイスを {{site.data.keyword.iot_short_notm}} に接続するための必須パラメーターでもあります。  
**重要:** デバイス ID は 36 文字以下でなければなりません。以下の文字だけを含めることができます。
 <ul>
 <li>英数字 (a-z、A-Z、0-9)</li>
 <li>ハイフン (-)</li>
 <li>下線 (&lowbar;)</li>
 <li>ピリオド (.)</li>  
 </ul>
 **ヒント:** ネットワークに接続されたデバイスの場合は、デバイス MAC アドレス (区切り文字のコロンは付けない) などをデバイス ID として入力できます。  
12. オプション: **「追加フィールド」**をクリックして、シリアル番号、製造元、型式などのデバイス情報を追加します。
   
 **ヒント:** この情報は、後で追加したり編集したりすることもできます。
12. オプション: デバイスの JSON メタデータを入力します。
   
 **ヒント:** デバイスのメタデータは、後で追加したり編集したりすることもできます。
13. **「次へ」**をクリックして、デバイスの追加を完了します。
14. 要約情報が正しいことを確認してから、**「追加」**をクリックして接続を追加します。
  
**ヒント:** 自動生成の認証トークンを受け入れることも、自分で認証トークンを指定することもできます。  
自分でトークンを作成する場合は、長さを 8 文字から 36 文字にして、英数字と以下の特殊文字だけを使用してください。
 - ハイフン (-)
 - 下線 (&lowbar;)
 - 感嘆符 (!)
 - アンパーサンド (&)
 - アットマーク (@)
 - 疑問符 (?)
 - アスタリスク (\*)
 - 正符号 (+)
 - ピリオド (.)
 - 右括弧と左括弧  

 **重要:** 反復した文字シーケンスや、辞書に出てくる単語やユーザー名などの事前定義されたシーケンスをトークンに含めないでください。
15. デバイス情報のページで、以下のデバイス情報をコピーして保存します。  
 - 組織 ID (`tubo8x` など)
 - デバイス・タイプ (`my_device_type` など)
 - デバイス ID (`my_first_device` など)
 - 認証方式 (`token` など)
 - 認証トークン (`PtBVriRqIg4uh)_-Kl` など)  
  **ヒント:** {{site.data.keyword.iot_short_notm}} へのデバイスの接続を構成するときに、組織 ID、認証トークン、デバイス・タイプ、デバイス ID が必要になります。  

これで、デバイスを登録できました。次に、デバイスから {{site.data.keyword.iot_short_notm}} に接続するための構成を行います。

## 手順 2: デバイスを {{site.data.keyword.iot_short_notm}} に接続する
{: #iotplatform_subtask2}

デバイスを {{site.data.keyword.iot_short_notm}} に登録したら、登録情報を使用してデバイスを接続し、デバイス・データの受信を開始できます。

{{site.data.keyword.iot_short_notm}} は、多くのデバイス・タイプをサポートします。デバイスを接続する基本プロセスには、ほとんどの場合、以下の手順が含まれています。
- MQTT メッセージングを使用するようにデバイスをセットアップし、組織 ID、認証トークン、デバイス・タイプ、デバイス ID を使用して認証します。  
- MQTT プロトコルを使用して、デバイス・メッセージを {{site.data.keyword.iot_short_notm}} 組織に送信します。

**ヒント:** 一般的なデバイスに対応した多数の接続レシピが用意されています。レシピのリストについては、
IBM.com の[デバイス接続のレシピ](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/)を参照してください。

デバイスを接続するときには、以下の情報が必要になります。
- URL: *org_id*.messaging.internetofthings.ibmcloud.com  
*org_id* は、{{site.data.keyword.iot_short_notm}} 組織の ID です。
- ポート:
 - 1883
 - 8883 (暗号化)
 - 443 (Web ソケット)
- デバイス ID: d:*org_id*:*device_type*:*device_id*  
デバイスは、このパラメーターの組み合わせで一意的に識別されます。
- ユーザー名: use-token-auth  
この値の場合は、トークンによる許可を使用しています。
- パスワード: *認証トークン*  
この値は、デバイスの登録時に自分で定義した固有のトークンか、デバイスに割り当てられたトークンです。
- イベント・トピック形式: iot-2/evt/*event_id*/fmt/*format_string*  
*event_id* では、{{site.data.keyword.iot_short_notm}} に表示されるイベント名を指定します。*format_string* は、イベントの形式 (JSON など) です。
- メッセージ形式: JSON
  
 {{site.data.keyword.iot_short_notm}} は、いくつかの形式 (JSON やテキストなど) をサポートします。

デバイスを接続するための詳細については、技術資料にある[デバイスの MQTT 接続](devices/mqtt.html)を参照してください。
API 資料の[接続](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Connectivity/post_device_types_deviceType_devices_deviceId_events_eventName)のセクションにも、必要な情報が記載されています。

## デバイス接続のレシピ

Watson IoT Platform にデバイスを登録して接続するための詳しい流れについては、以下のレシピをご覧ください。

- [How to Register Devices in IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/how-to-register-devices-in-ibm-iot-foundation/)

- [Connecting Raspberry Pi as a Device to Watson IoT using Node-RED](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/)

- [Connect an Arduino Uno device to the IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/connect-an-arduino-uno-device-to-the-ibm-internet-of-things-foundation/)

- [Connecting a Sense HAT to Watson IoT using Node-RED](https://developer.ibm.com/recipes/tutorials/connecting-a-sense-hat-to-watson-iot-using-node-red/)

- [Connecting Raspberry Pi with Windows IoT Core as a Device to Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-with-windows-iot-core-as-a-device-to-watson-iot-using-node-red/)
