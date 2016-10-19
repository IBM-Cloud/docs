---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# デバイス開発者用の Java
{: #java}

最終更新日: 2016 年 8 月 2 日
{: .last-updated}


Java を使用して、{{site.data.keyword.iot_full}} 上で組織と対話するデバイスを構築してカスタマイズできます。Java を使用してデバイスの開発を始める場合は、提供されている情報と例を活用してください。
{:shortdesc}

## Java クライアントとリソースのダウンロード
{: #java_client_download}

{{site.data.keyword.iot_short_notm}} 用の Java クライアント・ライブラリーとサンプルを利用するには、GitHub の [iot-java](https://github.com/ibm-watson-iot/iot-java) リポジトリーにアクセスし、インストール手順を実行します。


## コンストラクター
{: #constructor}

コンストラクターはクライアント・インスタンスを作成し、以下の定義を格納するプロパティー・オブジェクトを受け入れます。

|定義 |説明 |
|:---|:---|
|`org` |組織 ID。このフィールドは必須です。Quickstart フローを使用する場合は、`quickstart` を指定します。|
|`type`  |デバイスのタイプ。このフィールドは必須です。|
|`id`  |デバイスの ID。このフィールドは必須です。|
|`auth-method`   |使用する認証の方式。現在サポートされている値は、`token` のみです。|
|`auth-token`   |デバイスを Watson IoT Platform に安全に接続するための認証トークン。|
|`clean-session`|true または false 値。永続サブスクリプション・モードでアプリケーションを接続する場合のみ必要です。デフォルトでは、`clean-session` は `true` に設定されます。|

**注:** 永続サブスクリプション・モードでデバイスを接続するには、`clean-session` を `false` に設定します。クリーン・セッションについて詳しくは、[MQTT 資料](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)の『サブスクリプション・バッファーとクリーン・セッション』のセクションを参照してください。

properties オブジェクトによって、{{site.data.keyword.iot_short_notm}} モジュールとの対話に使用する定義が作成されます。

以下のコードは、Quickstart モードでイベントをパブリッシュするデバイスを示しています。

```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class QuickstartDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data using Properties class
        Properties options = new Properties();
        options.setProperty("org", "quickstart");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Quickstart flow allows only QoS = 0
        myClient.publishEvent("status", event, 0);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

以下のコード・サンプルは、どのようにすればデバイスが登録済みフローでイベントをパブリッシュできるかを示しています。


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

### 構成ファイルの使用

プロパティー・オブジェクトを直接使用する代わりに、プロパティーの名前と値のペアを含む構成ファイルを使用できます。プロパティー・オブジェクトを含む構成ファイルを使用する場合は、以下のコード形式を使用してください。

```
package com.ibm.iotf.sample.client.device;

import java.io.File;
import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublishPropertiesFile {

    public static void main(String[] args) {
        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = DeviceClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event, 1);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

構成ファイルの内容は、次の形式でなければなりません。

```
    [device]
    org=$orgId
    typ=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```

## {{site.data.keyword.iot_short_notm}} への接続
{: #connecting_to_iotp}

connect 関数を呼び出すことによって {{site.data.keyword.iot_short_notm}} に接続します。connect 関数はオプションのブール値パラメーター `autoRetry` (デフォルトでは `true`) を受け取ります。 `autoRetry` パラメーターは、MqttException エラーが発生したときにライブラリーが再接続できるようにします。使用されたデバイス登録の詳細が誤っていることが原因で MqttSecurityException エラーが発生した場合は、`autoRetry` パラメーターが `true` に設定されていても、ライブラリーは再接続を試みませんのでご注意ください。

```
DeviceClient myClient = new DeviceClient(options);

myClient.connect(true);
```

{{site.data.keyword.iot_short_notm}} サービスへの接続に成功すると、デバイス・クライアントはイベントのパブリッシュやデバイス・コマンドのサブスクライブなどの操作をアプリケーションから実行できるようになります。


## イベントのパブリッシュ
{: #publishing_events}

イベントとは、デバイスが {{site.data.keyword.iot_short_notm}} にデータをパブリッシュするためのメカニズムのことです。デバイスはイベントの内容を制御し、送信するイベントごとに名前を割り当てます。

{{site.data.keyword.iot_short_notm}} インスタンスがイベントを受信すると、その受信イベントの資格情報によって、送信元デバイスが識別されます。そのためデバイスが、別のデバイスになりすますことはできません。

イベントは、MQTT プロトコルによって定義された 3 つの[サービス品質 (QoS) レベル](../../reference/mqtt/index.html#qos-levels)のいずれでもパブリッシュできます。デフォルトでは、イベントは QoS=0 でパブリッシュされます。

### デフォルトの QoS レベルでイベントをパブリッシュする

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### イベントの QoS レベルの引き上げ

パブリッシュされるイベントの [QoS レベル](../../reference/mqtt/index.html#qos-levels)を引き上げることができます。QoS レベルがゼロより大きいイベントは、追加の確認受信情報が含まれているため、パブリッシュにかかる時間が延びる可能性があります。

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### HTTP を使用したイベントのパブリッシュ

MQTT のほかに、デバイスは HTTP を使用して {{site.data.keyword.iot_short_notm}} にイベントをパブリッシュすることもできます。その場合のステップは以下のとおりです。

* プロパティー・ファイルを使用して DeviceClient インスタンスを作成する。
* パブリッシュする必要があるイベントを作成する。
* イベント名を指定し、`publishEventOverHTTP()` メソッドを使用してイベントをパブリッシュする。以下にコードを示します。

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

int httpCode = myClient.publishEventOverHTTP("blink", event);
```

[HttpDeviceEventPublish] デバイス例にコード全体があります。

`publishEventOverHTTP()` メソッドは、プロパティー・ファイルの設定に基づいて、Quickstart モードまたは登録済みフロー・モードでイベントをパブリッシュします。プロパティー・ファイル内の組織 ID が `quickstart` の場合、`publishEventOverHTTP()` メソッドは、デバイス用サンプル Quickstart サービスにプレーン HTTP 形式でイベントをパブリッシュします。有効な登録済み組織がプロパティー・ファイルで使用されている場合、このメソッドは常に HTTPS (HTTP over SSL) でイベントをパブリッシュするので、すべての通信が保護されます。

HTTP プロトコルによる配信は「最高 1 回」の送信です。これは、MQTT プロトコルのサービス品質レベル「最高 1 回」(QoS 0) に似ています。「最高 1 回」の送信を使用してイベントをパブリッシュする場合、アプリケーションはエラー発生時の再試行ロジックを実装する必要があります。

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## コマンドの処理
{: #handling_commands}

デバイス・クライアントは、接続時に、このデバイスに対するコマンドに自動的にサブスクライブします。特定のコマンドを処理するには、コマンド・コールバック・メソッドを登録する必要があります。
メッセージは、以下のプロパティーを持つ Command クラスのインスタンスとして返されます。

| プロパティー     |データ・タイプ     | 説明|
|----------------|----------------|
|`payload` |java.lang.String| メッセージ・ペイロードのデータ。|
|`format`  |java.lang.String| 形式は任意のストリング (JSON など) となります。|
|`command`   |java.lang.String|コマンドを識別します。|
|`timestamp`   |org.joda.time.DateTime|イベントの日時。|


``` sourceCode
package com.ibm.iotf.sample.client.device;

import java.util.Properties;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;


import com.ibm.iotf.client.device.Command;
import com.ibm.iotf.client.device.CommandCallback;
import com.ibm.iotf.client.device.DeviceClient;


//Implement the CommandCallback class to provide the way in which you want the command to be handled
class MyNewCommandCallback implements CommandCallback, Runnable {

    // A queue to hold & process the commands for smooth handling of MQTT messages
    private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

    /**
    * This method is invoked by the library whenever there is command matching the subscription criteria
    */
    @Override
    public void processCommand(Command cmd) {
        try {
            queue.put(cmd);
            } catch (InterruptedException e) {
        }
    }

    @Override
    public void run() {
        while(true) {
            Command cmd = null;
            try {
                //In this sample, we just display the command
                cmd = queue.take();
                System.out.println("COMMAND RECEIVED = '" + cmd.getCommand() + "'\twith Payload = '" + cmd.getPayload() + "'");
            } catch (InterruptedException e) {}
        }
    }
}

public class RegisteredDeviceCommandSubscribe {


    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Pass the above implemented CommandCallback as an argument to this device client
        myClient.setCommandCallback(new MyNewCommandCallback());

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();
    }
}
```

## サンプル
{: #samples}

{{site.data.keyword.iot_short_notm}} Java クライアント・ライブラリーを使用して開発されたデバイスとデバイス管理のサンプルのリストについては、[GitHub リポジトリー](https://github.com/ibm-messaging/iot-device-samples/tree/master/java)を参照してください。
