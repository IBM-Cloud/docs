---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-22"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->

# 备份数据
您可以通过复制 {{site.data.keyword.cloudantfull}} 数据库来备份 {{site.data.keyword.iotinsurance_full}} 数据。
{:shortdesc}

下表显示了存储在 {{site.data.keyword.iotinsurance_full}} 中的 {{site.data.keyword.iotinsurance_short}} 数据库。

*表 1：{{site.data.keyword.iotinsurance_short}} 数据库*

数据库名称| 更改频率| 更改原因 | 需要备份 | 注释
------------- | -------------| -------------| -------------| -------------
favorites|管理|新管理员操作|是|-
Devices|管理|添加或除去了新设备或用户|是| Transformer 通过设备提供者在内存中动态生成表并向其填入数据。对于直接连接的网关，此表会存储设备。
hazardevents|随机|检测到新的保障事件|是|-
Jscode|管理|部署了保障的新 JS 代码|是*| 管理员可以选择跳过备份并部署新版本的 JS 代码。
Promotions|管理|添加了新升级|是|-
shieldassociations|管理|添加了新用户或保障|是|-
Shields|管理|添加了新保障|是|-
Users|管理|添加了新用户|是|-
aggregation|-|-|否|可以重新构建。
aggregationschedule|-|-| 否|可以重新构建。

要备份 {{site.data.keyword.iotinsurance_short}} 数据，请执行以下步骤：

## 创建副本 {{site.data.keyword.cloudant_short_notm}} 实例
{: #createinstance}
使用 [{{site.data.keyword.cloudant}} 复制指示信息 ![外部链接图标](../../icons/launch-glyph.svg)](https://docs.cloudant.com/replication.html)，创建副本 {{site.data.keyword.cloudant}} 实例。为了进行灾难恢复，请在非原始 {{site.data.keyword.iotinsurance_short}} 服务位置创建副本。例如，如果原始实例位于达拉斯，那么副本可位于伦敦。

## 找到凭证和 URL
{: #locate_credentials}
找到原始 {{site.data.keyword.cloudant}} 实例和已复制实例的凭证和 URL。
1. 打开 {{site.data.keyword.cloudant}} 服务。
2. 单击位于服务名称下方的**服务凭证**选项卡。
3. 单击**查看凭证**。
4. 记下用户名、密码和 URL。

## 创建新的复制任务
{: #create_replication}
为必须备份的每个数据库创建复制任务。先前部分的表 1 中列出了需要备份的数据库。

1. 打开 {{site.data.keyword.Bluemix_notm}} 控制台。

2. 打开原始 {{site.data.keyword.cloudant}} 服务。

3. 单击**启动**以打开 {{site.data.keyword.cloudant}} 仪表板。

4. 在菜单上，选择**复制**。

5. 在“源数据库”部分中，输入原始数据库的 URL。每个数据库 URL 的格式均为 https://<CloudantbaseURL>/<database_name>。例如，hazardevents 数据库 URL 为 https://<CloudantbaseURL>/hazardevents。

6. 在“目标数据库”部分中，输入新数据库的 URL。

7. **重要信息：**请勿选择**持续复制**。持续复制会严重影响性能。

8. 单击**复制数据**。  

9. （可选）由于后续复制任务会覆盖先前的数据，因此请考虑将数据导出为 CSV 文件。有关指示信息，请参阅[将 Cloudant JSON 导出为 CSV、RSS 或 iCal ![外部链接图标](../../icons/launch-glyph.svg)](https://developer.ibm.com/clouddataservices/2015/09/22/export-cloudant-json-as-csv-rss-or-ical/){: new_window}。

10. 对每个数据库重复这些步骤。

## 运行备份
{: #run_backup}
创建复制任务后，可以随时重新运行备份。
1. 打开 {{site.data.keyword.Bluemix_notm}} 控制台。
2. 打开原始 {{site.data.keyword.cloudant}} 服务。
3. 单击**启动**以打开 {{site.data.keyword.cloudant}} 仪表板。
4. 在菜单上，单击**复制**，然后选择**所有复制**。
5. 选择所有数据库，然后重新运行每个复制。通过单击**活动复制**，可以检查正在执行的作业的状态。
6. 所有复制完成后，可以将数据导出为 CSV 平面文件。

## 复原数据
{: #restore_data}
可以从复制的数据库或通过装入保存的 CSV 文件来复原数据。
1. 打开 {{site.data.keyword.Bluemix_notm}} 控制台。
2. 停止 {{site.data.keyword.iotinsurance_short}} 服务。
3. 使用以下某种方法复原数据：
  - 直接将数据从 CSV 备份文件装入到主 Cloudant 实例
  - 创建复制任务，该任务将复制的数据库作为源，将原始数据库作为目标。此任务会将复制的数据移入到原始数据库。
4. 运行以下脚本以重新创建设计文档并复原引用完整性。这些脚本位于 [GitHub 站点上的 {{site.data.keyword.iotinsurance_short}} API 示例 ![外部链接图标](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/){: new_window} 中。
  - iot4i-api/wearable-framework/auto-create/create.sh - 此脚本可在 {{site.data.keyword.cloudant}} 内重新创建设计文档。
  - iot4i-api/wearable-framework/health/check-relations - 此脚本可重新建立引用完整性。例如，如果发生删除了保障但仍存在用户关联的情况，那么此脚本可进行更正。
