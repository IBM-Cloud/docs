---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# デバイス開発者用の Java
{: #java}

Java™ を使用して、{{site.data.keyword.iot_full}} の組織と対話するデバイスを作成し、カスタマイズできます。デバイス開発を簡単に始められるように、{{site.data.keyword.iot_short_notm}} に対応した Java クライアント・ライブラリー、資料、サンプルが用意されています。
{:shortdesc}

## Java クライアントとリソースのダウンロード
{: #java_client_download}

{{site.data.keyword.iot_short_notm}} 用の Java クライアント・ライブラリーとサンプルを利用するには、GitHub の [iot-java ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-watson-iot/iot-java){: new_window} リポジトリーにアクセスし、インストール手順を実行します。

## コンストラクター
{: #constructor}

コンストラクターは、クライアント・インスタンスを作成し、以下の定義を格納する `Properties` オブジェクトを受け入れます。

|定義 |説明 |
|:----|:----|
|`org` |組織 ID に設定する必要がある必須の値。Quickstart フローを使用する場合は、`quickstart` を指定します。|
|`type`  |デバイスのタイプを指定する必須の値。|
|`id`  |デバイスの固有の ID を指定する必須の値。|
|`auth-method`  |使用する認証の方式。サポートされている唯一の方式は `token` です。|
|`auth-token`   |デバイスを {{site.data.keyword.iot_short_notm}} に安全に接続するための認証トークン。|
|`clean-session`|true または false の値。永続サブスクリプション・モードでアプリケーションを接続する場合のみ必要です。デフォルトでは、`clean-session` は true に設定されます。|
|`Port`|接続先のポート番号。8883 か 443 のいずれかを指定してください。ポート番号を指定しない場合、クライアントは、デフォルトのポート番号 8883 で {{site.data.keyword.iot_short_notm}} に接続します。|
|`MaxInflightMessages`  |接続の処理中メッセージの最大数を設定します。デフォルト値は 100 です。|
|`Automatic-Reconnect`  |true か false の値。切断状態になったデバイスを自動的に {{site.data.keyword.iot_short_notm}} に再接続する場合は、これを指定する必要があります。デフォルト値は false です。|
|`Disconnected-Buffer-Size`|クライアントの切断中にメモリー内に保管できるメッセージの最大数。デフォルト値は 5000 です。|
|`WebSocket`|true または false の値。{{site.data.keyword.iot_short_notm}} との Web ソケット接続を使用する場合に必要です。デフォルト値は false です。|

**注:** 永続サブスクリプション・モードでデバイスを接続するには、`clean-session` を `false` に設定します。クリーン・セッションについて詳しくは、[MQTT 資料](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)の『サブスクリプション・バッファーとクリーン・セッション』のセクションを参照してください。

`Properties` オブジェクトによって、{{site.data.keyword.iot_short_notm}} モジュールとの対話に使用する定義が作成されます。

デバイスが Quickstart モードでイベントをパブリッシュするコード・サンプルを以下に示します。

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

`Properties` オブジェクトを直接使用する代わりに、プロパティーの名前と値のペアを含む構成ファイルを使用できます。`Properties` オブジェクトを含む構成ファイルを使用する場合は、以下のコード形式を使用してください。

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


{{site.data.keyword.iot_short_notm}} に接続するには、`connect()` 関数を使用します。`connect()` 関数には、`autoRetry` というオプションのブール値パラメーターが含まれています。このパラメーターで、MqttException 接続障害が発生した場合にライブラリーが再接続を試行するかどうかを指定できます。デフォルトでは、`autoRetry` は true に設定されます。渡されたデバイス登録の詳細に誤りがあったために MqttSecurityException 接続の障害が発生した場合は、`autoRetry` が true に設定されていても、ライブラリーは再接続を試行しません。

`connect()` 関数を呼び出す前に、`setKeepAliveInterval(int)` メソッドを使用して MQTT のキープアライブ間隔を設定することもできます。`setKeepAliveInterval(int)` の値は、秒単位で指定します。このメソッドで、送受信されるメッセージとメッセージの間隔の最大時間を定義できます。このメソッドを使用すると、クライアントは、TCP/IP タイムアウト期間の終了を待たずに、サーバーが使用不能になったことを検出できます。クライアントは、それぞれのキープアライブ間隔の期間中に少なくとも 1 つのメッセージがネットワークを通過するかどうかを確認します。タイムアウト期間中に受け取るデータ関連メッセージがゼロであれば、クライアントは、小さな `ping` メッセージを送信してサーバーに応答してもらいます。`setKeepAliveInterval(int)` は、デフォルトで 60 秒に設定されます。クライアントでキープアライブ処理機能を無効にする場合は、`setKeepAliveInterval(int)` の値を 0 に設定します。


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(true);
```

接続障害が発生した場合の再試行の数を制御するために、多重定義の connect(int numberOfTimesToRetry) 関数を使用します。


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(10);
```

デバイスは、{{site.data.keyword.iot_short_notm}} に正常に接続してから、イベントをパブリッシュしたり、アプリケーションからのデバイス・コマンドにサブスクライブしたりできます。


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

パブリッシュされるイベントの [QoS レベル](../../reference/mqtt/index.html#qos-levels)を引き上げることができます。QoS レベルがゼロより大きいイベントは、追加の確認受信情報があるので、パブリッシュにかかる時間が延びる可能性があります。

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### カスタム形式のイベントのパブリッシュ

さまざまな形式でイベントをパブリッシュできます。例えば、JSON、ストリング、バイナリーなどの形式が可能です。デフォルトでは、ライブラリーは、JSON 形式でイベントをパブリッシュしますが、別の形式のデータを指定することもできます。例えば、ストリング形式のデータをパブリッシュする場合は、以下のコード・スニペットを使用します。

```
myClient.connect();

String data = "cpu:"+getProcessCpuLoad();
status = myClient.publishEvent("load", data, "text", 2);
```

**注:** 前のコード例では、イベントのペイロードをストリング形式にする必要があります。

XML データは、ストリング形式に変換して以下のようにパブリッシュできます。

```
status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

同じように、バイナリー形式のイベントをパブリッシュする場合は、バイト配列を使用します。その概要を以下の例に示します。

```
myClient.connect();

byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### HTTP によるイベントのパブリッシュ
{: #publishing_events_http}


MQTT のほかにも、HTTP を使用してイベントを {{site.data.keyword.iot_short_notm}} にパブリッシュするようにデバイスを構成することもできます。HTTP を介してイベントをパブリッシュする手順の概要を以下に示します。

1. プロパティー・ファイルを使用して `DeviceClient` インスタンスを作成する。
2. パブリッシュする必要があるイベントを作成する。
3. イベント名を指定し、`publishEventOverHTTP()` メソッドを使用してイベントをパブリッシュする。以下にコード・サンプルを示します。

``` 
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

boolean response  = myClient.api().publishDeviceEventOverHTTP("blink", event, ContentType.json);
```

コード全体を見たい場合は、[HttpDeviceEventPublish ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")] というデバイスのサンプルを参照してください。{: new_window}

`publishEventOverHTTP()` メソッドは、プロパティー・ファイルの設定に基づいて、Quickstart モードまたは登録済みフロー・モードでイベントをパブリッシュします。プロパティー・ファイルで組織 ID を `quickstart` に設定すると、`publishEventOverHTTP()` メソッドは、デバイス用サンプル Quickstart サービスにプレーン HTTP 形式でイベントをパブリッシュします。登録されている有効な組織をプロパティー・ファイルで指定した場合は、イベントが HTTPS で安全にパブリッシュされます。

HTTP プロトコルによる配信は「最高 1 回」の送信です。これは、MQTT プロトコルのサービス品質レベル「最高 1 回」(QoS 0) に似ています。「最高 1 回」の送信を使用してイベントをパブリッシュする場合、アプリケーションはエラー発生時の再試行ロジックを実装する必要があります。

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## コマンドの処理
{: #handling_commands}

デバイス・クライアントは、接続時に、このデバイスに対するコマンドに自動的にサブスクライブします。特定のコマンドを処理するには、コマンド・コールバック・メソッドを登録する必要があります。
メッセージは、以下のプロパティーがある `Command` クラスのインスタンスとして返されます。

| プロパティー     |データ・タイプ     | 説明|
|----------------|----------------|
|`payload` |java.lang.String| メッセージ・ペイロードのデータ。|
|`format`  |java.lang.String| 形式は任意のストリング (JSON など) となります。|
|`command`   |java.lang.String|コマンドを識別します。|
|`timestamp`   |org.joda.time.DateTime|イベントの日時。|


```
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

{{site.data.keyword.iot_short_notm}} Java クライアント・ライブラリーを使用して開発されたデバイス・サンプルとデバイス管理サンプルのリストについては、[iot-device-samples GitHub リポジトリー ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-messaging/iot-device-samples/tree/master/java){: new_window} を参照してください。
