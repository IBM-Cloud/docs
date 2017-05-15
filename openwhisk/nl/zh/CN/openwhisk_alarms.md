---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Alarm 包
{: #openwhisk_catalog_alarm}

`/whisk.system/alarms` 包可用于按指定的频率触发触发器。这对于设置重复发生的作业或任务（例如，每小时调用一次系统备份操作）来说非常有用。

此包中包含以下订阅源。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | 包 | - | 警报和定期实用程序 |
| `/whisk.system/alarms/alarm` | 订阅源 | cron、trigger_payload 和 maxTriggers | 定期触发触发器事件 |


## 定期触发触发器事件
{: #openwhisk_catalog_alarm_fire}

`/whisk.system/alarms/alarm` 订阅源将警报服务配置为按指定的频率触发触发器事件。参数如下所示：

- `cron`：字符串，基于 UNIX crontab 语法，用于指示何时触发触发器，时间采用全球标准时间 (UTC)。此字符串是 5 个字段组成的序列，字段之间用空格分隔：`X X X X X`。有关使用 cron 语法的更多详细信息，请参阅 http://crontab.org。以下是该字符串所指示的一些频率示例：

  - `* * * * *`：每一分钟的顶部。
  - `0 * * * *`：每一小时的顶部。
  - `0 */2 * * *`：每 2 小时（即 02:00:00、04:00:00、...）
  - `0 9 8 * *`：每一个月第八天的上午 9:00:00 (UTC)

- `trigger_payload`：此参数的值成为每次触发器触发时触发器的内容。

- `maxTriggers`：达到此限制时，停止触发触发器。缺省值为 1,000,000。您可以将其设置为无限 (-1)。

以下是通过触发器事件中的 `name` 和 `place` 值创建每 2 分钟将触发一次的触发器的示例。

  ```
  wsk trigger create periodic \
    --feed /whisk.system/alarms/alarm \
    --param cron "*/2 * * * *" \
    --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

每次生成的事件将包含 `trigger_payload` 值中指定的属性作为参数。在本例中，每个触发器事件将包含参数 `name=Odin` 和 `place=Asgard`。

**注**：参数 `cron` 还支持 6 个字段的定制语法，其中第一个字段代表秒。
有关使用此定制 cron 语法的更多详细信息，请参阅 https://github.com/ncb000gt/node-cron。以下是使用 6 字段表示法的示例：
  - `*/30 * * * * *`：每 30 秒。

