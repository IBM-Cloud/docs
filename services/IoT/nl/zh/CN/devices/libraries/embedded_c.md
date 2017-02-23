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


# 针对设备开发者的 Embedded C
{: #embedded_c}

您可以使用 Embedded C 来构建和定制设备，以用于在 {{site.data.keyword.iot_full}} 上与您的组织进行交互。使用提供的信息和示例通过 Embedded C 开始开发设备。
{:shortdesc}

## 下载 Embedded C 客户机和资源
{: #embeddedc_client_download}

要访问 {{site.data.keyword.iot_short_notm}} 的 Embedded C 客户机库和样本，请转至 GitHub 中的 [iotf-embeddedc](https://github.com/ibm-messaging/iotf-embeddedc) 存储库，并完成安装指示信息。


## 依赖关系
{: #dependencies}

|依赖关系 |描述|
|:---|:---|
|[Eclipse Paho Embedded C 库](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git) |提供 MQTT C 客户机库。有关更多信息，请参阅 [MQTT Client Package -  C for embedded devices](http://www.eclipse.org/paho/clients/c/embedded/)。|


## 安装
{: #installation}

要安装 Embedded C 的 {{site.data.keyword.iot_short_notm}} 客户机库，请完成以下指示信息：

1. 要安装最新版本的库，请在命令行上输入以下代码：
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. 将 Paho 库 .tar 文件复制到 *lib* 目录。
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. 解压缩库文件
```  cd lib
    tar xvzf org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz
```
下载的客户机具有以下文件结构：

```
 |-lib - 包含所有从属文件
 |-samples - 包含 helloWorld 和 sampleDevice 样本
   |-sampleDevice.c - 样本设备实现
   |-helloworld.c - Quickstart 应用程序
   |-README.md
   |-Makefile
   |-build.sh
 |-iotfclient.c - 主客户机文件
 |-iotfclient.h - 客户机的头文件
```

## 初始化客户机库
{: #initialize_client_library}

下载客户机库后，必须对其进行初始化并将其连接到 {{site.data.keyword.iot_short_notm}}。可以通过传递参数或使用配置文件来初始化 Embedded C 的 {{site.data.keyword.iot_short_notm}} 客户机库。

### 传递参数

`initialize` 函数使用以下参数来连接到 {{site.data.keyword.iot_short_notm}} 服务：

|定义 |描述 |
|:---|:---|
|`客户机 (client)`|*iotfclient* 的指针。|
|`org`|组织标识。|
|`type` |设备类型。|
|`id` |设备的标识。|
|`auth-method` |要使用的认证方法。当前支持的唯一值是 `token`。|
|`auth-token`|用于将设备安全连接到 Watson IoT Platform 的认证令牌。|


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

### 使用配置文件

您还可使用配置文件初始化嵌入式 C 客户机库。`initialize_configfile` 函数将配置文件路径作为参数。

```
	#include "iotfclient.h"
	....
	....
	char *filePath = "./device.cfg";
	Iotfclient client;
	rc = initialize_configfile(&client, filePath);
	....
```

配置文件必须使用以下格式：

```
	org=$orgId
	type=$myDeviceType
	id=$myDeviceId
	auth-method=token
	auth-token=$token
```

## 连接到服务
{: #connecting_service}

初始化 {{site.data.keyword.iot_short_notm}} Embedded C 客户机库后，可以通过调用 `connectiotf` 函数来连接到 {{site.data.keyword.iot_short_notm}}。

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

## 处理命令
{: #handling_commands}

设备客户机进行连接时，会自动预订此设备的任何命令。要处理特定命令，需要通过调用 `setCommandHandler` 函数来注册命令回调函数。回调函数具有以下属性：

|属性 |描述|
|:---|:---|
|`commandName`  |调用的命令的名称。 |  
|`format`  |事件的格式。格式可以为任意字符串，例如 JSON。|
|`payload`  |命令有效内容的数据。最大长度为 131072 字节。 |


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
**注：**通过 `yield()` 函数，设备能接收来自 Watson IoT Platform 的命令，并使连接保持活动。如果未在 keepAlive 时间间隔指定的时间范围内调用 `yield()` 函数，那么设备不会接收到从该平台发出的任何命令。分配给 `yield()` 函数的值指定在将控制返回给应用程序之前，可以从套接字读取数据的时间长度（以毫秒为单位）。

## 发布事件
{: #publishing_events}

可以使用以下属性来发布事件：

|属性 |描述|
|:---|:---|
|eventType  |发布的事件的类型，例如 status 或 gps。 |  
|eventFormat  |格式可以为任意字符串，例如 `json`。 |
|data  |有效内容的数据。最大长度为 131072 字节。 |
|QoS  |发布活动的服务质量级别。支持的值为 `0`、`1` 和 `2`。|


```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", "{\"d\" : {\"temp\" : 34 }}", QOS0);
	....
```

## 断开客户机连接
{: #disconnect_client}

要断开客户机连接并释放连接，请运行以下代码片段：

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

## 样本
{: #samples}

样本设备和应用程序代码在 [GitHub](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples) 中提供。
