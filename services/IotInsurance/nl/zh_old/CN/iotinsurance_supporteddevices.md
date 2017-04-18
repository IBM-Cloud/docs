---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 受支持的设备和供应商
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} 支持与多个云供应商和设备的集成。
{: shortdesc}

## 按供应商列出的受支持设备
{: #supportedvendors}
下表列出 {{site.data.keyword.iotinsurance_short}} 所支持的供应商和设备，并描述集成类型。以下集成类型可用：

  - **{{site.data.keyword.iot_short_notm}}** - 设备或主数据中心直接在 {{site.data.keyword.iot_short_notm}} 中发布传感器事件。{{site.data.keyword.iotinsurance_short}} 可以直接处理传感器事件，或者在 {{site.data.keyword.iotinsurance_short}} Transformer 对它们稍作修改后处理。

  - **云到云** - 设备或主数据中心在第三方云中发布传感器事件。{{site.data.keyword.iotinsurance_short}} Transformer 从第三方云中读取那些事件，并在 {{site.data.keyword.iot_short_notm}} 中对它们进行发布。

<table>
<thead>
<tr>
<th>供应商名称</th>
<th>集成类型</th>
<th>测试的设备</th>
<th>供应商信息</th>
</tr>
</thead>
<tbody>
<tr>
<td>Bosch E-Call</td>
<td>{{site.data.keyword.iot_short_notm}}.  
编写用于测试集成的网关应用程序。</td>
<td>Bosch Retrofit E-Call</td>
<td>[供应商 Web 站点 ![外部链接图标](../../icons/launch-glyph.svg)](http://www.bosch-connectivity.com/en/what_we_offer/products_and_solutions_1/retrofit_ecall/connected_devices_3){: new_window}</td>
</tr>
<tr>
<td>EnOcean</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>按钮</li>
<li>接触器</li>
<li>温度</li>
</ul>
</td>
<td>[供应商 Web 站点 ![外部链接图标](../../icons/launch-glyph.svg)](https://www.enocean.com/en/</td>){: new_window}</tr>
<tr>
<td>WiButler (iExergy)</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>烟雾探测器</li>
<li>按钮</li></td>
</ul>
<td>[供应商 Web 站点 ![外部链接图标](../../icons/launch-glyph.svg)](https://www.wibutler.com/en_GB){: new_window}</td>
</tr>
<tr>
<td>Wink</td>
<td>云到云</td>
<td>漏水</td>
<td>[供应商 Web 站点 ![外部链接图标](../../icons/launch-glyph.svg)](https://www.wink.com/){: new_window}</td>
</tr>
<tr>
<td>Yanzi</td>
<td>{{site.data.keyword.iot_short_notm}} 和云到云</td>
<td>未测试任何传感器。</td>
<td>[供应商 Web 站点 ![外部链接图标](../../icons/launch-glyph.svg)](https://ibm.ent.box.com/notes/126680846739){: new_window}</td>
</tr>
</tbody>
</table>

## 集成设备和供应商云
{: #integratingdevices}
您可将设备和供应商云与 {{site.data.keyword.iotinsurance_short}} 集成。以下各节为每个供应商提供集成过程和示例用户记录。

有关集成传感器和设备的更多信息，请参阅[设备工具包](iotinsurance_device_toolkit.html)：


### EnOcean
#### 集成过程
  1. 在连接到 {{site.data.keyword.iotinsurance_short}} 的 {{site.data.keyword.iot_short_notm}} 实例中创建网关。
  2. 将 EnOcean 主数据中心连接到 {{site.data.keyword.iot_short_notm}} 网关。
  3. 将网关标识添加到 {{site.data.keyword.iotinsurance_short}} 中的用户记录。

#### 示例用户记录

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "digital-concepts-gateway1"
    ],
    ...
}
```

### WiButler (iExergy)

#### 集成过程
目前支持与 WiButler 数据的集成仅作为概念验证或技术预览，不用作生产目的。WiButler 硬件需要固件更新，以将数据流式处理到 {{site.data.keyword.iot_short_notm}}。

#### 示例用户记录

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "Wibutler-Gateway-ID"
    ],
    ...
}
```

### Wink

#### 集成过程

**选项 1**
  1. 获取 [Wink 授权令牌 ![外部链接图标](../../icons/launch-glyph.svg)](http://docs.winkapiv2.apiary.io/#){: new_window}。
  2. 使用 {{site.data.keyword.iotinsurance_short}} API 在 {{site.data.keyword.iotinsurance_short}}系统中，将授权令牌添加到相应用户。

**选项 2**  
使用移动应用程序集成（已弃用）。此方法仅在 V1.0 版的 {{site.data.keyword.iotinsurance_short}} 中可用。

#### 示例用户记录

```
{
  "username": "user@example.com",
  "password": "",
  ....
  "deviceID": "528DB5CA-7F3D-4478-A4EB-994E7F118B6B",
  "assets": [
    {
      "name": "default",
      "providers": [
        {
          "name": "wink",
          "tokens": {
            "data": {
              "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
              "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
              "token_type": "bearer",
              "token_endpoint": "https://api.wink.com/oauth2/token",
              "scopes": "full_access"
            },
            "errors": [],
            "pagination": {},
            "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
            "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
            "token_type": "bearer",
            "token_endpoint": "https://api.wink.com/oauth2/token",
            "scopes": "full_access"
          }
        }
      ]
    }
  ]
}

```

### Yanzi
#### 集成过程
**选项 1**  
将 Yanzi Cloud 的凭证添加到提供者的 Transformer 存储库目录中的 yanzi-config.json。“yanziCloud”对象是凭证的正确位置。  

**选项 2**  
Yanzi 在 Yanzi Cloud 和 {{site.data.keyword.iot_short_notm}} 之间使用云到云集成。此集成的授权在 Yanzi Cloud 中发生。完成授权后，Yanzi Cloud 会将事件发送到 {{site.data.keyword.iot_short_notm}}。您还必须使用“iotfCredentials”对象，将 {{site.data.keyword.iot_short_notm}} 实例的凭证添加到提供者 Transformer 存储库目录的 yanzi-config.json 中。

#### 示例用户记录

```
{
  "yanziCloud": {
      "cirrusHost": "wss://",
      "username": "",
      "password": "",
      "locationId": "",
      "unitDid": ""
  },
  "iotfCredentials": {
      "org": "",
      "apiKey": "",
      "apiToken": "",
      "type": "shared",
      "mqtt_host": "gbdprt.messaging.internetofthings.ibmcloud.com",
      "domain": "internetofthings.ibmcloud.com"
  }
}
```

### Weather Company 数据
#### 集成过程
目前支持与 Weather Company 数据的集成仅作为概念验证或技术预览，不用作生产目的。

提供地址，以针对特定位置，从 Weather Company 检索当前天气（外部温度）条件。



#### 示例用户记录

```
{ "username": "johndoe",
   "fullname": "John Doe",
    "firstname": "John",
    "lastname": "Doe",
    "password": "",
     "accessLevel": 13,
     "address": "Mies-van-der-Rohe-Straße 6, 80807 München, Germany",
     ...
}

```
