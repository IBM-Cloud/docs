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


# 针对设备开发者的 mBed C++
{: #mbedcpp}

使用 [mBed C++ 客户机库](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/)可轻松将 [mBed 设备](https://www.mbed.com/en/)（例如，[LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/) 或 [FRDM-K64F](https://developer.mbed.org/platforms/FRDM-K64F/)）连接到 {{site.data.keyword.iot_full}} 服务。
{:shortdesc}

有关更多信息，请参阅 [ibmiotf](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/)（在 [developer.mbed.org](https://developer.mbed.org/) 上）。

虽然库使用的是 C++，但仍会避免动态内存分配，也不会使用 STL 函数，因为有时 mBed 设备有特殊的内存型号，会使移植变得困难。在任何情况下，库都允许您尽可能使内存使用情况可预测。

## 依赖关系
{: #dependencies}

|依赖关系 |描述|
|:---|:---|
|[Eclipse Paho MQTT 库](https://developer.mbed.org/teams/mqtt/code/MQTT/)|为 mBed 设备提供 MQTT 客户机库。有关更多信息，请参阅 [Embedded MQTT C/C++ Client Libraries](http://www.eclipse.org/paho/clients/c/embedded/)|
|[EthernetInterface library](https://developer.mbed.org/users/mbed_official/code/EthernetInterface/)|基于以太网的 mBed IP 库。|

## 如何使用库
{: #library_use}

使用 mBed C++ IBMIoTF 客户机库时，请使用 [mBed 编译器](https://developer.mbed.org/compiler/)来创建应用程序。mBed 编译器提供了轻量级在线 C/C++ IDE，此 IDE 配置用于编写、编译和下载程序以在 mBed 微控制器上运行。

**注：**您不必安装或设置任何内容就能开始运行 mBed。

有关如何将 ARM mBed NXP LPC 1768 微控制器连接到 {{site.data.keyword.iot_short_notm}} 的信息，请参阅 [mBed C++ Client Library for IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/mbed-c-client-library-for-ibm-iot-foundation/) 诀窍。

## 构造方法
{: #constructor}

构造方法用于构建客户机实例，并接受以下参数：

|参数 |描述 |
|:---|:---|
|`org` |组织标识。此值是必需的。如果使用的是 Quickstart 流，请指定 `quickstart`。|
|`type`   |设备类型。此字段是必填的。|
|`id`   |设备的标识。此字段是必填的。|
|`auth-method`   |认证方法，这是可选字段，仅对于注册流需要。当前支持的唯一值是 `token`。|
|`auth-token`   |用于将设备安全连接到 Watson IoT Platform 的认证令牌。这是可选字段，仅对于注册流需要。|

这些参数创建用于与 {{site.data.keyword.iot_short_notm}} 服务进行交互的定义。

以下代码样本概述了 DeviceClient 实例可以如何与 {{site.data.keyword.iot_short_notm}} Quickstart 服务进行交互：

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

如先前的代码样本中所示，如果未指定设备标识，那么 DeviceClient 会将设备的 MAC 地址用作设备标识来连接到 {{site.data.keyword.iot_short_notm}}。设备代码可以使用 `getDeviceId()` 方法从 DeviceClient 实例检索设备标识。

以下代码块显示了如何创建 DeviceClient 实例以与 {{site.data.keyword.iot_short_notm}} 注册的组织进行交互。

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

## 连接到 {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

设备可以通过在 DeviceClient 实例上调用 connect 函数来连接到 {{site.data.keyword.iot_short_notm}}。

```
  #include "DeviceClient.h"
  ....
  ....

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);

  bool status = client.connect();

```
成功连接后，设备可以将事件发布到 {{site.data.keyword.iot_short_notm}}，并可以侦听命令。
此外，设备还可以使用 `isConnected()` 方法来查询连接的状态，如以下示例中所示：

```
  #include "DeviceClient.h"
  ....
  ....

  client.isConnected();

```


## 发布事件
{: #publishing_events}

事件是设备将数据发布到 {{site.data.keyword.iot_short_notm}} 时所采用的机制。设备控制事件内容，并为其发送的每个事件指定名称。

{{site.data.keyword.iot_short_notm}} 实例接收到事件时，所接收事件的凭证会识别发送设备，这意味着一台设备无法冒充其他设备。

可以在 MQTT 协议定义的三个[服务质量 (QoS) 级别](../../reference/mqtt/index.html#qos-levels)中的任一级别发布事件。缺省情况下，事件在 QoS 0 级别发布。

### 使用缺省服务质量发布事件

以下样本显示了如何通过 JSON 格式将以下数据点发布到 {{site.data.keyword.iot_short_notm}}：

- LPC1768，例如 x、y 和 z 轴
- 操纵杆位置
- 当前温度读数

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
有关完整样本，请参阅 [IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp)。
### 提高事件的 QoS 级别

可以提高已发布事件的 [QoS 级别](../../reference/mqtt/index.html#qos-levels)。QoS 级别大于 `0` 的事件发布所用时间可能更长，因为包含额外的接收确认信息。

**注：**Quickstart 流方式仅支持 QoS 0。

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

### 处理事件发布期间的连接丢失错误


`publishEvent()` 方法返回 false 值时，可以检查连接的状态，如果连接断开，可以调用 `reConnect()`。

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
库不会存储在未连接状态期间发布的事件，所以在连接重新建立后，设备需要再次调用 `publishEvent()` 方法来发送这些事件。

## 处理命令
{: #handling_commands}

设备客户机进行连接时，会自动预订此设备的所有命令。要处理特定命令，需要注册命令回调方法。
消息将作为 Command 类的实例返回，此类具有以下属性：

|属性 |描述|
|:---|:---|
|`command` | 调用的命令的名称。|  
|`format`  |事件的格式。格式可以为任意字符串，例如 JSON。 |
|`payload`  |命令有效内容的数据。最大长度为 131072 字节。 |


以下代码定义了样本命令回调函数，此函数处理来自应用程序的 LED 闪烁时间间隔命令，并在 DeviceClient 实例上设置函数句柄，以便每当设备接收到 blink 命令时，都运行回调方法。

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
有关完整样本，请参阅 [IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp)。
**注：**必须定期调用 `client.yield()` 函数来接收命令。通过 `client.yield()` 函数，设备能接收来自 Watson IoT Platform 的命令，并使连接保持活动。如果未在 keepAlive 时间间隔指定的时间范围内调用 `client.yield()` 函数，那么设备不会接收到从该平台发出的任何命令。分配给 `client.yield()` 函数的值指定在将控制返回给应用程序之前，可以从套接字读取数据的时间长度（以毫秒为单位）。



## 断开客户机连接
{: #disconnect_client}

要断开客户机连接并释放连接，请运行以下代码片段：

```
	...
	client.disconnect();
	....
```
## 样本
{: #samples}

[IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/) 是一个代码样本，显示了如何使用 {{site.data.keyword.iot_short_notm}} 客户机库将 mbed LPC1768 或 FRDM-K64F 设备连接到服务实例。
