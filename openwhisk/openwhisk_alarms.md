---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Using the Alarm package
{: #openwhisk_catalog_alarm}

The `/whisk.system/alarms` package can be used to fire a trigger at a specified frequency. This is useful for setting up recurring jobs or tasks, such as invoking a system backup action every hour.

The package includes the following feed.

| Entity | Type | Parameters | Description |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | package | - | Alarms and periodic utility |
| `/whisk.system/alarms/alarm` | feed | cron, trigger_payload, maxTriggers | Fire trigger event periodically |


## Firing a trigger event periodically
{: #openwhisk_catalog_alarm_fire}

The `/whisk.system/alarms/alarm` feed configures the Alarm service to fire a trigger event at a specified frequency. The parameters are as follows:

- `cron`: A string, based on the UNIX crontab syntax, that indicates when to fire the trigger in Coordinated Universal Time (UTC). The string is a sequence of five fields that are separated by spaces: `X X X X X`.
For more details about using cron syntax, see: http://crontab.org. Following are some examples of the frequency that is indicated by the string:

  - `* * * * *`: top of every minute.
  - `0 * * * *`: top of every hour.
  - `0 */2 * * *`: every 2 hours (i.e. 02:00:00, 04:00:00, ...)
  - `0 9 8 * *`: at 9:00:00AM (UTC) on the eighth day of every month

- `trigger_payload`: The value of this parameter becomes the content of the trigger every time the trigger is fired.

- `maxTriggers`: Stop firing triggers when this limit is reached. Defaults to 1,000,000. You can set it to infinite (-1).

The following is an example of creating a trigger that will be fired once every 2 minutes with `name` and `place` values in the trigger event.

  ```
  wsk trigger create periodic \
    --feed /whisk.system/alarms/alarm \
    --param cron "*/2 * * * *" \
    --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

Each generated event will include as parameters the properties specified in the `trigger_payload` value. In this case, each trigger event will have parameters `name=Odin` and `place=Asgard`.

**Note**: The parameter `cron` also supports a custom syntax of six fields, where the first field represents seconds. 
For more details about using this custom cron syntax, see: https://github.com/ncb000gt/node-cron. 
Here is an example using six fields notation:
  - `*/30 * * * * *`: every thirty seconds.

