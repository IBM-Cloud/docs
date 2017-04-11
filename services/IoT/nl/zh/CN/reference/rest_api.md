---

copyright:

years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# API
{: #overview}

有多个 API 可用于为连接到 {{site.data.keyword.iot_full}} 的设备、网关和应用程序开发代码。

HTTP API 以 HTTP 基本认证保护。当您使用仪表板生成 API 密钥时，系统即会向您呈现密钥和认证令牌。有关更多信息，请参阅


## HTTP REST API

注册自己的组织后，系统会向您提供 6 个字符的组织标识。在任何 API 调用的主机名中需要此标识，在以下地址中可访问组织的基本 URL：

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002/

要认证应用程序 API 的请求，请将用户名设置为 API 密钥，将密码设置为认证令牌。

对于消息传递 API，使用以下地址：<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002


## API 链接

使用下表中的链接可了解有关 {{site.data.keyword.iot_short_notm}} 所提供 API 的更多信息。

### 一般 HTTP API

API                     | 用于...       
------------- | -------------
[组织管理 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | 配置组织（包括创建和删除设备）、检查使用情况、提供状态服务并诊断设备连接问题。
[安全 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | 管理用户邀请和认证，以及用户、API 密钥和设备的授权。
[信息管理 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  访问设备事件数据，以及获取和更新设备位置并取得该位置的天气信息。**注：**天气信息依赖于 The Weather Company 的集成。
[The Weather Company ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html#!/Device_Location_Weather){: new_window} | 将 The Weather Company 的数据与现有设备集成。
[Analytics ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/analytics.html){: new_window} | 对从设备进入 {{site.data.keyword.iot_short_notm}} 的数据创建规则、警报和操作。
[设备管理 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/device-mgmt.html){: new_window} | 使用设备管理协议与受管设备进行交互。
[消息传递 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | 使用 HTTP 发布事件并发送命令。**注：**对于消息传递 API，使用地址 https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002



### 扩展 HTTP API

API                     | 用于...       
------------- | -------------
[AT&T 扩展 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | 管理 AT&T 设备。
[Jasper 扩展 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | 管理 Jasper 设备。
[Orange 扩展 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | 查看与 {{site.data.keyword.iot_short_notm}} 组织连接且已安装 Orange SIM 卡的设备的 SIM 卡数据。
### Beta HTTP API

API                     | 用于...       
------------- | -------------
[网关安全 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | 检查角色并将角色分配给网关设备。
[设备安全 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | 检查角色并将角色分配给设备。
[接口映射 ![外部链接图标](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   使用接口映射和访问设备数据。
