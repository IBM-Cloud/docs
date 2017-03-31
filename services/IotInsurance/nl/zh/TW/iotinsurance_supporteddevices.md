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

# 支援的裝置及供應商
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} 支援與多個雲端供應商及裝置的整合。
{: shortdesc}

## 依供應商排列的支援裝置
{: #supportedvendors}
下表列出 {{site.data.keyword.iotinsurance_short}} 支援的供應商及裝置，並說明整合類型。以下是可用的整合類型：

  - **{{site.data.keyword.iot_short_notm}}** - 裝置或集線器會直接在 {{site.data.keyword.iot_short_notm}} 發佈感應器事件。{{site.data.keyword.iotinsurance_short}} 可以處理感應器事件，不論是直接處理或在 {{site.data.keyword.iotinsurance_short}} Transformer 稍微修改它們之後處理。

  - **雲端對雲端** - t裝置或集線器會在協力廠商雲端中發佈感應器事件。{{site.data.keyword.iotinsurance_short}} Transformer 從協力廠商雲端讀取那些事件，並發佈在 {{site.data.keyword.iot_short_notm}}。

<table>
<thead>
<tr>
<th>供應商名稱</th>
<th>整合類型</th>
<th>已測試的裝置</th>
<th>供應商資訊</th>
</tr>
</thead>
<tbody>
<tr>
<td>Bosch E-Call</td>
<td>{{site.data.keyword.iot_short_notm}}。  
已撰寫閘道應用程式來測試整合。</td>
<td>Bosch Retrofit E-Call</td>
<td>[供應商網站 ![外部鏈結圖示](../../icons/launch-glyph.svg)](http://www.bosch-connectivity.com/en/what_we_offer/products_and_solutions_1/retrofit_ecall/connected_devices_3){: new_window}</td>
</tr>
<tr>
<td>EnOcean</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>按鈕</li>
<li>聯絡</li>
<li>溫度</li>
</ul>
</td>
<td>[供應商網站 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://www.enocean.com/en/</td>){: new_window}
</tr>
<tr>
<td>WiButler (iExergy)</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>煙霧偵測器</li>
<li>按鈕</li></td>
</ul>
<td>[供應商網站 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://www.wibutler.com/en_GB){: new_window}</td>
</tr>
<tr>
<td>Wink</td>
<td>雲端對雲端</td>
<td>漏水</td>
<td>[供應商網站 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://www.wink.com/){: new_window}</td>
</tr>
<tr>
<td>Yanzi</td>
<td>{{site.data.keyword.iot_short_notm}} 與雲端對雲端</td>
<td>未測試任何感應器。</td>
<td>[供應商網站 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://ibm.ent.box.com/notes/126680846739){: new_window}</td>
</tr>
</tbody>
</table>

## 整合裝置及供應商雲端
{: #integratingdevices}
您可以整合您的裝置及供應商雲端與 {{site.data.keyword.iotinsurance_short}}。下列各節提供每個供應商的整合程序與範例使用者記錄。

如需整合感應器及裝置的相關資訊，請參閱[裝置工具箱](iotinsurance_device_toolkit.html)：


### EnOcean
#### 整合程序
  1. 在連接至 {{site.data.keyword.iotinsurance_short}} 的 {{site.data.keyword.iot_short_notm}} 實例中建立閘道。
  2. 將 EnOcean 集線器連接至 {{site.data.keyword.iot_short_notm}} 閘道。
  3. 將閘道 ID 新增至 {{site.data.keyword.iotinsurance_short}} 中的使用者記錄。

#### 範例使用者記錄

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

#### 整合程序
與 WiButler 資料的整合目前僅以概念證明或技術預覽的形式受到支援，不作為正式作業之用。WiButler 硬體需要韌體更新才能將資料串流至 {{site.data.keyword.iot_short_notm}}。

#### 範例使用者記錄

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

#### 整合程序

**選項 1**
  1. 取得 [Wink 授權記號 ![外部鏈結圖示](../../icons/launch-glyph.svg)](http://docs.winkapiv2.apiary.io/#){: new_window}。
  2. 使用 {{site.data.keyword.iotinsurance_short}} API，將授權記號新增至 {{site.data.keyword.iotinsurance_short}} 系統中的對應使用者。

**選項 2**  
使用行動應用程式來整合（已淘汰）。此方法只適用於 {{site.data.keyword.iotinsurance_short}} 1.0 版。

#### 範例使用者記錄

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
#### 整合程序
**選項 1**  
  將 Yanzi Cloud 的認證新增到 Transformer 儲存庫的提供者目錄中的 yanzi-config.json。"yanziCloud" 物件是認證的正確位置。  

**選項 2**  
  Yanzi 在 Yanzi 雲端與 {{site.data.keyword.iot_short_notm}} 之間使用雲端對雲端的整合。這項整合的授權發生在 Yanzi 雲端內。授權完成之後，Yanzi 雲端會傳送事件至 {{site.data.keyword.iot_short_notm}}。您也必須使用 "iotfCredentials" 物件，將 {{site.data.keyword.iot_short_notm}} 實例的認證新增到 Transformer 儲存庫的提供者目錄中的 yanzi-config.json。

#### 範例使用者記錄

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

### Weather Company 資料
#### 整合程序
與 Weather Company 資料的整合目前僅以概念證明或技術預覽的形式受到支援，不作為正式作業之用。

請提供地址以從 The Weather Company 擷取特定位置的目前天氣（室外溫度）狀況。



#### 範例使用者記錄

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
