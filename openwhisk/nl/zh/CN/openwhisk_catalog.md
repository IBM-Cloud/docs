---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-04"
 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用针对 {{site.data.keyword.openwhisk_short}} 启用的 {{site.data.keyword.Bluemix_notm}} 服务
{: #openwhisk_ecosystem}

在 {{site.data.keyword.openwhisk}} 中，通过包的目录，您能够轻松地借助多个有用的功能增强应用程序，以及访问生态系统中的外部服务。启用了 {{site.data.keyword.openwhisk_short}} 的外部服务的示例包括 Cloudant、The Weather Company、Slack 和 GitHub。
{: shortdesc}

目录在 `/whisk.system` 名称空间中作为包提供。请参阅[浏览包](./openwhisk_packages.html#openwhisk_packagedisplay)以获取有关如何使用命令行工具来浏览目录的信息。

以下主题记录了目录中的某些包。

## 使用 Cloudant 包
{: #openwhisk_catalog_cloudant}
`/whisk.system/cloudant` 包支持您使用 Cloudant 数据库。此包中包含以下操作和订阅源。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | 包 | {{site.data.keyword.Bluemix_notm}}ServiceName、host、username、password、dbname、overwrite | 使用 Cloudant 数据库 |
| `/whisk.system/cloudant/read` | 操作 | dbname、includeDoc 和 id | 从数据库中读取文档 |
| `/whisk.system/cloudant/write` | 操作 | dbname、overwrite 和 doc | 将文档写入数据库 |
| `/whisk.system/cloudant/changes` | 订阅源 | dbname、maxTriggers | 对数据库进行更改时触发触发器事件 |

以下主题将指导您设置 Cloudant 数据库，配置关联的包以及使用 `/whisk.system/cloudant` 包中的操作和订阅源。

### 在 {{site.data.keyword.Bluemix_notm}} 中设置 Cloudant 数据库
{: #openwhisk_catalog_cloudant_in}

如果是在 {{site.data.keyword.Bluemix}} 中使用 {{site.data.keyword.openwhisk_short}}，{{site.data.keyword.openwhisk_short}} 将为 {{site.data.keyword.Bluemix_notm}} Cloudant 服务实例自动创建包绑定。如果不是在 {{site.data.keyword.Bluemix_notm}} 中使用 {{site.data.keyword.openwhisk_short}} 和 Cloudant，请跳至下一步。

1. 在 {{site.data.keyword.Bluemix_notm}} [仪表板](http://console.ng.{{site.data.keyword.Bluemix_notm}}.net)中创建 Cloudant 服务实例。

  确保记住服务实例的名称以及您所在的 {{site.data.keyword.Bluemix_notm}} 组织和空间的名称。

2. 确保 {{site.data.keyword.openwhisk_short}} CLI 位于与上一步中使用的 {{site.data.keyword.Bluemix_notm}} 组织和空间对应的名称空间中。

  ```
  wsk property set --namespace my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space
  ```
  {: pre}

  或者，可以使用 `wsk property set --namespace` 从您可访问的名称空间的列表中设置名称空间。

3. 刷新名称空间中的包。刷新操作将自动为已创建的 Cloudant 服务实例创建包绑定。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  {{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1 private binding
  ```
  {: screen}

  您会看到与 {{site.data.keyword.Bluemix_notm}} Cloudant 服务实例对应的包绑定的标准名称。

4. 检查以确认先前创建的包绑定是否已使用 Cloudant {{site.data.keyword.Bluemix_notm}} 服务实例主机和凭证进行配置。

  ```
  wsk package get /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: pre}
  ```
  ok: got package /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1, projecting parameters
  [
      ...
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
      ...
  ]
  ```
  {: screen}

### 在 {{site.data.keyword.Bluemix_notm}} 外部设置 Cloudant 数据库
{: #openwhisk_catalog_cloudant_outside}

如果不是在 {{site.data.keyword.Bluemix_notm}} 中使用 {{site.data.keyword.openwhisk_short}}，或者如果要在 {{site.data.keyword.Bluemix_notm}} 外部设置 Cloudant 数据库，那么必须为您的 Cloudant 帐户手动创建包绑定。您需要 Cloudant 帐户主机名、用户名和密码。

1. 创建为您的 Cloudant 帐户配置的包绑定。

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
  ```
  {: pre}

2. 验证包绑定是否存在。

  ```
  wsk package list
  ```
  {: pre}
  ```
packages
  /myNamespace/myCloudant private binding
  ```
  {: screen}


### 侦听对 Cloudant 数据库的更改
{: #openwhisk_catalog_cloudant_listen}

可以使用 `changes` 订阅源来配置服务，以在每次对 Cloudant 数据库进行更改时都触发触发器。参数如下所示：

- `dbname`：Cloudant 数据库的名称。
- `maxTriggers`：达到此限制时，停止触发触发器。缺省值为无限。

1. 使用先前创建的包绑定中的 `changes` 订阅源来创建触发器。确保将 `/myNamespace/myCloudant` 替换为您的包名。

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}
  ```
ok: created trigger feed myCloudantTrigger
  ```
  {: screen}

2. 轮询激活。

  ```
wsk activation poll
  ```
  {: pre}

3. 在 Cloudant 仪表板中，修改现有文档或创建新文档。

4. 观察针对每次文档更改的 `myCloudantTrigger` 触发器的新激活。

**注**：如果无法观察到新激活，请查看有关对 Cloudant 数据库执行读写操作的后续各部分。测试以下读写步骤将帮助验证 Cloudant 凭证是否正确。

现在，可以创建规则并将其关联到操作，以对文档更新做出反应。

生成的事件的内容具有以下参数：

- `id`：文档标识。
- `seq`：Cloudant 生成的序列标识。
- `changes`：对象数组，每个对象都具有 `rev` 字段，用于包含文档的修订版标识。

触发器事件的 JSON 表示如下所示：

  ```
  {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```


### 写入 Cloudant 数据库
{: #openwhisk_catalog_cloudant_write}

可以使用操作将文档存储在名为 `testdb` 的 Cloudant 数据库中。确保此数据库在 Cloudant 帐户中存在。

1. 使用先前创建的包绑定中的 `write` 操作来存储文档。确保将 `/myNamespace/myCloudant` 替换为您的包名。

  ```
  wsk action invoke /myNamespace/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```
  {: screen}

2. 通过在 Cloudant 仪表板中浏览以查找该文档，验证该文档是否存在。

  `testdb` 数据库的仪表板 URL 类似于以下内容：`https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`。


### 从 Cloudant 数据库进行读取
{: #openwhisk_catalog_cloudant_read}

可以使用操作从名为 `testdb` 的 Cloudant 数据库中访存文档。确保此数据库在 Cloudant 帐户中存在。

1. 使用先前创建的包绑定中的 `read` 操作来访存文档。确保将 `/myNamespace/myCloudant` 替换为您的包名。

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3"
    "name": "Walter White"
  }
  ```
  {: screen}

### 使用操作序列和更改触发器处理 Cloudant 数据库中的文档

您可以使用规则中的操作序列来访存和处理与 Cloudant 更改事件相关联的文档。

以下是处理文档的操作的样本代码：
```
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```
{: codeblock}

创建用于处理 Cloudant 中文档的操作：
```
wsk action create myAction myAction.js
```
{: pre}

要从数据库读取文档，您可以使用 Cloudant 包中的 `read` 操作。`read` 操作可随 `myAction` 一起编写以创建操作序列。
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

在用于激活对新 Cloudant 触发器事件的操作的规则中，可使用操作 `sequenceAction`。
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**注**：Cloudant `changes` 触发器曾经支持参数 `includeDoc`，现在该参数已不再受支持。您需要重新创建之前使用 `includeDoc` 创建的触发器。请执行以下步骤来重新创建触发器：

  ```
  wsk trigger delete myCloudantTrigger
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  上述示例可用于创建操作序列，以读取更改后的文档并调用现有操作。请务必禁用可能不再有效的任何规则，然后使用操作序列模式创建新规则。

## 使用 Alarm 包
{: #openwhisk_catalog_alarm}

`/whisk.system/alarms` 包可用于按指定的频率触发触发器。这对于设置重复发生的作业或任务（例如，每小时调用一次系统备份操作）来说非常有用。

此包中包含以下订阅源。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | 包 | - | 警报和定期实用程序 |
| `/whisk.system/alarms/alarm` | 订阅源 | cron、trigger_payload 和 maxTriggers | 定期触发触发器事件 |


### 定期触发触发器事件
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
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron "*/2 * * * *" --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

每次生成的事件将包含 `trigger_payload` 值中指定的属性作为参数。在本例中，每个触发器事件将包含参数 `name=Odin` 和 `place=Asgard`。

**注**：参数 `cron` 还支持 6 个字段的定制语法，其中第一个字段代表秒。
有关使用此定制 cron 语法的更多详细信息，请参阅 https://github.com/ncb000gt/node-cron。以下是使用 6 字段表示法的示例：
  - `*/30 * * * * *`：每 30 秒。

## 使用 Weather 包
{: #openwhisk_catalog_weather}

通过 `/whisk.system/weather` 包，可以方便地调用 Weather Company Data for IBM Bluemix API。

此包中包含以下操作。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | 包 | username 和 password | 来自 Weather Company Data for IBM Bluemix API 的服务  |
| `/whisk.system/weather/forecast` | 操作 | latitude、longitude、timePeriod | 指定时间段的预报|

建议使用 `username` 和 `password` 值创建包绑定。这样就无需在每次调用包中的操作时指定这些凭证。

### 获取某个位置的天气预报
{: #openwhisk_catalog_weather_forecast}

`/whisk.system/weather/forecast` 操作通过从 The Weather Company 调用 API，返回某个位置的天气预报。参数如下所示：

- `username`：The Weather Company Data for IBM Bluemix 的用户名，此用户名有权调用预测 API。
- `password`：The Weather Company Data for IBM Bluemix 的密码，此密码有权调用预测 API。
- `latitude`：位置的纬度坐标。
- `longitude`：位置的经度坐标。
- `timeperiod`：预报的时间段。有效选项为：'10day' -（缺省值）返回 10 天的每日预报，'48hour' - 返回 2 天的每小时预报，'current' - 返回当前天气状况，'timeseries' - 返回当前观察数据和过去长达 24 小时（从当前日期和时间开始）的观察数据。


以下是创建包绑定并获取 10 天天气预报的示例。

1. 使用 API 密钥创建包绑定。

  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}

2. 调用包绑定中的 `forecast` 操作来获取天气预报。

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude 43.7 --param longitude -79.4
  ```
  {: pre}

  ```
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  {: screen}


## 使用 Watson 包
{: #openwhisk_catalog_watson}

通过 Watson 包，可以方便地调用各种 Watson API。

提供以下 Watson 包：

| 包 | 描述 |
| --- | --- |
| `/whisk.system/watson-translator`   | 用于文本翻译和语言识别的包 |
| `/whisk.system/watson-textToSpeech` | 用于将文本转换为语音的包 |
| `/whisk.system/watson-speechToText` | 用于将语音转换为文本的包 |

**注**：当前不推荐使用 `/whisk.system/watson` 包，请迁移到上述新包，而新操作提供相同的接口。

### 使用 Watson Translator 包

通过 `/whisk.system/watson-translator` 包，可以方便地调用 Watson API 以进行翻译。

此包中包含以下操作。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | 包 | username 和 password | 用于文本翻译和语言识别的包  |
| `/whisk.system/watson-translator/translator` | 操作 | payload、translateFrom、translateTo、translateParam、username、password | 翻译文本 |
| `/whisk.system/watson-translator/languageId` | 操作 | payload、username 和 password | 识别语言 |

**注**：不推荐使用包含 `/whisk.system/watson/translate` 和 `/whisk.system/watson/languageId` 操作的 `/whisk.system/watson` 包。

#### 在 Bluemix 中设置 Watson Translator 包

如果是在 Bluemix 中使用 OpenWhisk，那么 OpenWhisk 将为 Bluemix Watson 服务实例自动创建包绑定。

1. 在 Bluemix [仪表板](http://console.ng.Bluemix.net)中创建 Watson Translator 服务实例。

  确保记住服务实例的名称以及您所在的 Bluemix 组织和空间的名称。

2. 确保 OpenWhisk CLI 位于与上一步中使用的 Bluemix 组织和空间对应的名称空间中。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  或者，可以使用 `wsk property set --namespace` 从您可访问的名称空间的列表中设置名称空间。

3. 刷新名称空间中的包。刷新操作将自动为已创建的 Watson 服务实例创建包绑定。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  {: screen}


#### 在 Bluemix 外设置 Watson Translator 包

如果不是在 Bluemix 中使用 OpenWhisk，或者如果要在 Bluemix 外部设置 Watson Translator，那么必须为您的 Watson Translator 服务手动创建包绑定。您需要 Watson Translator 服务用户名和密码。

- 创建为您的 Watson Translator 服务配置的包绑定。

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### 翻译文本
{: #openwhisk_catalog_watson_translate}

`/whisk.system/watson-translator/translator` 操作将文本从一种语言翻译为另一种语言。参数如下所示：

- `username`：Watson API 用户名。
- `password`：Watson API 密码。
- `payload`：要翻译的文本。
- `translateParam`：指示要翻译文本的输入参数。例如，如果 `translateParam=payload`，那么将翻译传递给该操作的 `payload` 参数的值。
- `translateFrom`：源语言的两位数代码。
- `translateTo`：目标语言的两位数代码。

- 调用包绑定中的 `translator` 操作，以将某些文本从英语翻译为法语。

  ```
  wsk action invoke myWatsonTranslator/translator --blocking --result --param payload 'Blue skies ahead' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


#### 识别某些文本的语言
{: #openwhisk_catalog_watson_identifylang}

`/whisk.system/watson-translator/languageId` 操作可识别某些文本的语言。参数如下所示：

- `username`：Watson API 用户名。
- `password`：Watson API 密码。
- `payload`：要识别的文本。

- 调用包绑定中的 `languageId` 操作来识别语言。

  ```
  wsk action invoke myWatsonTranslator/languageId --blocking --result --param payload 'Ciel bleu a venir'
  ```
  {: pre}
  ```
  {
    "payload": "Ciel bleu a venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  {: screen}


### 使用 Watson Text to Speech 包
{: #openwhisk_catalog_watson_texttospeech}

通过 `/whisk.system/watson-textToSpeech` 包，可以方便地调用要将文本转换为语音的 Watson API。

此包中包含以下操作。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | 包 | username 和 password | 用于将文本转换为语音的包 |
| `/whisk.system/watson-textToSpeech/textToSpeech` | 操作 | payload、voice、accept、encoding、username、password | 将文本转换为音频 |

**注**：不推荐使用包含 `/whisk.system/watson/textToSpeech` 操作的 `/whisk.system/watson` 包。

#### 在 Bluemix 中设置 Watson Text to Speech 包

如果是在 Bluemix 中使用 OpenWhisk，那么 OpenWhisk 将为 Bluemix Watson 服务实例自动创建包绑定。

1. 在 Bluemix [仪表板](http://console.ng.Bluemix.net)中创建 Watson Text to Speech 服务实例。

  确保记住服务实例的名称以及您所在的 Bluemix 组织和空间的名称。

2. 确保 OpenWhisk CLI 位于与上一步中使用的 Bluemix 组织和空间对应的名称空间中。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  或者，可以使用 `wsk property set --namespace` 从您可访问的名称空间的列表中设置名称空间。

3. 刷新名称空间中的包。刷新操作将自动为已创建的 Watson 服务实例创建包绑定。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  {: screen}


#### 在 Bluemix 外设置 Watson Text to Speech 包

如果不是在 Bluemix 中使用 OpenWhisk，或者如果要在 Bluemix 外部设置 Watson Text to Speech，那么必须为您的 Watson Text to Speech 服务手动创建包绑定。您需要 Watson Text to Speech 服务用户名和密码。

- 创建为您的 Watson Speech to Text 服务配置的包绑定。

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### 将某些文本转换为语音
{: #openwhisk_catalog_watson_speechtotext}

`/whisk.system/watson-speechToText/textToSpeech` 操作可将某些文本转换为音频语音。参数如下所示：

- `username`：Watson API 用户名。
- `password`：Watson API 密码。
- `payload`：要转换为语音的文本。
- `voice`：讲话者的声音。
- `accept`：语音文件的格式。
- `encoding`：语音二进制数据的编码。


- 调用包绑定中的 `textToSpeech` 操作来转换文本。

  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
        "payload": "<base64 encoding of a .wav file>"
  }
  ```
  {: screen}


### 使用 Watson Speech to Text 包
{: #openwhisk_catalog_watson_speechtotext}

通过 `/whisk.system/watson-speechToText` 包，可以方便地调用要将语音转换为文本的 Watson API。

此包中包含以下操作。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | 包 | username 和 password | 用于将语音转换为文本的包 |
| `/whisk.system/watson-speechToText/speechToText` | 操作 | payload、content_type、encoding、username、password、continuous、inactivity_timeout、interim_results、keywords、keywords_threshold、max_alternatives、model、timestamps、watson-token、word_alternatives_threshold、word_confidence、X-Watson-Learning-Opt-Out | 将音频转换为文本 |

**注**：不推荐使用包含 `/whisk.system/watson/speechToText` 操作的 `/whisk.system/watson` 包。

#### 在 Bluemix 中设置 Watson Speech to Text 包

如果是在 Bluemix 中使用 OpenWhisk，那么 OpenWhisk 将为 Bluemix Watson 服务实例自动创建包绑定。

1. 在 Bluemix [仪表板](http://console.ng.Bluemix.net)中创建 Watson Speech to Text 服务实例。

  确保记住服务实例的名称以及您所在的 Bluemix 组织和空间的名称。

2. 确保 OpenWhisk CLI 位于与上一步中使用的 Bluemix 组织和空间对应的名称空间中。

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  或者，可以使用 `wsk property set --namespace` 从您可访问的名称空间的列表中设置名称空间。

3. 刷新名称空间中的包。刷新操作将自动为已创建的 Watson 服务实例创建包绑定。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_SpeechToText_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_SpeechToText_Credentials-1 private
  ```
  {: screen}


#### 在 Bluemix 外设置 Watson Speech to Text 包

如果不是在 Bluemix 中使用 OpenWhisk，或者如果要在 Bluemix 外部设置 Watson Speech to Text，那么必须为您的 Watson Speech to Text 服务手动创建包绑定。您需要 Watson Speech to Text 服务用户名和密码。

- 创建为您的 Watson Speech to Text 服务配置的包绑定。

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### 将语音转换为文本

`/whisk.system/watson-speechToText/speechToText` 操作可将音频语音转换为文本。参数如下所示：

- `username`：Watson API 用户名。
- `password`：Watson API 密码。
- `payload`：要转换为文本的已编码语音二进制数据。
- `content_type`：音频的 MIME 类型。
- `encoding`：语音二进制数据的编码。
- `continuous`：指示是否返回代表长时间停顿所分隔的连续短语的多个最终结果。
- `inactivity_timeout`：如果在所提交的音频中只检测到沉默，那么在该时间（秒）之后，会关闭连接。
- `interim_results`：指示服务是否返回中间结果。
- `keywords`：要在音频中抓住的关键字列表。
- `keywords_threshold`：抓住关键字的下限置信度值。
- `max_alternatives`：要返回的替代脚本的最大数目。
- `model`：要用于辨识请求的模型的标识。
- `timestamps`：指示是否针对每一个字返回时间校准。
- `watson-token`：为服务提供认证令牌，作为提供服务凭证的替代方法。
- `word_alternatives_threshold`：将假设识别为可能的替代文字的下限置信度值。
- `word_confidence`：指示是否针对每一个字返回 0 到 1 范围内的置信度测量。
- `X-Watson-Learning-Opt-Out`：指示是否针对调用选择退出数据收集。
 

- 调用包绑定中的 `speechToText` 操作来转换已编码的音频。

  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
        "data": "Hello Watson"
  }
  ```
  {: screen}
 
 
## 使用 Message Hub 包
{: #openwhisk_catalog_message_hub}

此包允许您创建用于在消息发布到 Bluemix 上的 [Message Hub](https://developer.ibm.com/messaging/message-hub/) 服务实例时做出反应的触发器。

### 创建用于侦听 Message Hub 实例的触发器
{: #openwhisk_catalog_message_hub_trigger}
为了创建用于在消息发布到 Message Hub 实例时做出反应的触发器，您需要使用名为 `messaging/messageHubFeed` 的订阅源。此订阅源支持以下参数：

|名称|类型|描述|
|---|---|---|
|kafka_brokers_sasl|字符串的 JSON 数组|此参数是 `<host>:<port>` 字符串的数组，字符串中包含 Message Hub 实例中的代理程序|
|user|字符串|您的 Message Hub 用户名|
|password|字符串|您的 Message Hub 密码|
|topic|字符串|希望触发器侦听的主题|
|kafka_admin_url|URL 字符串|Message Hub Admin REST 接口的 URL|
|api_key|字符串|您的 Message Hub API 密钥|
|isJSONData|布尔值（可选 - 缺省值为 false）|设置为 `true` 时，订阅源在将消息内容作为触发器有效内容传递之前，会先尝试将其解析为 JSON。|

此参数列表可能看起来让人望而生畏，但可以使用包刷新 CLI 命令自动设置这些参数：

1. 在正用于 OpenWhisk 的当前组织和空间下创建 Message Hub 服务实例。

2. 验证要侦听的主题在 Message Hub 中是否已存在，或者创建要侦听消息的新主题，例如 `mytopic`。

2. 刷新名称空间中的包。刷新操作将自动为已创建的 Message Hub 服务实例创建包绑定。

  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```
  {: screen}

  现在，包绑定包含与 Message Hub 实例关联的凭证。

3. 现在，您只需创建要在新消息发布到 Message Hub 时触发的触发器即可。

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

### 在 Bluemix 外设置 Message Hub 包

如果不是在 Bluemix 中使用 OpenWhisk，或者如果要在 Bluemix 外部设置 Message Hub，那么必须为 Message Hub 服务手动创建包绑定。您需要 Message Hub 服务凭证和连接信息。

- 创建为 Message Hub 服务配置的包绑定。

  ```
  wsk trigger create MyMessageHubTrigger -f /whisk.system/messaging/messageHubFeed -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443 -p api_key <your API key>
  ```
  {: pre}

### 侦听发往 Message Hub 实例的消息
{: #openwhisk_catalog_message_hub_listen}
创建触发器后，系统将监视消息传递服务中指定的主题。发布新消息时，将触发触发器。

该触发器的有效内容将包含 `messages` 字段，此字段是自上次触发触发器以来已发布的消息的数组。数组中的每个消息对象都将包含以下字段：
- topic
- partition
- offset
- key
- value

在 Kafka 术语中，这些字段应该可顾名思义。但是，需要特别注意 `value`。如果创建触发器时 `isJSONData` 参数设置为 `false`（或根本未设置），那么 `value` 字段将为所发布消息的原始值。然而，如果创建触发器时将 `isJSONData` 设置为 `true`，那么系统将尽力尝试将此值解析为 JSON 对象。如果解析成功，那么触发器有效内容中的 `value` 将为生成的 JSON 对象。

例如，如果在 `isJSONData` 设置为 `true` 的情况下发布消息 `{"title": "Some string", "amount": 5, "isAwesome": true}`，触发器有效内容可能类似于以下内容：

```
{
  "messages": [
      {
        "partition": 0,
        "key": null,
        "offset": 421760,
        "topic": "mytopic",
        "value": {
            "amount": 5,
            "isAwesome": true,
            "title": "Some string"
        }
      }
  ]
}
```

但是，如果在 `isJSONData` 设置为 `false` 的情况下发布相同的消息，触发器有效内容将类似于以下内容：

```
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Some string\", \"amount\": 5, \"isAwesome\": true}"
    }
  ]
}
```

### 消息将批量处理
您会注意到触发器有效内容包含消息数组。这意味着如果向消息传递系统生成消息的速度非常快，订阅源将尝试在单次触发触发器时对发布的消息进行批量处理。这将允许消息更快速、更高效地发布到触发器。

请记住，对触发器所触发的操作进行编码时，有效内容中的消息数在技术上是无限的，但始终会大于 0。


## 使用 Slack 包
{: #openwhisk_catalog_slack}

通过 `/whisk.system/slack` 包，可以方便地使用 [Slack API](https://api.slack.com/)。

此包中包含以下操作：

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/slack` | 包 | url、channel 和 username | 与 Slack API 进行交互 |
| `/whisk.system/slack/post` | 操作 | text、url、channel 和 username | 将消息发布到 Slack 通道 |

建议使用 `username`、`url` 和 `channel` 值创建包绑定。通过绑定，就无需在每次调用包中的操作时指定这些值。

### 将消息发布到 Slack 通道
{: #openwhisk_catalog_slack_post}

`/whisk.system/slack/post` 操作可将消息发布到指定的 Slack 通道。参数如下所示：

- `url`：Slack Webhook URL。
- `channel`：要将消息发布到的 Slack 通道。
- `username`：发布消息的用户的名称。
- `text`：要发布的消息。
- `token`：（可选）Slack [访问令牌](https://api.slack.com/tokens)。请参阅[下文](./openwhisk_catalog.html#openwhisk_catalog_slack_token)，以获取有关使用 Slack 访问令牌的更多详细信息。

下面是配置 Slack、创建包绑定并将消息发布到通道的示例。

1. 为您的团队配置 Slack [入局 Webhook](https://api.slack.com/incoming-webhooks)。

  配置 Slack 后，您会获得类似于以下内容的 Webhook URL：`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`。下一步中将需要此 URL。

2. 使用 Slack 凭证、要发布到的通道和执行发布的用户名来创建包绑定。

  ```
  wsk package bind /whisk.system/slack mySlack --param url "https://hooks.slack.com/services/..." --param username Bob --param channel "#MySlackChannel"
  ```
  {: pre}

3. 调用包绑定中的 `post` 操作，以将消息发布到 Slack 通道。

  ```
  wsk action invoke mySlack/post --blocking --result --param text "Hello from OpenWhisk!"
  ```
  {: pre}

### 使用基于 Slack 令牌的 API
{: #openwhisk_catalog_slack_token}

如果您愿意，可选择性使用基于 Slack 令牌的 API，而不使用 Webhook API。如果选择这样做，请传递包含 Slack [访问令牌](https://api.slack.com/tokens)的 `token` 参数。然后，您可使用任一 [Slack API 方法](https://api.slack.com/methods)作为 `url` 参数。例如，要发布消息，使用的 `url` 参数值将为 [slack.postMessage](https://api.slack.com/methods/chat.postMessage)。

## 使用 GitHub 包
{: #openwhisk_catalog_github}

通过 `/whisk.system/github` 包，可以方便地使用 [GitHub API](https://developer.github.com/)。

此包中包含以下订阅源：

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/github` | 包 | username、repository 和 accessToken | 与 GitHub API 进行交互 |
| `/whisk.system/github/webhook` | 订阅源 | events、username、repository 和 accessToken | 对 GitHub 活动触发触发器事件 |

建议使用 `username`、`repository` 和 `accessToken` 值创建包绑定。通过绑定，就无需在每次使用包中的订阅源时指定这些值。

### 使用 GitHub 活动触发触发器事件
{: #openwhisk_catalog_github_fire}

`/whisk.system/github/webhook` 订阅源将服务配置为当指定的 GitHub 存储库中发生活动时触发触发器。参数如下所示：

- `username`：GitHub 存储库的用户名。
- `repository`：GitHub 存储库。
- `accessToken`：您的 GitHub 个人访问令牌。[创建令牌](https://github.com/settings/tokens)时，请确保选择 repo:status 和 public_repo 作用域。此外，请确保还没有为存储库定义任何 Webhook。
- `events`：相关的 [GitHub 事件类型](https://developer.github.com/v3/activity/events/types/)。

下面是创建触发器的示例，此触发器将在每次 GitHub 存储库中发生新落实时触发。

1. 生成 GitHub [个人访问令牌](https://github.com/settings/tokens)。

  下一步中将使用此访问令牌。

2. 使用访问令牌创建为您的 GitHub 存储库配置的包绑定。

  ```
wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. 使用 `myGit/webhook` 订阅源为 GitHub `push` 事件类型创建触发器。

  ```
wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

使用 `git push` 对 Github 存储库作出的承诺将导致触发器由 Webhook 触发。如果存在与触发器匹配的规则，那么将会调用相关联的操作。
该操作会接收 GitHub Webhook 有效内容作为输入参数。每一个 GitHub Webhook 事件都具有相似的 JSON 模式，但是却是事件类型所确定的唯一有效内容对象。
有关更多有效内容的内容信息，请参阅 [GitHub 事件和有效内容](https://developer.github.com/v3/activity/events/types/) API 文档。


## 使用 Push 包
{: #openwhisk_catalog_pushnotifications}

`/whisk.system/pushnotifications` 包允许您使用推送服务。 

此包中包含以下操作和订阅源：

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | 包 | appId、appSecret  | 使用推送服务 |
| `/whisk.system/pushnotifications/sendMessage` | 操作 | text、url、deviceIds、platforms、tagNames、apnsBadge、apnsCategory、apnsActionKeyTitle、apnsSound、apnsPayload、apnsType、gcmCollapseKey、gcmDelayWhileIdle、gcmPayload、gcmPriority、gcmSound、gcmTimeToLive | 将推送通知发送到一个或多个指定设备 |
| `/whisk.system/pushnotifications/webhook` | 订阅源 | 事件 | 在推送服务的设备活动（设备注册、取消注册、预订或取消预订）上触发触发器事件 |
建议使用 `appId` 和 `appSecret` 值创建包绑定。这样就无需在每次调用包中的操作时指定这些凭证。

### 创建 Push 包绑定
{: #openwhisk_catalog_pushnotifications_create}

创建 Push Notification 包绑定时，必须指定以下参数：

-  `appId`：Bluemix 应用程序 GUID。
-  `appSecret`：Bluemix 推送通知服务 appSecret。

下面是创建包绑定的示例。

1. 在 [Bluemix 仪表板](http://console.ng.bluemix.net)中创建 Bluemix 应用程序。

2. 初始化推送通知服务，并将该服务绑定到 Bluemix 应用程序

3. 配置 [Push Notification 应用程序](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)。

  确保记住您所创建的 Bluemix 应用程序的 `App GUID` 和 `App Secret`。


4. 创建与 `/whisk.system/pushnotifications` 的包绑定。

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}

5. 验证包绑定是否存在。

  ```
  wsk package list
  ```
  {: pre}

  ```
  packages
  /myNamespace/myPush private binding
  ```
  {: screen}

### 发送推送通知
{: #openwhisk_catalog_pushnotifications_send}

`/whisk.system/pushnotifications/sendMessage` 操作会将推送通知发送到已注册的设备。参数如下所示：
- `text`：要向用户显示的通知消息。例如：`-p text "Hi ,OpenWhisk send a notification"`。
- `url`：可与警报一起发送的可选 URL。例如：`-p url "https:\\www.w3.ibm.com"`。
- `deviceIds`：指定设备的列表。例如：`-p deviceIds "[\"deviceID1\"]"`。
- `platforms`：向指定平台的设备发送通知。“A”表示 apple (iOS) 设备，“G”表示 google (Android) 设备。例如，`-p platforms "[\"A\"]"`。
- `tagNames`：向已预订其中任何标记的设备发送通知。例如，`-p tagNames "[\"tag1\"]"`。
- `gcmPayload`：作为通知消息一部分发送的定制 JSON 有效内容。例如：`-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`：通知到达设备时，要尝试播放的声音文件（在设备上）。
- `gcmCollapseKey`：此参数可识别一组消息
- `gcmDelayWhileIdle`：当此参数设置为 true 时，表示在设备变为活动之前，不会发送消息。
- `gcmPriority`：设置消息的优先级。
- `gcmTimeToLive`：此参数指定当设备脱机时，会在 GCM 存储器中保留消息的时间长度（秒）。
- `apnsBadge`：显示为应用程序图标的角标的数字。
- `apnsCategory`：要用于交互式推送通知的类别标识。
- `apnsIosActionKey`：Action 键的标题。
- `apnsPayload`：作为通知消息一部分发送的定制 JSON 有效内容。
- `apnsType`：[“DEFAULT”、“MIXED”、“SILENT”]。
- `apnsSound`：应用程序捆绑软件中声音文件的名称。此文件的声音播放为警报。

以下是 pushnotification 包中发送推送通知的示例。

1. 使用先前创建的包绑定中的 `sendMessage` 操作来发送推送通知。确保将 `/myNamespace/myPush` 替换为您的包名。

  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}

  ```
  {
  "result": {
          "pushResponse": "{"messageId":"11111H","message":{"message":{"alert":"this is my message","url":"http.google.com"},"settings":{"apns":{"sound":"default"},"gcm":{"sound":"default"},"target":{"deviceIds":["T1","T2"]}}}"
  },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

### 在 Push 活动上触发触发器事件
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook` 可配置 Push 服务，当在指定的应用程序中存在设备活动（如设备注册/取消注册或预订/取消预订）时，触发触发器。

参数如下所示：

- `appId：`Bluemix 应用程序 GUID。
- `appSecret：`Bluemix 推送通知服务 appSecret。
- `events：`受支持的事件为 `onDeviceRegister`、`onDeviceUnregister`、`onDeviceUpdate`、`onSubscribe`、`onUnsubscribe`。要在发生所有事件时都获得通知，请使用通配符 `*`。

以下是创建触发器的示例，此触发器将在每次向 Push Notifications 服务应用程序注册新设备时触发。

1. 使用 appId 和 appSecret，创建针对 Push Notifications 服务配置的包绑定。

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. 使用 `myPush/webhook` 订阅源为 Push Notifications 服务 `onDeviceRegister` 事件类型创建触发器。

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}
