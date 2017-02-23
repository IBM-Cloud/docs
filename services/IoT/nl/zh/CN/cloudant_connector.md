---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用 {{site.data.keyword.cloudant_short_notm}} 连接和配置历史服务  
{: #cloudant_main}

通过将 {{site.data.keyword.cloudantfull}} 服务连接到 {{site.data.keyword.iot_full}}，您可以存储和访问设备数据。根据所选的存储区时间间隔，设备数据会存储在每天、每周或每月数据库中。

当开始使用 {{site.data.keyword.cloudant_short_notm}} 来存储设备数据时，将自动创建三个数据库，其中一个用于当前存储区时间间隔，一个用于即将开始的时间间隔，还有一个是配置数据库。可以将设计文档添加到配置数据库中，这样在创建新数据库时，就会将设计文档复制到新数据库。等到一个时间间隔结束时，设备数据会存储在用于这个新时间间隔的存储区数据库中，然后会为下一个时间间隔创建一个新的数据库。

当设备数据发送到数据库时，可用的存储方式有两种。如果数据是有效的 JSON，并且设备事件的格式设置为 `JSON`，那么设备数据会采用以下格式进行存储：

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

如果设备数据不是有效的 JSON，或者如果格式未设置为 `JSON`，那么设备数据会采用以下格式以基本 64 位编码字符串的形式存储在 `payload` 字段下：

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

将 {{site.data.keyword.cloudant_short_notm}} 连接到 {{site.data.keyword.iot_short}} 服务之前，请完成以下任务：

- 使用 Bluemix“目录”在 {{site.data.keyword.iot_short_notm}} 所在的 Bluemix 空间中设置 {{site.data.keyword.cloudant_short_notm}}。

确保您在 Bluemix 组织中具有开发者特权，并且已通过 Bluemix 登录。如果没有通过 Bluemix 登录，或者在 Bluemix 组织中不具有开发者特权，那么您无法授权绑定 {{site.data.keyword.cloudant_short_notm}} 和 {{site.data.keyword.iot_short_notm}}。

要连接 {{site.data.keyword.cloudant_short_notm}}，请完成以下步骤：

1. 在 {{site.data.keyword.iot_short}} 仪表板上，单击导航栏中的**扩展**。
2. 在“历史数据存储”磁贴中，单击**设置**。
2. {{site.data.keyword.iot_short}} 服务所在的 Bluemix 空间内的所有可用 {{site.data.keyword.cloudant_short_notm}} 服务都会列在“配置历史数据存储”部分中。
3. 选择要连接的 {{site.data.keyword.cloudant_short_notm}} 服务。
4. 选择 {{site.data.keyword.cloudant_short_notm}} 配置选项：

  a. 选择存储区时间间隔。存储区时间间隔控制用于存储设备数据的新数据库的创建频率。将按照所选的存储区时间间隔，在所选时区的午夜时间创建存储区。

  b. 选择时区。将根据所选时区的时间，而不是根据设备的本地时间，来确定应该放入哪些存储区设备数据。当设备数据发送到 {{site.data.keyword.cloudant_short_notm}} 时，会将数据上的时间戳记转换为所选时区，以确定数据应进入哪个数据库。

  c. 选择用于确定数据库名称的选项。数据库名称将为 `iotp_<orgID>_<dbname>_<bucket_name>`，其中：

 +  * `<orgID>` 是组织标识。
 +  * `<dbname>` 是您为数据库名称中由“`数据库名称`”字段控制的这一部分选择的值。
 +  * `<bucket_name>` 是根据您为“`存储区时间间隔`”字段选择的值确定的字符串：
 +    * 对于“`天`”存储区时间间隔，`<bucket_name>` 将为 `yyyy-mm-dd`。例如，`2016-07-06` 表示 2016 年 7 月 6 日的事件。
 +    * 对于“`周`”存储区时间间隔，`<bucket_name>` 将为 `yyyy-'w'ww`，其中 `'w'ww` 指示第几周。例如，`2016-w03` 表示 2016 年第 3 周的事件。
 +    * 对于“`月`”存储区时间间隔，`<bucket_name>` 将为 `yyyy-mm`。例如，`2016-07` 表示 2016 年 7 月的事件。

5. 单击**授权**。
6. 单击“授权”对话框中的**确认**。

设备数据现在正在存储到 {{site.data.keyword.cloudant}}。

## 关于使用历史服务的诀窍  
{: #recipes}

以下诀窍描述了如何将 {{site.data.keyword.cloudant_short_notm}} 用作 {{site.data.keyword.iot_short}} 的历史存储：

- [Configure {{site.data.keyword.cloudant_short_notm}} as Historian Data Storage for {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/cloudant-nosql-db-as-historian-data-storage-for-ibm-watson-iot-parti/) 诀窍描述了如何在 {{site.data.keyword.cloudant_short_notm}} 上存储设备数据，并演示了如何在作为历史数据存储的 {{site.data.keyword.cloudant_short_notm}} 上配置并存储设备数据。

- [Query and Process {{site.data.keyword.iot_short}} Device Data from {{site.data.keyword.cloudant_short_notm}}](https://developer.ibm.com/recipes/tutorials/cloudant-nosql-db-as-historian-data-storage-for-ibm-watson-iot-partii) 诀窍显示了如何对 {{site.data.keyword.cloudant_short_notm}} 中存储的设备数据进行查询和执行数据处理操作。

- [Visualize Watson IoT Device Data stored in Cloudant NoSQL DB](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=27327) 诀窍显示了如何链接折线图卡和历史数据存储，以在 Watson IoT Platform 仪表板上显示设备数据。


## 创建新设计文档  
{: #design_docs}

新的设计文档会包含在配置数据库中，并会复制到创建的每个数据库。配置数据库名称为“iotp_<orgid>_<choice>_configuration”，使用的参数与“开始之前”部分的步骤 3b 中所述的数据库名称相同。

{{site.data.keyword.iot_short_notm}} 内包含的缺省设计文档除了实现 summarize 函数之外，还会实现当前历史库中可用的查询。

可以向配置数据库添加其他设计文档，在创建新的存储区时间间隔数据库时，会将这些文档复制到新数据库。要将设计文档添加到配置数据库，请参阅 [Cloudant API 文档](https://docs.cloudant.com/document.html)。

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant_short_notm}}](link) -->
