---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Alarm 套件
{: #openwhisk_catalog_alarm}

`/whisk.system/alarms` 套件可以用來依指定的頻率發動觸發程式。這適用於設定循環工作或作業（例如，每個小時呼叫系統備份動作）。

該套件包含下列資訊來源。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | 套件 | - | 警示及定期公用程式 |
| `/whisk.system/alarms/alarm` | 資訊來源 | cron、trigger_payload、maxTriggers | 定期發動觸發程式事件 |


## 定期發動觸發程式事件
{: #openwhisk_catalog_alarm_fire}

`/whisk.system/alarms/alarm` 資訊來源會配置 Alarm 服務依指定的頻率發動觸發程式事件。參數如下所示：

- `cron`：根據 UNIX crontab 語法，指出何時發動觸發程式的字串（世界標準時間，UTC）。字串是五個欄位的序列，以空格區隔：`X X X X X`。
如需使用 cron 語法的詳細資料，請參閱：http://crontab.org。以下是一些以該字串指出的頻率範例：

  - `* * * * *`：每分鐘整分。
  - `0 * * * *`：每小時整點。
  - `0 */2 * * *`：每 2 小時（亦即 02:00:00、04:00:00、...）
  - `0 9 8 * *`：每月 8 日上午 9:00:00 (UTC)

- `trigger_payload`：每次發動觸發程式時，此參數的值都會變成觸發程式的內容。

- `maxTriggers`：在達到此限制時停止發動觸發程式。預設值為 1,000,000。您可以將其設定為無限 (-1)。

下列範例說明如何使用觸發程式事件中的 `name` 及 `place` 值來建立每 2 分鐘發動一次的觸發程式。

  ```
  wsk trigger create periodic \
    --feed /whisk.system/alarms/alarm \
    --param cron "*/2 * * * *" \
    --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

每一個產生的事件都會包含為參數，即 `trigger_payload` 值所指定的內容。在此情況下，每一個觸發程式事件都會有參數 `name=Odin` 及 `place=Asgard`。

**附註**：參數 `cron` 也支援六個欄位的自訂語法，其中第一個欄位代表秒。
如需使用此自訂 cron 語法的詳細資料，請參閱：https://github.com/ncb000gt/node-cron。
以下是使用六個欄位表示法的範例：
  - `*/30 * * * * *`：每 30 秒。

