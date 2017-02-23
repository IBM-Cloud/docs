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

# Java を使用した管理対象デバイスの開発
{: #java_deviceManagement}

##概要
{: #introduction}

{{site.data.keyword.iot_full}} において、管理対象デバイスとは、デバイス管理操作 (ファームウェア、ロケーション、診断の更新など) を行うことのできるデバイスのことです。
{{site.data.keyword.iot_short}} Java™ クライアント・ライブラリーや提供された情報を使用することで、Java コードを作成して接続デバイスを管理対象デバイスにすることができます。Java コードを作成し、デバイスをデバイス管理サービスに接続してデバイス管理操作を実行するためのサンプルも用意されています。

アプリケーションが Java クライアント・ライブラリーを使用してデバイスと対話する方法について詳しくは、『[アプリケーション開発者用の Java](../../applications/libraries/java.html)』を参照してください。

## デバイス管理
{: #device_management}

[デバイス管理](../reference/device_mgmt.html)機能により、デバイス管理能力が向上し、{{site.data.keyword.iot_short_notm}} サービスが強化されます。デバイス管理では、管理対象デバイスと非管理対象デバイスを次のように区別します。

-   **管理対象デバイス**とは、管理エージェントがインストールされているデバイスとして定義されます。管理エージェントは、デバイスのメタデータを送受信し、{{site.data.keyword.iot_short_notm}} からのデバイス管理コマンドに応答します。
-   **非管理対象デバイス**とは、デバイス管理エージェントを持たないデバイスのことです。すべてのデバイスは、非管理対象デバイスとしてライフサイクルを開始します。そして、デバイス管理エージェントから {{site.data.keyword.iot_short_notm}} にメッセージを送信することで管理対象デバイスに移行できます。

## {{site.data.keyword.iot_short_notm}} デバイス管理サービスへの接続
{: #connecting_dm_service}

## デバイス・データの作成
{: #creating_device_data}

[デバイス・モデル](../reference/device_model.html)とは、デバイスのメタデータと管理特性を記述したものです。{{site.data.keyword.iot_short_notm}} のデバイス・データベースは、デバイス情報のマスター・ソースです。アプリケーションと管理対象デバイスは、ロケーションやファームウェア更新の進捗などの更新情報をデータベースに送信できます。{{site.data.keyword.iot_short_notm}} がそうした更新情報を受信すると、デバイス・データベースが更新され、アプリケーションでその情報を使用できるようになります。

`DeviceData` は、ibmiotf クライアント・ライブラリーにあるデバイス・モデルであり、そこには以下のオブジェクトがあります。

-   DeviceInfo (必須)
-   DeviceLocation (デバイスがロケーションの更新をサポートする場合は必須)
-   DiagnosticErrorCode (デバイスが ErrorCode を更新する場合は必須)
-   DiagnosticLog (デバイスがログ情報を更新する場合は必須)
-   DeviceFirmware (デバイスがファームウェア・アクションをサポートしている場合は必須)
-   DeviceMetadata (オプション)

次のコード・サンプルでは、サンプル・データを使用して、必須オブジェクト `DeviceInfo` とオプション・オブジェクト `DeviceMetadata` を作成する方法を示します。

```
DeviceInfo deviceInfo = new DeviceInfo.Builder().
           serialNumber("10087").
           manufacturer("IBM").
           model("7865").
           deviceClass("A").
           description("My RasPi Device").
           fwVersion("1.0.0").
           hwVersion("1.0").
           descriptiveLocation("EGL C").
           build();

/**
  * Create a DeviceMetadata object
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);
```

上記のサンプルで作成したオブジェクト `DeviceInfo` と `DeviceMetadata` を含んだ `DeviceData` オブジェクトを作成するために、次のコード・サンプルを使用します。

  ```
  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
               metadata(metadata).
               build();
  ```

## ManagedDevice の作成
{: #construct_managed_device}

`ManagedDevice` は、デバイスを管理対象デバイスとして {{site.data.keyword.iot_short_notm}} に接続し、1 つ以上のデバイス管理操作をデバイスが実行できるようにするデバイス・クラスです。`ManagedDevice` インスタンスを使用すると、デバイス・イベントのパブリッシュやアプリケーションからのコマンドの listen などといった、通常のデバイス操作も実行できます。

`ManagedDevice` は、さまざまなユーザー・パターンをサポートする、以下のコンストラクターを公開します。

**コンストラクター 1**

コンストラクター 1 は、`DeviceData` と以下のすべての必須プロパティーを受け入れて、`ManagedDevice` インスタンスを {{site.data.keyword.iot_short_notm}} に作成します。

|プロパティー |説明 |
|:---|:---|
|`Organization-ID` |組織 ID|
|`Device-Type` |デバイスのタイプ。通常、deviceType は、特定のタスクを実行するデバイスのグループです (例えば "weatherballoon")。|
|`Device-ID` |デバイスの ID。通常、特定のデバイス・タイプにおいて、deviceId はそのデバイスの固有 ID です (シリアル番号や MAC アドレスなど)。|
|`Authentication-Method` |使用する認証の方式。現在サポートされている値は、`token` のみです。|
|`Authentication-Token` |デバイスを Watson IoT Platform に安全に接続するための認証トークン。|


次のコードでは、`ManagedDevice` インスタンスの作成方法の概要を示します。

```
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Device-Type", "iotsample-arduino");
options.setProperty("Device-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

`DeviceClient` インスタンスを既に使用している場合には、プロパティーの名前が若干異なっており、{{site.data.keyword.iot_short_notm}} ダッシュボード内の名前を反映していることに気付くはずです。`DeviceClient` を `ManagedDevice` にマイグレーションするときにこれまでの形式を使用するには、次のサンプルに示すように `ManagedDevice` インスタンスを作成します。

```
Properties options = new Properties();
options.setProperty("org", "uguhsp");
options.setProperty("type", "iotsample-arduino");
options.setProperty("id", "00aabbccde03");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");
ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

**コンストラクター 2**

`DeviceData` インスタンスと `MqttClient` インスタンスの両方を受け入れることによって、`ManagedDevice` インスタンスを作成します。このコンストラクターでは、次のサンプルに示すとおり、デバイス・タイプやデバイス ID などのデバイス属性をさらに追加して `DeviceData` を作成する必要があります。

```
// Code that constructs the MqttClient (either Synchronous or Asynchronous MqttClient)
.....

// Code that constructs the DeviceData
DeviceData deviceData = new DeviceData.Builder().
             typeId("Device-Type").
             deviceId("Device-ID").
             deviceInfo(deviceInfo).
             metadata(metadata).
             build();

....
ManagedDevice managedDevice = new ManagedDevice(mqttClient, deviceData);
```

**注:** このコンストラクターは、カスタム・デバイス・ユーザーが、既に作成および接続されている `MqttClient` インスタンスを使用する `ManagedDevice` インスタンスを作成するときに役立ち、これをデバイス管理操作に活用することができます。しかし、すべてのデバイス機能を活用する場合は、ユーザーがライブラリーを使用することをお勧めします。

## 管理

`管理`デバイスは、manage() メソッドを呼び出してデバイス管理アクティビティーに参加することができます。デバイスがまだ {{site.data.keyword.iot_short_notm}} に接続されていない場合は、管理要求が出されると、接続要求が内部的に開始します。

```
managedDevice.manage();
```

デバイスは、多重定義された manage (lifetime) メソッドを使用して、所定の時間フレームの間にデバイスを登録することができます。この時間フレームでは、デバイスが次回の**デバイスを管理**要求を送信するまでの制限時間を指定します。これを過ぎると、デバイスは非管理対象デバイスに戻り、「休止」のマークが付けられます。

```
managedDevice.manage(3600);
```

`管理`操作について詳しくは、[documentation] を参照してください。

  [documentation]:../device_mgmt/operations/manage.html

## 管理解除

デバイスは、管理される必要がなくなったときに unmanage() メソッドを呼び出すことができます。{{site.data.keyword.iot_short_notm}} は、新しいデバイス管理要求をこのデバイスに送信しなくなり、このデバイスからのすべてのデバイス管理要求 (**デバイスを管理**要求を除く) が拒否されるようになります。

```
managedDevice.unmanage();
```

`管理解除`操作について詳しくは、[documentation] を参照してください。

  [documentation]:../device_mgmt/operations/manage.html

## ロケーションの更新
{: #construct_location_update}
デバイス位置を判別できるデバイスは、ロケーションの変更を {{site.data.keyword.iot_short_notm}} に通知することができます。ロケーションを更新するには、デバイスで、`DeviceLocation` オブジェクトを使用する `DeviceData` インスタンスを最初に作成する必要があります。

```
// Construct the location object with latitude, longitude and elevation
DeviceLocation deviceLocation = new DeviceLocation.Builder(30.28565, -97.73921).
                            elevation(10).
                            build();
DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLocation(deviceLocation).
             metadata(metadata).
             build();
```

デバイスが {{site.data.keyword.iot_short_notm}} に接続されると、次のメソッドを使用してロケーションを更新できます。

```
int rc = deviceLocation.sendLocation();
if(rc == 200) {
        System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
            System.err.println("Failed to update the location");
}
```

その後に生じるデバイス・ロケーションの更新については、次のサンプルに示すように、`DeviceLocation` オブジェクトのプロパティーを変更して更新できます。

```
int rc = deviceLocation.update(40.28, -98.33, 11);
if(rc == 200) {
    System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
    System.err.println("Failed to update the location");
}
```

update() メソッドは、{{site.data.keyword.iot_short_notm}} に新規ロケーションを通知します。

ロケーションの更新について詳しくは、リンクされた[資料](../device_mgmt/operations/update.html)を参照してください。



## エラー・コードの追加と消去
{: #appending_error_codes}

デバイスは、エラー状況の変化を {{site.data.keyword.iot_short_notm}} に通知することができます。エラー・コードを送信するには、デバイスは、次のサンプルに示すように `DiagnosticErrorCode` オブジェクトを作成する必要があります。

```
DiagnosticErrorCode errorCode = new DiagnosticErrorCode(0);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceErrorCode(errorCode).
             metadata(metadata).
             build();
```

デバイスが {{site.data.keyword.iot_short_notm}} に接続されるとすぐ、次のように send() メソッドを呼び出すことで `ErrorCode` を送信できます。

```
errorCode.send();
```

その後、次のように append メソッドを呼び出すことによって、新規 `ErrorCodes` を {{site.data.keyword.iot_short_notm}} に簡単に追加できます。

```
int rc = errorCode.append(500);
if(rc == 200) {
    System.out.println("Current Errorcode (" + errorCode + ")");
} else {
    System.out.println("Errorcode addition failed!");
}
```

また、次のように clear() メソッドを呼び出すことによって、{{site.data.keyword.iot_short_notm}} から `ErrorCodes` を消去することもできます。

```
int rc = errorCode.clear();
if(rc == 200) {
    System.out.println("ErrorCodes are cleared successfully!");
} else {
    System.out.println("Failed to clear the ErrorCodes!");
}
```

## ログ・メッセージの追加と消去

デバイスは、新しいログ・エントリーを追加することによって、{{site.data.keyword.iot_short_notm}} に変更を通知することができます。ログ・エントリーには以下の情報が含まれます。
- ログ・メッセージ
- タイム・スタンプ
- 重大度
- Base64 エンコード・バイナリー診断データ (オプション)

ログ・メッセージを送信するには、デバイスは、次のサンプルに示すように `DiagnosticLog` オブジェクトを作成する必要があります。

```
DiagnosticLog log = new DiagnosticLog(
            "Simple Log Message",
            new Date(),
            DiagnosticLog.LogSeverity.informational);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLog(log).
             metadata(metadata).
             build();
```

デバイスが {{site.data.keyword.iot_short_notm}} に接続されるとすぐ、次のサンプルに示すように send() メソッドを呼び出すことでログ・メッセージを送信できます。

```
log.send();
```

その後、次のサンプルに示すように append メソッドを呼び出すことによって、新規ログ・メッセージを {{site.data.keyword.iot_short_notm}} に簡単に追加できます。

```
int rc = log.append("sample log", new Date(), DiagnosticLog.LogSeverity.informational);

if(rc == 200) {
    System.out.println("Current Log (" + log + ")");
} else {
    System.out.println("Log Addition failed");
}
```

また、次のサンプルに示すように clear メソッドを呼び出すことによって、{{site.data.keyword.iot_short_notm}} からログ・メッセージを消去することもできます。

```
rc = log.clear();
if(rc == 200) {
    System.out.println("Logs are cleared successfully");
} else {
    System.out.println("Failed to clear the Logs")
}
```

デバイス診断操作の目的はデバイス・エラー情報を提供することです。デバイスと {{site.data.keyword.iot_short_notm}} の接続に関連した診断情報はここでは提供されません。

診断操作について詳しくは、[資料](../device_mgmt/operations/diagnostics.html)を参照してください。

## ファームウェア・アクション
{: #firmware_actions}

ファームウェア更新プロセスは、2 つの別個のアクションに分かれています。

* ファームウェアのダウンロード
* ファームウェアの更新

デバイスは、ファームウェア・アクションをサポートするために、次のアクティビティーを実行する必要があります。

**1. DeviceFirmware オブジェクトの作成**

ファームウェア・アクションを実行するために、デバイスは次のように `DeviceFirmware` オブジェクトを作成し、それを `DeviceData` に追加する必要があります。

```
DeviceFirmware firmware = new DeviceFirmware.Builder().
            version("Firmware.version").
            name("Firmware.name").
            url("Firmware.url").
            verifier("Firmware.verifier").
            state(FirmwareState.IDLE).
            build();

DeviceData deviceData = new DeviceData.Builder().
            deviceInfo(deviceInfo).
            deviceFirmware(firmware).
            metadata(metadata).
            build();

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
managedDevice.connect();
```

`DeviceFirmware` オブジェクトは、デバイスの現在のファームウェアを表しており、ファームウェア・ダウンロード・アクションとファームウェア更新アクションの状況を {{site.data.keyword.iot_short_notm}} に報告するために使用されます。

**2. サーバーへのファームウェア・アクション・サポートの通知**

サーバーがファームウェア要求を開始するには、デバイスがファームウェア・アクション・フラグを true に設定する必要があります。これは、次のメソッドにブール値を指定して呼び出すことによって行えます。

```
managedDevice.supportsFirmwareActions(true);
managedDevice.manage();
```

ファームウェア・アクション・サポートについて {{site.data.keyword.iot_short_notm}} に通知するのは管理要求であるため、ファームウェア・アクション・サポートを設定した直後に manage() メソッドを呼び出す必要があります。

**3. ファームウェア・アクション・ハンドラーの作成**

デバイスは、ファームウェア・アクションをサポートするために、ハンドラーを作成し、それを `ManagedDevice` に追加する必要があります。ハンドラーは、`DeviceFirmwareHandler` クラスを拡張し、以下のメソッドを実装する必要があります。

```
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**3.1 downloadFirmware のサンプル実装**

この実装では、ファームウェアをダウンロードしてダウンロードの状況を報告するときに `DeviceFirmware` オブジェクトを使用するロジックを追加する必要があります。ファームウェアのダウンロード操作に成功した場合、状況が `DOWNLOADED` に設定され、`UpdateStatus` が `SUCCESS` に設定されます。

ファームウェアのダウンロード中にエラーが発生した場合、状態が `IDLE` に設定され、`updateStatus` が以下のいずれかのエラー状況値に設定されます。

* `OUT_OF_MEMORY
* CONNECTION_LOST
* INVALID_URI`

次のサンプルでは、Raspberry Pi デバイス用のファームウェア・ダウンロード実装の概要を示します。

```
public void downloadFirmware(DeviceFirmware deviceFirmware) {
    boolean success = false;
    URL firmwareURL = null;
    URLConnection urlConnection = null;

    try {
        firmwareURL = new URL(deviceFirmware.getUrl());
        urlConnection = firmwareURL.openConnection();
        if(deviceFirmware.getName() != null) {
            downloadedFirmwareName = deviceFirmware.getName();
        } else {
            // use the timestamp as the name
            downloadedFirmwareName = "firmware_" +new Date().getTime()+".deb";
        }

        File file = new File(downloadedFirmwareName);
        BufferedInputStream bis = new BufferedInputStream(urlConnection.getInputStream());
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(file.getName()));

        int data = bis.read();
        if(data != -1) {
            bos.write(data);
            byte[] block = new byte[1024];
            while (true) {
                int len = bis.read(block, 0, block.length);
                if(len != -1) {
                    bos.write(block, 0, len);
                } else {
                    break;
                }
            }
            bos.close();
            bis.close();
            success = true;
        } else {
            //There is no data to read, so set an error
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
        }
    } catch(MalformedURLException me) {
        // Invalid URL, so set the status to reflect the same,
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
    } catch (IOException e) {
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.CONNECTION_LOST);
    } catch (OutOfMemoryError oom) {
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
    }

    if(success == true) {
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
        deviceFirmware.setState(FirmwareState.DOWNLOADED);
    } else {
        deviceFirmware.setState(FirmwareState.IDLE);
    }
}
```

デバイスでは、ダウンロードしたファームウェア・イメージの整合性をベリファイヤーを使用して検査し、その状況を {{site.data.keyword.iot_short_notm}} に報告することができます。ベリファイヤーは、デバイスの開始時 (DeviceFirmware オブジェクトの作成中) にデバイスで設定することもできますし、アプリケーションでファームウェア・ダウンロード要求の一部として設定することもできます。同一性を検証するサンプル・コードを以下に示します。

```
private boolean verifyFirmware(File file, String verifier) throws IOException {
    FileInputStream fis = null;
    String md5 = null;
    try {
        fis = new FileInputStream(file);
        md5 = org.apache.commons.codec.digest.DigestUtils.md5Hex(fis);
        System.out.println("Downloaded Firmware MD5 sum:: "+ md5);
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        fis.close();
    }
    if(verifier.equals(md5)) {
        System.out.println("Firmware verification successful");
        return true;
    }
    System.out.println("Download firmware checksum verification failed.. "
            + "Expected "+verifier + " found "+md5);
    return false;
}
```

コード全体を示すサンプルについては、[RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) デバイス管理サンプルを参照してください。



**3.2 updateFirmware のサンプル実装**

この実装では、ダウンロードされたファームウェアをインストールして更新の状況を報告するときに `DeviceFirmware` オブジェクトを使用するロジックを追加する必要があります。ファームウェア更新操作に成功した場合、ファームウェアの状態が IDLE に設定され、`updateStatus` が `SUCCESS` に設定されるはずです。

ファームウェア更新中にエラーが発生した場合、`updateStatus` が以下のエラー状況値のいずれかに設定されるはずです。

`* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE`

Raspberry Pi デバイスのファームウェア更新のサンプル実装を以下に示します。

```
public void updateFirmware(DeviceFirmware deviceFirmware) {
    try {
        ProcessBuilder pkgInstaller = null;
        Process p = null;
        pkgInstaller = new ProcessBuilder("sudo", "dpkg", "-i", downloadedFirmwareName);
        boolean success = false;
        try {
            p = pkgInstaller.start();
            boolean status = waitForCompletion(p, 5);
            if(status == false) {
                p.destroy();
                deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
                return;
            }
            System.out.println("Firmware Update command "+status);
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
            deviceFirmware.setState(FirmwareState.IDLE);
        } catch (IOException e) {
            e.printStackTrace();
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
        } catch (InterruptedException e) {
            e.printStackTrace();
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
        }
    } catch (OutOfMemoryError oom) {
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
    }
}
```

コード全体を示すサンプルは、デバイス管理サンプル [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) にあります。


**4. ManagedDevice へのハンドラーの追加**

{{site.data.keyword.iot_short_notm}} からファームウェア・アクション要求が出されたときに対応するメソッドを ibmiotf クライアント・ライブラリーが呼び出すように、作成されたハンドラーを ManagedDevice インスタンスに追加する必要があります。

```
DeviceFirmwareHandlerSample fwHandler = new DeviceFirmwareHandlerSample();
deviceData.addFirmwareHandler(fwHandler);
```

ファームウェア・アクションについて詳しくは、[このページ](../device_mgmt/operations/firmware_actions.html)を参照してください。

## デバイス・アクション

{{site.data.keyword.iot_short_notm}} は、以下のデバイス・アクションをサポートしています。

* リブート
* 工場出荷時設定にリセット

デバイスは、デバイス・アクションをサポートするために、次のアクティビティーを実行する必要があります。

**1. サーバーへのデバイス・アクション・サポートの通知**

リブートや工場出荷時設定へのリセットを実行するには、まず、そのサポートについてデバイスから {{site.data.keyword.iot_short_notm}} に通知する必要があります。これは、次のメソッドにブール値を指定して呼び出すことによって行えます。

```
managedDevice.supportsDeviceActions(true);
    managedDevice.manage();
```

デバイス・アクション・サポートについて {{site.data.keyword.iot_short_notm}} に通知するのは管理要求であるため、デバイス・アクション・サポートを設定した直後に manage() メソッドを呼び出す必要があります。

**2. デバイス・アクション・ハンドラーの作成**

デバイスは、デバイス・アクションをサポートするために、ハンドラーを作成し、それを ManagedDevice に追加する必要があります。ハンドラーは、DeviceActionHandler クラスを拡張し、以下のメソッドを実装する必要があります。

```
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**2.1 handleReboot のサンプル実装**

この実装では、デバイスをリブートしてリブートの状況を報告するときに DeviceAction オブジェクトを使用するロジックを追加する必要があります。デバイスは、失敗した場合にのみ、状況を更新してオプションでメッセージを出す必要があります (操作が成功した場合はデバイスがリブートされるので、デバイス・コードで {{site.data.keyword.iot_short_notm}} の更新を制御することはできなくなるからです)。Raspberry Pi デバイスのリブートのサンプル実装を以下に示します。

```
public void handleReboot(DeviceAction action) {
    ProcessBuilder processBuilder = null;
    Process p = null;
    processBuilder = new ProcessBuilder("sudo", "shutdown", "-r", "now");
    boolean status = false;
    try {
        p = processBuilder.start();
        // wait for say 2 minutes before giving it up
        status = waitForCompletion(p, 2);
    } catch (IOException e) {
        action.setMessage(e.getMessage());
    } catch (InterruptedException e) {
        action.setMessage(e.getMessage());
    }
    if(status == false) {
        action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

コード全体を示すサンプルは、デバイス管理サンプル [DeviceActionHandlerSample] にあります。

  [DeviceActionHandlerSample]: https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java

**2.2 handleFactoryReset のサンプル実装**

この実装では、デバイスを工場出荷時設定にリセットして状況を報告するときに DeviceAction オブジェクトを使用するロジックを追加する必要があります。デバイスは、失敗した場合にのみ、状況を更新してオプションでメッセージを出す必要があります (このプロセスの一部としてデバイスがリブートされるので、デバイスで {{site.data.keyword.iot_short_notm}} の状況の更新を制御することはできなくなるからです)。工場出荷時設定にリセットの実装のスケルトンを以下に示します。

```
public void handleFactoryReset(DeviceAction action) {
    try {
        // code to perform Factory reset
    } catch (IOException e) {
        action.setMessage(e.getMessage());
    }
    if(status == false) {
        action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

**3. ManagedDevice へのハンドラーの追加**

{{site.data.keyword.iot_short_notm}} からデバイス・アクション要求が出されたときに対応するメソッドを ibmiotf クライアント・ライブラリーが呼び出すように、作成されたハンドラーを ManagedDevice インスタンスに追加する必要があります。

```
DeviceActionHandlerSample actionHandler = new DeviceActionHandlerSample();
deviceData.addDeviceActionHandler(actionHandler);
```

デバイス・アクションについて詳しくは、[このページ](../device_mgmt/operations/device_actions.html)を参照してください。



## デバイス属性変更の listen
{: #listen_device_attribute}

この ibmiotf クライアント・ライブラリーは、{{site.data.keyword.iot_short_notm}} から更新要求が送られるたびに、対応するオブジェクトを更新します。このような更新要求は、アプリケーションから直接開始されるか、{{site.data.keyword.iot_short_notm}} の REST API を使用して間接的に開始されます (ファームウェア更新)。ライブラリーは、これらの属性を更新するだけでなく、デバイス属性の更新時にデバイスに通知できるようにするためのメカニズムも提供します。

この操作によって更新できる属性は、`location`、`metadata`、`device information`、`firmware` です。

デバイスで通知を受け取るために、対象のオブジェクトに対するプロパティー変更リスナーを追加する必要があります。

```
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

また、デバイスは、通知を受け取るために `propertyChange()` メソッドを実装する必要もあります。次のサンプルでこの実装方法を示します。

```
public void propertyChange(PropertyChangeEvent evt) {
    if(evt.getNewValue() == null) {
        return;
    }
    Object value = (Object) evt.getNewValue();

    switch(evt.getPropertyName()) {
        case "metadata":
            DeviceMetadata metadata = (DeviceMetadata) value;
            System.out.println("Received an updated metadata -- "+ metadata);
            break;

        case "location":
            DeviceLocation location = (DeviceLocation) value;
            System.out.println("Received an updated location -- "+ location);
            break;

        case "deviceInfo":
            DeviceInfo info = (DeviceInfo) value;
            System.out.println("Received an updated device info -- "+ info);
            break;

        case "mgmt.firmware":
            DeviceFirmware firmware = (DeviceFirmware) value;
            System.out.println("Received an updated device firmware -- "+ firmware);
            break;
    }
}
```

デバイス属性の更新について詳しくは、[このページ](../device_mgmt/operations/update.html)を参照してください。

## 例
{: #examples}

-   [SampleRasPiDMAgent](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgent.java) - Raspberry Pi でさまざまなデバイス管理操作を実行する方法を示すサンプル・エージェント・コード。
-   [SampleRasPiManagedDevice](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiManagedDevice.java) - デバイス操作と管理操作の両方を実行する方法を示すサンプル・コード。
-   [SampleRasPiDMAgentWithCustomMqttAsyncClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttAsyncClient.java) - カスタム MqttAsyncClient を使用するサンプル・エージェント・コード。
-   [SampleRasPiDMAgentWithCustomMqttClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttClient.java) - カスタム MqttClient を使用するサンプル・エージェント・コード。
-   [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) - Raspberry Pi の FirmwareHandler のサンプル実装。
-   [DeviceActionHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java) - DeviceActionHandler のサンプル実装
-   [ManagedDeviceWithLifetimeSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/ManagedDeviceWithLifetimeSample.java) - 存続期間を指定して定期的な管理要求を送信する方法を示すサンプル。
-   [DeviceAttributesUpdateListenerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceAttributesUpdateListenerSample.java) - さまざまなデバイス属性の変更を listen する方法を示すサンプル・リスナー・コード。
-   [NonBlockingDiagnosticsErrorCodeUpdateSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/NonBlockingDiagnosticsErrorCodeUpdateSample.java) - サーバーからの応答を待たずに ErrorCode を追加する方法を示すサンプル。

##レシピ
{: #Recipes}

[レシピ](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/)には、Raspberry Pi デバイスを管理対象デバイスとして {{site.data.keyword.iot_short_notm}} に接続し、このクライアント・ライブラリーを使用してさまざまなデバイス管理操作を段階的に実行する方法が示されています。
