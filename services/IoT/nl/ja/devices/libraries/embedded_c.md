---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-08-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# デバイス開発者のための Embedded C
{: #embedded_c}

Embedded C を使用して、{{site.data.keyword.iot_full}} 上で組織と対話するデバイスを構築してカスタマイズできます。Embedded C を使用してデバイスの開発を始める場合は、提供されている情報と例を活用してください。
{:shortdesc}

## Embedded C クライアントおよびリソースのダウンロード
{: #embeddedc_client_download}

{{site.data.keyword.iot_short_notm}} の Embedded C クライアント・ライブラリーおよびサンプルを利用するには、GitHub の [iotf-embeddedc](https://github.com/ibm-messaging/iotf-embeddedc) リポジトリーにアクセスして、インストール手順を実行します。


## 従属関係
{: #dependencies}

|従属関係 |説明|
|:---|:---|
|[Eclipse Paho Embedded C ライブラリー](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git) |MQTT C クライアント・ライブラリーを提供します。詳しくは、[MQTT クライアント・パッケージ - 組み込みデバイス用 C](http://www.eclipse.org/paho/clients/c/embedded/) を参照してください。|


## インストール
{: #installation}

Embedded C 用 {{site.data.keyword.iot_short_notm}} クライアント・ライブラリーをインストールするには、以下の手順を実行します。

1. 最新バージョンのライブラリーをインストールするには、コマンド・ラインに次のコードを入力します。
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. Paho ライブラリー .tar ファイルを *lib* ディレクトリーにコピーします。
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. ライブラリー・ファイルを解凍します。
```  cd lib
    tar xvzf org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz
```
ダウンロードしたクライアントは、次のようなファイル構造になっています。

```
 |-lib - すべての従属ファイルが入っています
 |-samples - helloWorld サンプルと sampleDevice サンプルが入っています
   |-sampleDevice.c - サンプル・デバイス実装
   |-helloworld.c - quickstart アプリケーション
   |-README.md
   |-Makefile
   |-build.sh
 |-iotfclient.c - メインクライアント・ファイル
 |-iotfclient.h - クライアント用ヘッダー・ファイル
```

## クライアント・ライブラリーの初期化
{: #initialize_client_library}

クライアント・ライブラリーをダウンロードしたら、初期化して {{site.data.keyword.iot_short_notm}} に接続する必要があります。パラメーターを渡すか構成ファイルを使用して、Embedded C 用 {{site.data.keyword.iot_short_notm}} クライアント・ライブラリーを初期化できます。

### パラメーターの引き渡し

`initialize` 関数は、{{site.data.keyword.iot_short_notm}} サービスに接続するために、以下のパラメーターを使用します。

|定義 |説明 |
|:---|:---|
|`client`|*iotfclient* へのポインター。|
|`org`|組織 ID。|
|`type` |デバイスのタイプ。|
|`id` |デバイス ID。|
|`auth-method` |使用する認証の方式。現在サポートされている値は、`token` のみです。|
|`auth-token`|デバイスを Watson IoT Platform に安全に接続するための認証トークン。|


```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	//quickstart
	rc = initialize(&client,"quickstart","iotsample","001122334455",NULL,NULL);
	//registered
	rc = initialize(&client,"org","type","id","auth-method","auth-token");
	....
```

### 構成ファイルの使用

構成ファイルを使用して Embedded C クライアント・ライブラリーを初期化することもできます。 `initialize_configfile` 関数は、構成ファイルのパスをパラメーターとして受け取ります。

```
	#include "iotfclient.h"
	....
	....
	char *filePath = "./device.cfg";
	Iotfclient client;
	rc = initialize_configfile(&client, filePath);
	....
```

構成ファイルでは、次の形式を使用する必要があります。

```
	org=$orgId
	type=$myDeviceType
	id=$myDeviceId
	auth-method=token
	auth-token=$token
```

## サービスへの接続
{: #connecting_service}

{{site.data.keyword.iot_short_notm}} Embedded C クライアント・ライブラリーを初期化した後、`connectiotf` 関数を呼び出すことによって {{site.data.keyword.iot_short_notm}} に接続できます。

```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	char *configFilePath = "./device.cfg";

	rc = initialize_configfile(&client, configFilePath);

	if(rc != SUCCESS){
		printf("initialize failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}

	rc = connectiotf(&client);

	if(rc != SUCCESS){
		printf("Connection failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}
	....
```

## コマンドの処理
{: #handling_commands}

デバイス・クライアントは、接続時に、このデバイスに対するコマンドに自動的にサブスクライブします。特定のコマンドを処理するには、`setCommandHandler` 関数を呼び出して、コマンド・コールバック関数を登録する必要があります。コールバック関数には、以下のプロパティーがあります。

|プロパティー |説明|
|:---|:---|
|`commandName`  |呼び出されたコマンドの名前。 |  
|`format`  |イベントの形式。形式は任意のストリング (JSON など) となります。|
|`payload`  |コマンド・ペイロードのデータ。最大長は 131072 バイトです。 |


```
	#include "iotfclient.h"

	void myCallback (char* commandName, char* format, void* payload)
	{
	printf("The command received :: %s\n", commandName);
	printf("format : %s\n", format);
	printf("Payload is : %s\n", (char *)payload);
	}
	...
	...
	char *filePath = "./device.cfg";
	rc = connectiotfConfig(filePath);
	setCommandHandler(myCallback);

	yield(1000);
	....

```
**注:** `yield()` 関数は、デバイスが Watson IoT Platform からコマンドを受け取ることができるようにし、接続を維持します。キープアライブ間隔によって指定された時間フレーム内に `yield()` 関数が呼び出されなければ、プラットフォームから送られるコマンドはデバイスで受け取られなくなります。`yield()` 関数に割り当てる値で、ソケットからデータを読み取ることができる時間の長さ (ミリ秒単位) を指定します。この時間が経過すると、制御がアプリケーションに戻されます。

## イベントのパブリッシュ
{: #publishing_events}

イベントは、以下のプロパティーでパブリッシュすることができます。

|プロパティー |説明|
|:---|:---|
|eventType  |パブリッシュされるイベントのタイプ (例えば、status や gps)。 |  
|eventFormat  |形式は任意のストリング (`json` など) となります。 |
|data  |ペイロードのデータ。最大長は 131072 バイトです。 |
|QoS  |パブリッシュ・イベントのサービス品質レベル。サポートされる値は、`0`、`1`、`2` です。|


```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", "{\"d\" : {\"temp\" : 34 }}", QOS0);
	....
```

## クライアントの切断
{: #disconnect_client}

クライアントを切断して接続を解放するには、次のコード・スニペットを実行します。

```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", payload , QOS0);
	...
	rc = disconnect();
	....
```

## サンプル
{: #samples}

デバイスとアプリケーションのサンプル・コードが [GitHub](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples) で提供されています。
