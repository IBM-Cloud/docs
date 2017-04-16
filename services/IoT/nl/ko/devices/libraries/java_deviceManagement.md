---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java를 사용하여 관리 디바이스 개발
{: #java_deviceManagement}

## 소개
{: #introduction}

{{site.data.keyword.iot_full}}에서 관리 디바이스는 디바이스 관리 오퍼레이션(예: 펌웨어, 위치 및 진단 업데이트)을 수행할 수 있는 디바이스입니다.
{{site.data.keyword.iot_short}} Java™ 클라이언트 라이브러리 및 제공된 정보를 사용하여 사용자는 연결된 디바이스를 관리 디바이스로 전환하기 위한 Java 코드를 개발할 수 있습니다. 또한 디바이스 관리 서비스에 디바이스를 연결하고 디바이스 관리 오퍼레이션을 실행하기 위한 Java 코드를 개발하는 데 도움이 되도록 샘플이 제공됩니다. 

애플리케이션이 Java 클라이언트 라이브러리를 사용하여 디바이스와 상호작용하는 방법에 대한 자세한 정보는 [애플리케이션 개발자용 Java](../../applications/libraries/java.html)를 참조하십시오. 

## 디바이스 관리
{: #device_management}

[디바이스 관리](../reference/device_mgmt.html) 기능은 디바이스를 관리하는 기능을 더 많이 추가하여 {{site.data.keyword.iot_short_notm}} 서비스를 개선합니다. 디바이스 관리에서는 다음과 같이 관리 디바이스와 비관리 디바이스를 명확하게 구분합니다.

-   **관리 디바이스**는 관리 에이전트가 설치된 디바이스로 정의됩니다. 관리 에이전트는 디바이스 메타데이터를 전송하고 수신하며 {{site.data.keyword.iot_short_notm}}의 디바이스 관리 명령에 응답합니다. 
-   **비관리 디바이스**는 디바이스 관리 에이전트가 없는 디바이스입니다. 모든 디바이스는 비관리 디바이스로서 자체 라이프사이클을 시작하며, 디바이스 관리 에이전트의 메시지를 {{site.data.keyword.iot_short_notm}}에 전송하여 관리 디바이스로 상태 전이할 수 있습니다. 

## {{site.data.keyword.iot_short_notm}} 디바이스 관리 서비스에 연결
{: #connecting_dm_service}

## 디바이스 데이터 작성
{: #creating_device_data}

[디바이스 모델](../reference/device_model.html)은 디바이스의 관리 특성 및 메타데이터에 대해 설명합니다. {{site.data.keyword.iot_short_notm}}의 디바이스 데이터베이스는 디바이스 정보의 마스터 소스입니다. 애플리케이션과 관리 디바이스는 위치 또는 펌웨어 업데이트 진행상태와 같은 업데이트를 데이터베이스에 보낼 수 있습니다. {{site.data.keyword.iot_short_notm}}에서 이러한 업데이트를 받으면 디바이스 데이터베이스가 업데이트되어 애플리케이션에서 해당 정보를 사용할 수 있게 됩니다.

`DeviceData`는 ibmiotf 클라이언트 라이브러리의 디바이스 모델이며 다음 오브젝트를 포함합니다.

-   DeviceInfo(필수)
-   DeviceLocation(디바이스에서 위치 업데이트를 지원하는 경우 필수)
-   DiagnosticErrorCode(디바이스에서 ErrorCode를 업데이트할 경우 필수)
-   DiagnosticLog(디바이스에서 로그 정보를 업데이트할 경우 필수)
-   DeviceFirmware(디바이스에서 펌웨어 조치를 지원하는 경우 필수)
-   DeviceMetadata(선택사항)

다음 코드 샘플은 샘플 데이터가 있는 선택적 `DeviceMetadata` 오브젝트와 함께 필수 오브젝트 `DeviceInfo` 오브젝트를 작성하는 방법을 보여줍니다.

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

다음 코드 샘플을 사용하여 이전 샘플에서 작성한 `DeviceInfo` 및 `DeviceMetadata` 오브젝트를 포함하는 `DeviceData` 오브젝트를 작성하십시오.

  ```
  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
               metadata(metadata).
               build();
  ```

## ManagedDevice 생성
{: #construct_managed_device}

`ManagedDevice`는 디바이스를 관리 디바이스로 {{site.data.keyword.iot_short_notm}}에 연결하고 디바이스에서 하나 이상의 디바이스 관리 오퍼레이션을 수행할 수 있게 하는 디바이스 클래스입니다. 디바이스 이벤트를 공개하고 애플리케이션에서 명령을 청취하는 등의 일반 디바이스 오퍼레이션을 수행하는 데도 `ManagedDevice` 인스턴스를 사용할 수 있습니다.

`ManagedDevice`는 서로 다른 사용자 패턴을 지원하는 다음 생성자를 노출합니다.

**Constructor One**

Constructor One은 `DeviceData`와 다음 필수 특성을 모두 승인하여 {{site.data.keyword.iot_short_notm}}에 `ManagedDevice` 인스턴스를 생성합니다.

|특성 |설명  |
|:---|:---|
|`Organization-ID` |조직 ID|
|`Device-Type` |디바이스 유형입니다. 일반적으로, deviceType은 특정 태스크를 수행하는 디바이스의 그룹화입니다(예: "weatherballoon"). |
|`Device-ID` |디바이스 ID입니다. 일반적으로, 제공된 디바이스 유형의 경우 deviceId는 해당 디바이스의 고유 ID입니다(예: 일련 번호 또는 MAC 주소). |
|`Authentication-Method` |사용할 인증 메소드입니다. 현재 지원되는 값은 `token`입니다.|
|`Authentication-Token` |디바이스를 Watson IoT Platform에 안전하게 연결하기 위한 인증 토큰입니다.|


다음 코드는 `ManagedDevice` 인스턴스 작성 방법을 간략하게 설명합니다.

```
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Device-Type", "iotsample-arduino");
options.setProperty("Device-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

이미 `DeviceClient` 인스턴스를 사용 중인 경우 특성의 이름이 약간 다르며 {{site.data.keyword.iot_short_notm}} 대시보드에 해당 이름이 반영되어 있음을 알 수 있습니다. `DeviceClient`에서 `ManagedDevice`로 마이그레이션하려면 다음 샘플에 개요된 대로 `ManagedDevice` 인스턴스를 생성하여 이전 형식을 계속 사용할 수 있습니다.

```
Properties options = new Properties();
options.setProperty("org", "uguhsp");
options.setProperty("type", "iotsample-arduino");
options.setProperty("id", "00aabbccde03");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");
ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

**Constructor Two**

`DeviceData` 및 `MqttClient` 인스턴스를 모두 승인하여 `ManagedDevice` 인스턴스를 생성합니다. 이 생성자는 다음 샘플에 개요된 대로 디바이스 유형과 디바이스 ID와 같은 추가 디바이스 속성이 있는 `DeviceData`를 작성해야 합니다.

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

**참고:** 이 생성자를 사용하면 사용자 정의 디바이스 사용자가 디바이스 관리 오퍼레이션을 이용하기 위해 이미 작성되어 연결된 `MqttClient` 인스턴스를 사용하여 `ManagedDevice` 인스턴스를 작성할 수 있습니다. 그러나 모든 디바이스 기능이 가능한 라이브러리를 사용하는 것이 좋습니다.

## 관리

`관리` 디바이스는 디바이스 관리 활동에 참여하기 위해 manage() 메소드를 호출할 수 있습니다. 디바이스가 아직 {{site.data.keyword.iot_short_notm}}에 연결되지 않은 경우 관리 요청을 통해 내부적으로 연결 요청을 시작합니다.

```
managedDevice.manage();
```

디바이스에서 오버로드된 관리(수명)를 사용하여 지정된 시간 범위에 디바이스를 등록할 수 있습니다. 시간 범위는 비관리 디바이스로 되돌리거나 휴면 상태로 표시되지 않도록 디바이스에서 다른 **디바이스 관리** 요청을 보내야 하는 기간을 지정합니다.

```
managedDevice.manage(3600);
```

`관리` 오퍼레이션에 대한 자세한 정보는 [문서]를 참조하십시오.

  [documentation]:../device_mgmt/operations/manage.html

## 비관리

디바이스가 더 이상 관리되지 않아도 되는 경우 unmanage() 메소드를 호출할 수 있습니다. {{site.data.keyword.iot_short_notm}}에서 더 이상 이 디바이스에 새 디바이스 관리 요청을 보내지 않으며 **디바이스 관리** 요청을 제외하고 이 디바이스에서 보내는 모든 디바이스 관리 요청이 거부됩니다.

```
managedDevice.unmanage();
```

`비관리` 오퍼레이션에 대한 자세한 정보는 [문서]를 참조하십시오.

  [documentation]:../device_mgmt/operations/manage.html

## 위치 업데이트
{: #construct_location_update}
위치를 판별할 수 있는 디바이스는 {{site.data.keyword.iot_short_notm}}에 위치 변경에 대해 알리도록 선택할 수 있습니다. 위치를 업데이트하려면 디바이스에서 `DeviceLocation` 오브젝트가 있는 `DeviceData` 인스턴스를 먼저 작성해야 합니다.

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

디바이스가 {{site.data.keyword.iot_short_notm}}에 연결되면 다음 메소드를 사용하여 위치를 업데이트할 수 있습니다.

```
int rc = deviceLocation.sendLocation();
if(rc == 200) {
        System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
            System.err.println("Failed to update the location");
}
```

후속 디바이스 위치 업데이트 사항은 다음 샘플에 개요된 대로 `DeviceLocation` 오브젝트의 특성을 수정하여 업데이트할 수 있습니다.

```
int rc = deviceLocation.update(40.28, -98.33, 11);
if(rc == 200) {
    System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
    System.err.println("Failed to update the location");
}
```

update() 메소드는 {{site.data.keyword.iot_short_notm}}에 새 위치에 대해 알립니다.

업데이트 위치에 대한 자세한 정보는 연결된 [문서](../device_mgmt/operations/update.html)를 참조하십시오.



## 오류 코드 추가 및 지우기
{: #appending_error_codes}

디바이스에서 {{site.data.keyword.iot_short_notm}}에 오류 상태에 있는 변경에 대해 알리도록 선택할 수 있습니다. 오류 코드를 보내려면 디바이스가 다음 샘플에 개요된 대로 `DiagnosticErrorCode` 오브젝트를 생성해야 합니다.

```
DiagnosticErrorCode errorCode = new DiagnosticErrorCode(0);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceErrorCode(errorCode).
             metadata(metadata).
             build();
```

디바이스가 {{site.data.keyword.iot_short_notm}}에 연결되면 즉시 다음과 같이 send() 메소드를 호출하여 `ErrorCode`를 보낼 수 있습니다.

```
errorCode.send();
```

다음과 같이 append 메소드를 호출하여 나중에 새로운 `ErrorCodes`를 {{site.data.keyword.iot_short_notm}}에 쉽게 추가할 수 있습니다.

```
int rc = errorCode.append(500);
if(rc == 200) {
    System.out.println("Current Errorcode (" + errorCode + ")");
} else {
    System.out.println("Errorcode addition failed!");
}
```

또한 다음과 같이 clear() 메소드를 호출하여 {{site.data.keyword.iot_short_notm}}에서 `ErrorCodes`를 지울 수 있습니다.

```
int rc = errorCode.clear();
if(rc == 200) {
    System.out.println("ErrorCodes are cleared successfully!");
} else {
    System.out.println("Failed to clear the ErrorCodes!");
}
```

## 로그 메시지 추가 및 지우기

새 로그 항목을 추가하여 디바이스에서 {{site.data.keyword.iot_short_notm}}에 변경을 알리도록 선택할 수 있습니다. 로그 항목에는 다음 정보가 포함되어 있습니다.
- 로그 메시지
- 시간소인
- 심각도
- Base64 인코딩된 2진 진단 데이터(선택사항)

로그 메시지를 보내려면 디바이스가 다음 샘플에 개요된 대로 `DiagnosticLog` 오브젝트를 생성해야 합니다.

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

디바이스가 {{site.data.keyword.iot_short_notm}}에 연결되면 즉시 다음 샘플에 개요된 send() 메소드를 호출하여 로그 메시지를 보낼 수 있습니다.

```
log.send();
```

그 이후로는 다음 샘플에 개요된 대로 append 메소드를 호출하여 새 로그 메시지를 쉽게 {{site.data.keyword.iot_short_notm}}에 추가할 수 있습니다.

```
int rc = log.append("sample log", new Date(), DiagnosticLog.LogSeverity.informational);

if(rc == 200) {
    System.out.println("Current Log (" + log + ")");
} else {
    System.out.println("Log Addition failed");
}
```

또한 다음 샘플에 개요된 대로 clear 메소드를 호출하여 {{site.data.keyword.iot_short_notm}}에서 로그 메시지를 지울 수 있습니다.

```
rc = log.clear();
if(rc == 200) {
    System.out.println("Logs are cleared successfully");
} else {
    System.out.println("Failed to clear the Logs")
}
```

디바이스 진단 오퍼레이션은 디바이스 오류에 대한 정보를 제공하고 {{site.data.keyword.iot_short_notm}}에 디바이스 연결과 관련된 진단 정보는 제공하지 않습니다.

진단 오퍼레이션에 대한 자세한 정보는 [문서](../device_mgmt/operations/diagnostics.html)를 참조하십시오.

## 펌웨어 조치
{: #firmware_actions}

펌웨어 업데이트 프로세스는 다음과 같이 서로 다른 두 개의 조치로 구분됩니다.

* 펌웨어 다운로드
* 펌웨어 업데이트

디바이스는 펌웨어 조치를 지원하기 위해 다음 활동을 수행해야 합니다. 

**1. DeviceFirmware 오브젝트 생성**

펌웨어 조치를 수행하려면 다음과 같이 디바이스에서 `DeviceFirmware` 오브젝트를 생성하여 `DeviceData`에 추가해야 합니다.

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

`DeviceFirmware` 오브젝트는 디바이스의 현재 펌웨어를 나타내며 펌웨어 다운로드 상태와 펌웨어 업데이트 조치를 {{site.data.keyword.iot_short_notm}}에 보고하는 데 사용합니다.

**2. 펌웨어 조치 지원에 대해 서버에 알림**

서버가 펌웨어 요청을 시작하도록 디바이스에서 펌웨어 조치 플래그를 true로 설정해야 합니다. 부울 값으로 다음 메소드를 호출하면 가능합니다.

```
managedDevice.supportsFirmwareActions(true);
managedDevice.manage();
```

관리 요청을 통해 {{site.data.keyword.iot_short_notm}}에 펌웨어 조치 지원에 대해 알리므로 펌웨어 조치 지원을 설정한 후 바로 manage() 메소드를 호출해야 합니다.

**3. 펌웨어 조치 핸들러 작성**

펌웨어 조치를 지원하기 위해 디바이스에서 핸들러를 작성하고 `ManagedDevice`에 추가해야 합니다. 핸들러에서 `DeviceFirmwareHandler` 클래스를 확장하고 다음 메소드를 구현해야 합니다.

```
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**3.1 downloadFirmware의 샘플 구현**

구현 시 `DeviceFirmware` 오브젝트를 사용하여 펌웨어를 다운로드한 다음 다운로드 상태를 보고하는 로직을 추가해야 합니다. 펌웨어 다운로드 오퍼레이션에 성공하면 상태가 `DOWNLOADED`로 설정된 다음 `UpdateStatus`가 `SUCCESS`로 설정됩니다.

펌웨어 다운로드 중에 오류가 발생하면 상태가 `IDLE`로 설정된 다음 `updateStatus`가 다음 오류 상태 값 중 하나로 설정됩니다.

* `OUT_OF_MEMORY
* CONNECTION_LOST
* INVALID_URI`

다음 샘플은 Raspberry Pi 디바이스의 펌웨어 다운로드 구현을 간략하게 설명합니다.

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

디바이스에서 검사기를 사용하여 다운로드한 펌웨어 이미지의 무결성을 확인하고 상태를 다시 {{site.data.keyword.iot_short_notm}}에 보고합니다. 시작 중(DeviceFirmware 오브젝트를 작성하는 중) 또는 애플리케이션의 펌웨어 다운로드 요청의 일부분으로 디바이스에서 검사기를 설정할 수 있습니다. 동일하게 검사하기 위한 샘플 코드는 다음과 같습니다. 

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

전체 코드는 [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) 디바이스 관리 샘플을 참조하십시오.



**3.2 updateFirmware의 샘플 구현**

구현 시 `DeviceFirmware` 오브젝트를 통해 다운로드한 펌웨어를 설치하고 업데이트 상태를 보고하는 로직을 추가해야 합니다. 펌웨어 업데이트 오퍼레이션에 성공하면 펌웨어 상태가 IDLE로 설정되고 `updateStatus`는 `SUCCESS`로 설정되어야 합니다.

펌웨어 업데이트 중 오류가 발생한 경우 `updateStatus`를 오류 상태 값 중 하나로 설정해야 합니다.

`* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE`

Raspberry Pi 디바이스의 샘플 펌웨어 업데이트 구현은 다음과 같습니다. 

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

전체 코드는 디바이스 관리 샘플 [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java)에 있습니다.


**4. ManagedDevice에 핸들러 추가**

{{site.data.keyword.iot_short_notm}}에서 펌웨어 조치를 요청하면 ibmiotf 클라이언트 라이브러리에서 해당 메소드를 호출하도록 작성된 핸들러를 ManageDevice 인스턴스에 추가해야 합니다.

```
DeviceFirmwareHandlerSample fwHandler = new DeviceFirmwareHandlerSample();
deviceData.addFirmwareHandler(fwHandler);
```

펌웨어 조치에 대한 자세한 정보는 [이 페이지](../device_mgmt/operations/firmware_actions.html)를 참조하십시오.

## 디바이스 조치

{{site.data.keyword.iot_short_notm}}에서는 다음 디바이스 조치를 지원합니다.

* 재부팅
* 팩토리 재설정

디바이스에서 디바이스 조치를 지원하려면 다음 활동을 수행해야 합니다.

**1. 서버에 디바이스 조치 지원에 대해 알림**

재부팅 및 팩토리 재설정을 수행하려면 디바이스에서 먼저 {{site.data.keyword.iot_short_notm}}에 해당 지원에 대해 알려야 합니다. 부울 값으로 다음 메소드를 호출하면 가능합니다. 

```
managedDevice.supportsDeviceActions(true);
    managedDevice.manage();
```

관리 요청을 통해 {{site.data.keyword.iot_short_notm}}에 디바이스 조치 지원에 대해 알리므로 디바이스 조치 지원을 설정한 후 바로 manage() 메소드를 호출해야 합니다.

**2. 디바이스 조치 핸들러 작성**

디바이스 조치를 지원하려면 디바이스에서 핸들러를 작성하고 ManagedDevice에 추가해야 합니다. 핸들러에서 DeviceActionHandler 클래스를 확장하고 다음 메소드에 대한 구현을 제공해야 합니다.

```
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**2.1 handleReboot의 샘플 구현**

구현 시 DeviceAction 오브젝트를 통해 디바이스를 재부팅하고 재부팅 상태를 보고하는 로직을 추가해야 합니다. 디바이스는 실패한 경우에만 선택적 메시지와 함께 상태를 업데이트해야 합니다(오퍼레이션에 성공하면 디바이스를 재부팅하고 디바이스 코드를 통해 {{site.data.keyword.iot_short_notm}}을 업데이트할 제어 기능이 없기 때문). Raspberry Pi 디바이스의 샘플 재부팅 구현은 다음과 같습니다. 

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

전체 모드는 디바이스 관리 샘플 [DeviceActionHandlerSample]에 있습니다.

  [DeviceActionHandlerSample]: https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java

**2.2 handleFactoryReset의 샘플 구현**

구현 시 DeviceAction 오브젝트를 통해 디바이스를 팩토리 설정으로 재설정하고 상태를 보고하는 로직을 추가해야 합니다. 디바이스는 실패한 경우에만 선택적 메시지와 함께 상태를 업데이트해야 합니다(이 프로세스의 일부로 디바이스가 재부팅되고 디바이스에서 {{site.data.keyword.iot_short_notm}}의 상태를 업데이트할 제어 기능이 없기 때문). 팩토리 재설정 구현의 스켈레톤은 다음과 같습니다. 

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

**3. ManagedDevice에 핸들러 추가**

{{site.data.keyword.iot_short_notm}}에서 디바이스 조치를 요청하면 ibmiotf 클라이언트 라이브러리에서 해당 메소드를 호출하도록 작성된 핸들러를 ManageDevice 인스턴스에 추가해야 합니다.

```
DeviceActionHandlerSample actionHandler = new DeviceActionHandlerSample();
deviceData.addDeviceActionHandler(actionHandler);
```

디바이스 조치에 대한 자세한 정보는 [이 페이지](../device_mgmt/operations/device_actions.html)를 참조하십시오.



## 디바이스 속성 변경 청취
{: #listen_device_attribute}

{{site.data.keyword.iot_short_notm}}에서 업데이트 요청이 있을 때마다 이 ibmiotf 클라이언트 라이브러리에서 해당 오브젝트를 업데이트합니다. 이러한 업데이트 요청은 애플리케이션이 직접 시작하거나 {{site.data.keyword.iot_short_notm}} REST API를 통해 간접적(펌웨어 업데이트)으로 시작합니다. 이러한 속성의 업데이트 외에도 라이브러리는 디바이스 속성이 업데이트될 때마다 디바이스에 알릴 수 있는 메커니즘을 제공합니다. 

이 오퍼레이션을 통해 업데이트할 수 있는 속성은 `위치`, `메타데이터`, `디바이스 정보` 및 `펌웨어`입니다.

알림을 받으려면 디바이스에서 관심있는 오브젝트에 대한 특성 변경 리스너를 추가해야 합니다.

```
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

또한 알림을 받는 `propertyChange()` 메소드를 구현해야 합니다. 다음 샘플은 이 메소드의 구현 방법을 간략하게 설명합니다.

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

디바이스 속성 업데이트에 대한 자세한 정보는 [이 페이지](../device_mgmt/operations/update.html)를 참조하십시오.

## 예제
{: #examples}

-   [SampleRasPiDMAgent](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgent.java) - Raspberry Pi에서 다양한 디바이스 관리 오퍼레이션 수행 방법을 보여주는 샘플 에이전트 코드입니다.
-   [SampleRasPiManagedDevice](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiManagedDevice.java) - 디바이스 오퍼레이션과 관리 오퍼레이션을 모두 수행할 수 있는 방법을 보여주는 샘플 코드입니다.
-   [SampleRasPiDMAgentWithCustomMqttAsyncClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttAsyncClient.java) - 사용자 정의 MqttAsyncClient를 포함하는 샘플 에이전트 코드입니다.
-   [SampleRasPiDMAgentWithCustomMqttClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttClient.java) - 사용자 정의 MqttClient가 포함된 샘플 에이전트 코드입니다.
-   [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) - Raspberry Pi용 FirmwareHandler의 샘플 구현입니다.
-   [DeviceActionHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java) - DeviceActionHandler의 샘플 구현입니다.
-   [ManagedDeviceWithLifetimeSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/ManagedDeviceWithLifetimeSample.java) - 수명을 지정하여 정기적으로 관리 요청을 보내는 방법을 표시하는 샘플입니다.
-   [DeviceAttributesUpdateListenerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceAttributesUpdateListenerSample.java) - 다양한 디바이스 속성 변경을 청취하는 방법을 보여주는 샘플 리스너 코드입니다.
-   [NonBlockingDiagnosticsErrorCodeUpdateSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/NonBlockingDiagnosticsErrorCodeUpdateSample.java) - 서버로부터의 응답을 기다리지 않고 ErrorCode를 추가하는 방법을 보여주는 샘플입니다.

## 지침서
{: #Recipes}

이 클라이언트 라이브러리를 사용하여 단계별로 다양한 디바이스 관리 오퍼레이션을 수행하기 위해 Raspberry Pi 디바이스를 관리 디바이스로 {{site.data.keyword.iot_short_notm}}에 연결하는 방법을 보여주는 [지침서](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/)를 참조하십시오.
