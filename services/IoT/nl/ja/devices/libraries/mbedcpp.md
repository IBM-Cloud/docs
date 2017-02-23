---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# デバイス開発者用の mBed C++
{: #mbedcpp}

[mBed C++ クライアント・ライブラリー](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/)を使用すると、[mBed デバイス](https://www.mbed.com/en/) ([LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/) や [FRDM-K64F](https://developer.mbed.org/platforms/FRDM-K64F/) など) を {{site.data.keyword.iot_full}} サービスに簡単に接続できます。
{:shortdesc}

詳しくは、[developer.mbed.org](https://developer.mbed.org/) の [ibmiotf](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/) を参照してください。

このライブラリーでは C++ を使用していますが、動的メモリー割り振りと STL 関数の使用は避けています。その理由は、mBed デバイスには特殊なメモリー・モデルが存在することがあり、移植が難しくなるためです。いずれにしても、このライブラリーを利用するなら、メモリーの使用について最大限に予測可能となります。

## 従属関係
{: #dependencies}

|従属関係 |説明|
|:---|:---|
|[Eclipse Paho MQTT ライブラリー](https://developer.mbed.org/teams/mqtt/code/MQTT/)|mBed デバイス向けの MQTT クライアント・ライブラリーを提供します。詳しくは、[Embedded MQTT C/C++ client libraries](http://www.eclipse.org/paho/clients/c/embedded/) を参照してください。|
|[EthernetInterface ライブラリー](https://developer.mbed.org/users/mbed_official/code/EthernetInterface/)|イーサネット経由の mBed IP ライブラリー。|

## ライブラリーの使用方法
{: #library_use}

mBed C++ IBMIoTF クライアント・ライブラリーを使用する場合は、[mBed コンパイラー](https://developer.mbed.org/compiler/)を使用してアプリケーションを作成します。mBed コンパイラーは、mBed マイクロコントローラー上で実行されるプログラムを作成、コンパイル、ダウンロードするために構成された、軽量のオンライン C/C++ IDE を提供します。

**注:** mBed と共に実行するためにインストールまたはセットアップしなければならないものはありません。

ARM mBed NXP LPC 1768 マイクロコントローラーを {{site.data.keyword.iot_short_notm}} に接続する方法については、[mBed C++ client library for IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/mbed-c-client-library-for-ibm-iot-foundation/) レシピを参照してください。

## コンストラクター
{: #constructor}

コンストラクターはクライアント・インスタンスを作成し、次のパラメーターを受け入れます。

|パラメーター |説明 |
|:---|:---|
|`org` |組織 ID。この値は必須です。Quickstart フローを使用する場合は、`quickstart` を指定します。|
|`type`   |デバイスのタイプ。このフィールドは必須です。|
|`id`   |デバイスの ID。このフィールドは必須です。|
|`auth-method`   |認証の方式。登録されたフローの場合にのみ必要な、オプション・フィールドです。現在サポートされている値は、`token` のみです。|
|`auth-token`   |デバイスを Watson IoT Platform に安全に接続するための認証トークン。登録されたフローの場合にのみ必要な、オプション・フィールドです。|

これらのパラメーターによって、{{site.data.keyword.iot_short_notm}} サービスとの対話に使用する定義が作成されます。

次のコード・サンプルでは、DeviceClient インスタンスが {{site.data.keyword.iot_short_notm}} Quickstart サービスとどのように対話できるかを示します。

```
  #include "DeviceClient.h"
  ....
  ....

  // Set {{site.data.keyword.iot_short_notm}} connection parameters
  char organization[11] = "quickstart";     // For a registered connection, replace with your org
  char deviceType[8] = "LPC1768";           // For a registered connection, replace with your device type
  char deviceId[3] = "01";                  // For a registered connection, replace with your device id

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId);

  // Get the DeviceID(MAC Address) if we are in quickstart mode and device ID is not specified
  if((strcmp(organization, QUICKSTART) == 0) && (strcmp("", deviceId) == 0))
  {
  	char tmpBuf[50];
  	client.getDeviceId(tmpBuf, sizeof(tmpBuf));
  }
  ....
```

上記のコード・サンプルに示されているように、デバイス ID が指定されていない場合、DeviceClient はデバイスの MAC アドレスをデバイス ID として使用して、{{site.data.keyword.iot_short_notm}} に接続します。デバイス・コードで `getDeviceId()` メソッドを使用して、デバイス ID を DeviceClient インスタンスから取得できます。

次のコード・ブロックでは、DeviceClient インスタンスを作成して、{{site.data.keyword.iot_short_notm}} 登録済み組織と対話する方法を示します。

```
  #include "DeviceClient.h"
  ....
  ....

  // Set {{site.data.keyword.iot_short_notm}} connection parameters
  char organization[11] = "hrcl78";
  char deviceType[8] = "LPC1768";
  char deviceId[3] = "LPC176801";
  char method[6] = "token";
  char token[9] = "password";

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);
  ....
```

## {{site.data.keyword.iot_short_notm}} への接続
{: #connecting_to_iotp}

デバイスは、DeviceClient インスタンスで connect 関数を呼び出すことによって、{{site.data.keyword.iot_short_notm}} と接続できます。

```
  #include "DeviceClient.h"
  ....
  ....

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);

  bool status = client.connect();

```
接続が成功したら、デバイスはイベントを {{site.data.keyword.iot_short_notm}} にパブリッシュし、コマンドを listen することができます。

また、次の例に示すとおり、デバイスは `isConnected()` メソッドを使用して接続の状況を照会することもできます。

```
  #include "DeviceClient.h"
  ....
  ....

  client.isConnected();

```


## イベントのパブリッシュ
{: #publishing_events}

イベントとは、デバイスが {{site.data.keyword.iot_short_notm}} にデータをパブリッシュするためのメカニズムのことです。デバイスはイベントの内容を制御し、送信するイベントごとに名前を割り当てます。

{{site.data.keyword.iot_short_notm}} インスタンスがイベントを受信すると、その受信イベントの資格情報によって、送信元デバイスが識別されます。そのためデバイスが、別のデバイスになりすますことはできません。

イベントは、MQTT プロトコルによって定義された 3 つの[サービス品質 (QoS) レベル](../../reference/mqtt/index.html#qos-levels)のいずれでもパブリッシュできます。デフォルトでは、イベントは QoS 0 でパブリッシュされます。

### デフォルトのサービス品質を使用したイベントのパブリッシュ

以下のサンプルでは、次のデータ・ポイントを JSON 形式で {{site.data.keyword.iot_short_notm}} にパブリッシュする方法を示します。

- LPC1768 (x、y、z 軸など)
- ジョイスティックの位置
- 現在温度の読み取り

```
	boolean status = client.connect();

	// Create buffer to hold the event
	char buf[250];

	// Construct an event message with desired datapoints in JSON format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf);
	....
```
全体を示すサンプルについては、[IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp) を参照してください。

### イベントの QoS レベルの引き上げ

パブリッシュされるイベントの [QoS レベル](../../reference/mqtt/index.html#qos-levels)を引き上げることができます。QoS レベルが `0` より大きいイベントは、追加の確認受信情報が含まれているため、パブリッシュにかかる時間が延びる可能性があります。

**注:** Quickstart フロー・モードは、QoS 0 のみをサポートしています。

```
	#include "MQTTClient.h"

	boolean status = client.connect();

	// Create buffer to hold the event
	char buf[250];

	// Construct an event message with desired datapoints in JSON format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf, MQTT::QOS2);
	....
```

### イベントのパブリッシュ中に接続が失われた場合の対応


`publishEvent()` メソッドから false 値が返された場合は、接続の状況を確認し、接続が失われていれば `reConnect()` を呼び出します。

```
	#include "MQTTClient.h"

	status = client.publishEvent("blink", buf, MQTT::QOS2);

	if(status == false) {
	    // Check if connection is lost and retry
	    while(!client.isConnected())
	    {
	        client.reConnect();
	        wait(5.0);
	    }
	}
	....
```
接続していない状態でパブリッシュしたイベントはライブラリーによって格納されないため、接続が再確立された後に、デバイスから再び `publishEvent()` メソッドを呼び出してそれらのイベントを送信する必要があります。


## コマンドの処理
{: #handling_commands}

デバイス・クライアントは、接続時に、このデバイスに対するコマンドに自動的にサブスクライブします。特定のコマンドを処理するには、コマンド・コールバック・メソッドを登録する必要があります。
メッセージは、以下のプロパティーを持つ Command クラスのインスタンスとして返されます。

|プロパティー |説明|
|:---|:---|
|`command` | 呼び出されたコマンドの名前。|  
|`format`  |イベントの形式。形式は任意のストリング (JSON など) となります。 |
|`payload`  |コマンド・ペイロードのデータ。最大長は 131072 バイトです。 |


次のコードで定義されたサンプル・コマンド・コールバック関数では、アプリケーションからの LED 点滅間隔コマンドを処理し、DeviceClient インスタンスに関数ハンドルを設定することで、デバイスが点滅コマンドを受信するたびにコールバック・メソッドが実行されるようにします。

```
    #include "DeviceClient.h"
    #include "Command.h"

    // Process the command and set the LED blink interval
    void processCommand(IoTF::Command &cmd)
    {
        if (strcmp(cmd.getCommand(), "blink") == 0)
    	{
    	    char *payload = cmd.getPayload();
    	    char* pos = strchr(payload, '}');
    	    if (pos != NULL) {
    	        *pos = '\0';
    	        char* ratepos = strstr(payload, "rate");
    	        if(ratepos == NULL)
    	            return;
    	        if ((pos = strchr(ratepos, ':')) != NULL)
    	        {
    	            int blink_rate = atoi(pos + 1);
    	            blink_interval = (blink_rate <= 0) ? 0 : (blink_rate > 50 ? 1 : 50/blink_rate);
    	        }
    	    }
    	} else {
            WARN("Unsupported command: %s\n", cmd.getCommand());
        }
    }

    client.setCommandCallback(processCommand);

    client.yield(1000);  // allow the MQTT client to receive messages
    ....
```
全体を示すサンプルについては、[IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp) を参照してください。

**注:** コマンドを受け取るには `client.yield()` 関数を定期的に呼び出す必要があります。
`client.yield()` 関数は、Watson IoT Platform からのコマンドをデバイスで受信できるようにし、接続が保持されるようにします。keepAlive 間隔で指定された時間フレーム内で `client.yield()` 関数が呼び出されなかった場合は、プラットフォームから送信されるコマンドをデバイスが受信しなくなります。`client.yield()` 関数に割り当てられる値は、ソケットからデータを読み取ることができる時間の長さ (ミリ秒) を指定します。この時間を過ぎると制御はアプリケーションに戻ります。

## クライアントの切断
{: #disconnect_client}

クライアントを切断して接続を解放するには、次のコード・スニペットを実行します。

```
	...
	client.disconnect();
	....
```
## サンプル
{: #samples}

[IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/) は、{{site.data.keyword.iot_short_notm}} クライアント・ライブラリーを使用して mbed LPC1768 デバイスまたは FRDM-K64F デバイスをサービス・インスタンスに接続する方法を示すコード・サンプルです。
