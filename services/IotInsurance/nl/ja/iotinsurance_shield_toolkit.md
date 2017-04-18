---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-27"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# シールド・ツールキットの使用
{: #iot4i_shield_toolkit}
シールドは、危険を識別して適切な自動応答を作成することで、資産とユーザーを保護するために使用します。{{site.data.keyword.iotinsurance_short}} シールド・ライブラリーに含まれるシールドを使用または変更するか、あるいは以下の手順と例を利用して独自のシールドを作成して実装することができます。
{:shortdesc}

## シールドについて。
シールドとは、センサーから受け取る入力での特定の条件によって起動できる、一連のルールと定義済みアクションです。例えば、センサーが水漏れを検出するとテキスト・メッセージを送信するルールを設定して、シールドを作成することができます。

## {{site.data.keyword.iotinsurance_short}} シールド・ライブラリーにあるシールドの使用

[{{site.data.keyword.iotinsurance_short}} シールド・ライブラリー ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window} には、幅広い種類の定義済みシールドが用意されています。それらのシールドをダウンロードして使用を開始するための手順については、そのサイト上の README ファイルを参照してください。

## 独自のシールドの作成
この例では、環境をセットアップし、シールドを定義し、ユーザーを作成し、シールドをユーザーに関連付ける方法を示します。また、オプションとして、プロモーションとシミュレート・ハザードを作成することもできます。
  

以下のセクションでは、水漏れに関する簡単なシールドを作成するコード・サンプルが示されています。サンプル・コード・セット全体を確認する場合は、[iot4i-api-examples-nodejs GitHub リポジトリー](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/)を参照してください。

### 前提条件
始める前に、以下の前提条件が満たされていることを確認してください。

- [Node.js](https://nodejs.org/en/) がコンピューターにインストールされている。  
- Node.js に対応するランタイム環境 (Eclipse など)。
- Git ソフトウェアおよび [API サンプルの GitHub ソース・コード・リポジトリー](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)へのアクセス。あるいは、[ソース・コード・ファイルを含むアーカイブ](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip)をダウンロードすることもできます。
- 準備しておいたソース・コード。
  
ソース・コードを準備するには、以下のステップを実行します。
  1. [GitHub ソース・コードのリポジトリー](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)をコンピューターに複製またはダウンロードします。
  2. コマンド・ラインを使用して、複製されたソース・コード・ファイルが含まれるフォルダーに移動し、`npm install` コマンドを実行して、プロジェクトのオープン・ソース前提条件をインストールします。

### 環境の設定
{: #environment}
REST API 呼び出しを送信するように環境を構成するには、API の URL を config.js ファイルの中に構成する必要があります。このコンテキストにおいて、統合サービスの URL は無視できます。

```
var config = module.exports = {
  api: "https//iot4insurance-api-<uniqueid>.mybluemix.net",
  aggregator: "https//iot4i-aggregator-<uniqueid>.mybluemix.net",
  credentials : {
    user: "Admin",
    pass: "<password from IoT4I service credentials>"
  }
};
```

### シールド定義の作成
{: #create_shield_def}

メソッド: POST  
API: /shield  
https://iot4i-docs-api.mybluemix.net/dist/#!/shield/addShield

createShield.js ファイルの中にシールド定義を作成します。水漏れを検出する簡単なシールドを、以下の例に示します。

```
var shield = {
  "UUID": "26",
  "name": "demoShield",
  "type": "Environmental Measurements",
  "description": "Detect water leaks",
  "image": "shieldWater",
  "canBeDisabled": false,
  "hazardDetectionOnCloud": true,
  "jsCodeMethod": "demoShield",
  "actions": [
     "pushios"
  ],
  "potentialClaimAmount": "10",
  "shieldParameters": []
};

```

各部の意味は、次のとおりです。
- **UUID** - シールドの汎用固有 ID (UUID)。
- **actions** - あるハザードが作成されたときに起動するアクションのリスト。この例の場合、iOS プッシュ通知を使用することにより、ハザードに関する情報がユーザーのアプリに送信されます。

### シールド・コードの作成
{: #create_shield_code}
シールド・エンジンでペイロードを処理する方法を定義するシールド・コードを、shieldCode.js ファイル内に作成します。

前の例で示されていたシールドにおいて、水漏れペイロードを処理するために使用できるシールド・コードを、以下のサンプルに示します。

```
var shieldCode = {
  "name": "demoshield",
  "shieldUUID": "26",
  "type": "shield",
  "code": code.toString()
};

```

各シールド・コードには、resource/shield.js ステートメントで定義されているリソースが含まれています。以下の各リソースには、前の例で示されていたシールド、ペイロード、ユーザーで使用できる例が含まれています。

  - シールド名  
  ```
  var DEMO_SHIELD_NAME = "demoshield";
  ```

  - シールド遅延 - ハザード相互間の遅延 (ミリ秒単位)。  
  ```
  var DEMO_SHIELD_DELAY = 5000;
  ```

  - シールド汎用固有 ID (UUID)  
  ```
  var DEMO_SHIELD_UUID = 26;
  ```

  - 入り口条件 - シールド・エンジンがペイロードを処理するために必要な条件と属性。この例の場合、ペイロードに属性 **liquid_detected** が含まれていなければならないというのが条件です。  
  ```
  var demoEntryCondition = function(payload) {
    return (payload.liquid_detected)
  };
  ```

  - Safelet - シールドのうち、ハザードが存在するかどうかを判別するアルゴリズムを計算し、実行するコア部分。以下の例の場合、必要な属性は **liquid_detected** だけですが、Safelet を使用することにより複雑なアルゴリズムを定義することもできます。  
  ```
  var demoSafelet = function(payload) {
    return (payload.liquid_detected);
  };
  ```

  - メッセージ - ハザードが処理される場合に、ユーザーに送信されるメッセージ。
  ```
  var demoMessage = function(payload) {
    return (constructMessage(payload, DEMO_SHIELD_UUID, 'demoHazard', 'a demo shield activated!'));
  };
  ```

  - シールドの実行 - シールド・エンジンが関連するすべてのシールドを自動的に実行するのを待機するのではなく、シールドを直接実行するために使用される関数。  
  ```
  var demoShield = function(payload) {
    var shield = getShieldByName(DEMO_SHIELD_NAME);
    return (commonShield (payload, shield));
  };
  ```

  - 登録シールド - シールドをシールド・エンジンに登録するため、シールド・コードの中で呼び出す必要のある事前定義済み機能。この例の **undefined** 値は前処理関数を表すものですが、この特定の例では不要です。シールドによっては、前処理関数を使用することによって、ペイロード中のデータを再構成することができます。例えば、温度読み取り値が華氏の値として報告されている一方、Safelet では摂氏が必要な場合には、前処理関数を使用することにより、温度データを必要な値に変換することができます。  
  ```
  registerShield(DEMO_SHIELD_UUID, DEMO_SHIELD_NAME, demoEntryCondition, undefined, demoSafelet, demoMessage, DEMO_SHIELD_DELAY);
  ```

### ユーザーの作成
{: #create_user}

メソッド: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/user/addUser

createUser.js ファイルの中でユーザーを作成します。単一のユーザーを作成する方法を、以下の例に示します。

```
var user = {
  "username": "user1",
  "fullname": "John Doe",
  "firstname": "John",
  "lastname": "Doe",
  "password": "user1234",
  "accessLevel": "100",
  "address": "42 Wallaby Way, Sydney",
  "email": "user@example.com",
  "deviceID": "user1",
  "deviceType": "wink",
  "type": "wink"
};

```

各部の意味は、次のとおりです。
- **username** - デバイス、シールド、プロモーションなど、ユーザーに関連するあらゆるエンティティーを特定するために使用される、ユーザーの固有キー。
- **password** - データベースには、パスワードのハッシュ値のみ格納されます。
- **DeviceId** - ユーザーを {{site.data.keyword.iot_full}} に登録するために使用される ID。その値はユーザー名と同じです。
- **accessLevel** - この値により、ユーザーがアクセスできる API エンドポイントが定義されます。
  - 100 - モバイル・アプリ
  - 10 - ダッシュボード
  - 1 - システム管理者

### シールド関連付けの作成
{: #create_shield_assoc}

メソッド: POST  
API: /user  
https://iot4i-docs-api.mybluemix.net/dist/#!/shieldassociation/addShieldAssociation

createUserShieldAssociation.js の中でシールドをユーザーにリンクするシールド関連付けを作成します。

以下の例では、前のセクションで作成されたシールドとユーザーのシールド関連付けが示されています。

```
var userShield = {
  "shieldUUID": "26",
  "username": "user1",
  "hazardDetectionOnCloud": true
};

```



### ハザード・シミュレーションの作成
{: #create_sim_hazard}

メソッド: POST  
API: /sendPayloadToMQTT  
https://iot4i-docs-api.mybluemix.net/dist/#!/global/sendPayloadToMQTT

シールドをテストするためのハザード・シミュレーション・ペイロードを作成することができます。

前の例で作成されたシールドをアクティブにし、関連するユーザーにアラートを送信するペイロードを作成する方法を、以下の例に示します。

```
var parameters {
  "payload": {
    "sensor_pod_id": "190107",
    "name": "Sensor",
    "manufacturer_device_model": "leakSMART",
    "device_manufacturer": "leaksmart",
    "model_name": "leakSMART Sensor",
    "upc_code": "waxman_sensor",
    "hub_id": "379652",
    "lat_lng": [null, null],
    "location": "",
    "status": "online",
    "liquid_detected": true,
    "usr": "user1",
    "activation": "2016-06-20T12:05:02.776Z"
  },
  "outputtype": "evt",
  "devicetype": "wink",
  "deviceid": "wink",
  "type": "wink"
};

```


### プロモーションの作成
{: #create_promotion}

{{site.data.keyword.iotinsurance_short}} は、モバイル・アプリを使用することにより、住宅所有者に対してプロモーションを送信することができます。プロモーションは、createPromotion.js ファイルを使用して作成します。

許可された配管工 (plumber) のためのプロモーションを作成する方法を、以下の例に示します。

```
var promotion = {
  "title": "Promotion 9",
  "description": "Contact one of our authorized plumbers to install your water leak detection solution.",
  "buttonTitle": "Call Now",
  "type": "1",
  "phone": "+015555555555",
  "username": "user1",  
};

```

オプションとして、モバイル・アプリをデプロイし、[ioti-mobile GitHub リポジトリーにある手順](https://github.com/ibm-watson-iot/ioti-mobile)を使用することにより、前のセクションで作成したユーザーとして接続することができます。
