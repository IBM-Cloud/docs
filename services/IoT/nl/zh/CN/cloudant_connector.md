---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用 {{site.data.keyword.cloudant}} 连接和配置历史服务  
{: #cloudant_main}
上次更新时间：2016 年 9 月 16 日
{: .last-updated}

通过将 {{site.data.keyword.cloudantfull}} 服务连接到 {{site.data.keyword.iot_full}}，您可以存储和访问设备数据。设备数据根据所选的存储区时间间隔，存储在每天、每周或每月数据库中。

开始使用 {{site.data.keyword.cloudant}} 来存储设备数据时，将自动创建三个数据库，一个数据库创建用于当前存储区时间间隔，一个用于下一个时间间隔，还有一个是配置数据库。可以向配置数据库添加设计文档，并在创建数据库时将这些文档复制到这些数据库。达到时间间隔结束时间时，设备数据会存储在用于新时间间隔的存储区数据库中，然后为下一个时间间隔创建新数据库。

设备数据发送到数据库时，可以采用两种存储方式中的一种进行存储。如果数据是有效的 JSON，并且设备事件的格式设置为 `JSON`，那么设备数据会采用以下格式进行存储：

```json

{
  "_id": "78bf4380-3311-11e6-a747-d7b140d1a70a",
  "_rev": "2-d13912b7c089f060a4ba7369fa86e46f",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "json_payload",
  "format": "json",
  "timestamp": "2016-06-15T16:54:41.464+01",
  "data": {
    "a": 22
  }
}

```

如果设备数据不是有效的 JSON，或者如果格式未设置为 `JSON`，那么设备数据会采用以下格式在 `payload` 字段下存储为基于 64 位编码的字符串：

```json

{
  "_id": "80f1ce10-3311-11e6-a747-d7b140d1a70a",
  "_rev": "1-bfcbf1e74389fe4188a9425c0cd2575a",
  "payload": "eHh4eHg=",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "non_json_payload",
  "format": "notjson",
  "timestamp": "2016-06-15T16:54:55.217+01"
}

```

## 开始之前  
{: #byb}

将 {{site.data.keyword.cloudant}} 连接到 {{site.data.keyword.iot_short}} 服务之前，请完成以下任务：

- 使用 Bluemix“目录”在 {{site.data.keyword.iot_short_notm}} 所在的 Bluemix 空间中设置 {{site.data.keyword.cloudant}}。

确保您在 Bluemix 组织中具有开发者特权，并且已通过 Bluemix 登录。如果没有通过 Bluemix 登录，或者在 Bluemix 组织中不具有开发者特权，那么您无法授权绑定 {{site.data.keyword.cloudant}} 和 {{site.data.keyword.iot_short_notm}}。

要连接 {{site.data.keyword.cloudant}}，请完成以下步骤：

1. 在 {{site.data.keyword.iot_short}} 仪表板上，单击导航栏中的**扩展**。
2. 在“历史数据存储”磁贴中，单击**设置**。
2. {{site.data.keyword.iot_short}} 服务所在的 Bluemix 空间内的所有可用 {{site.data.keyword.cloudant}} 服务都会列在“配置历史数据存储”部分中。
3. 选择要连接的 {{site.data.keyword.cloudant}} 服务。
4. 选择 {{site.data.keyword.cloudant}} 配置选项：

  a. 选择存储区时间间隔。存储区时间间隔控制用于存储设备数据的新数据库的创建频率。新存储区使用存储区时间间隔在所选时区中的午夜创建。

  b. 选择时区。所选时区中的时间将用于确定应该放入哪些存储区设备，而不根据设备本地时间确定。对于发送到 {{site.data.keyword.cloudant}} 的设备数据，当确定了数据将进入哪个数据库后，会将这些数据的时间戳记转换为所选时区。

  c. 选择数据库名称。数据库名称将为 `Iotp_<orgID>_<choice>_<bucket_name>`，其中 `<orgID>` 是组织标识，`<choice>` 是您选择的数据库名称，`<bucket_name>` 是字符串，用于定义数据库是使用每天、每周还是每月存储区时间间隔。`<bucket_name>` 使得以下格式。

  对于每天存储区时间间隔，`<bucket_name>` 将为 `yyyy-mm-dd`。对于每周存储区时间间隔，`<bucket_name>` 将为 `yyyy-www`，其中 `www` 指示第几周，例如 `2016-w03`。对于每月存储区时间间隔，`<bucket_name>` 将为 `yyyy-mm`。

5. 单击**授权**。
6. 单击“授权”对话框中的**确认**。

设备数据现在正在存储到 {{site.data.keyword.cloudant}}。

## 创建新的设计文档  
{: #design_docs}

新的设计文档会包含在配置数据库中，并会复制到创建的每个数据库。配置数据库名称为“Iotp_<orgid>_<choice>_configuration”，
使用的参数与“开始之前”部分的步骤 3b 中所述的数据库名称相同。

{{site.data.keyword.iot_short_notm}} 内包含的缺省设计文档除了 summarize 函数之外，还会实现当前历史中可用的查询。

可以向配置数据库添加其他设计文档，并在创建新的存储区数据库时将这些文档复制到这些数据库。要将设计添加到配置数据库，请参阅 [Cloudant API 文档](https://docs.cloudant.com/document.html)。

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant}}](link) -->
