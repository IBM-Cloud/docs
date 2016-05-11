---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用启用了 {{site.data.keyword.openwhisk_short}} 的服务 
{: #openwhisk_ecosystem}
*上次更新时间：2016 年 3 月 28 日*

在 {{site.data.keyword.openwhisk}} 中，通过包的目录，您能够轻松地借助多个有用的功能增强应用程序，以及访问生态系统中的外部服务。启用了 {{site.data.keyword.openwhisk_short}} 的外部服务的示例包括 Cloudant、The Weather Company、Slack 和 GitHub。
{: shortdesc}

目录在 `/whisk.system` 名称空间中作为包提供。请参阅[浏览包](./openwhisk_packages.html#openwhisk_packagedisplay)以获取有关如何使用命令行工具来浏览目录的信息。

以下主题记录了目录中的某些包。

## 使用 Cloudant 包
{: #openwhisk_catalog_cloudant}
`/whisk.system/cloudant` 包支持您使用 Cloudant 数据库。此包中包含以下操作和订阅源。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | 包 | {{site.data.keyword.Bluemix_notm}}ServiceName、host、username、password、dbname、includeDoc 和 overwrite | 使用 Cloudant 数据库 |
| `/whisk.system/cloudant/read` | 操作 | dbname、includeDoc 和 id | 从数据库中读取文档 |
| `/whisk.system/cloudant/write` | 操作 | dbname、overwrite 和 doc | 将文档写入数据库 |
| `/whisk.system/cloudant/changes` | 订阅源 | dbname 和 includeDoc | 对数据库进行更改时触发触发器事件 |

以下主题将指导您设置 Cloudant 数据库，配置关联的包以及使用 `/whisk.system/cloudant` 包中的操作和订阅源。

### 在 {{site.data.keyword.Bluemix_notm}} 中设置 Cloudant 数据库

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

  您应该会看到与 {{site.data.keyword.Bluemix_notm}} Cloudant 服务实例对应的包绑定的标准名称。

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

如果不是在 {{site.data.keyword.Bluemix_notm}} 中使用 {{site.data.keyword.openwhisk_short}}，或者如果要在 {{site.data.keyword.Bluemix_notm}} 外部设置 Cloudant 数据库，那么必须为您的 Cloudant 帐户手动创建包绑定。您需要 Cloudant 帐户主机名、用户名和密码。

1. 创建为您的 Cloudant 帐户配置的包绑定。

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username 'MYUSERNAME' -p password 'MYPASSWORD' -p host 'MYCLOUDANTACCOUNT.cloudant.com'
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

可以使用 `changes` 订阅源来配置服务，以在每次对 Cloudant 数据库进行更改时都触发触发器。

1. 使用先前创建的包绑定中的 `changes` 订阅源来创建触发器。确保将 `/myNamespace/myCloudant` 替换为您的包名。

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb --param includeDocs true
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

**注**：如果无法观察到新激活，请查看有关对 Cloudant 数据库执行读写操作的后续各部分。测试下面的读写步骤将帮助验证 Cloudant 凭证是否正确。

现在，可以创建规则并将其关联到操作，以对文档更新做出反应。

生成的事件的内容取决于创建触发器时 `includeDocs` 参数的值。如果设置为 true，那么触发的每个触发器事件都会包含修改后的 Cloudant 文档。例如，假设修改后的文档如下：

  ```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
  ```
  {: screen}

此示例中的代码会使用对应的 `_id`、`_rev` 和 `name` 参数来生成触发器事件。事实上，触发器事件的 JSON 表示与该文档完全相同。

否则，如果 `includeDocs` 为 false，那么事件将包含以下参数：

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

可以使用操作将文档存储在名为 `testdb` 的 Cloudant 数据库中。确保此数据库在 Cloudant 帐户中存在。

1. 使用先前创建的包绑定中的 `write` 操作来存储文档。确保将 `/myNamespace/myCloudant` 替换为您的包名。

  ```
  wsk action invoke /myNamespace/myCoudant/write --blocking --result --param dbname testdb --param doc '{"_id":"heisenberg", "name":"Walter White"}'
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCoudant/write with id 62bf696b38464fd1bcaff216a68b8287
  response:
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

可以使用操作从名为 `testdb` 的 Cloudant 数据库中访存文档。确保此数据库在 Cloudant 帐户中存在。

1. 使用先前创建的包绑定中的 `read` 操作来访存文档。确保将 `/myNamespace/myCloudant` 替换为您的包名。

  ```
  wsk action invoke /myNamespace/myCoudant/read --blocking --result --param dbname testdb --param id heisenberg
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


## 使用 Alarm 包
{: #openwhisk_catalog_alarm}

`/whisk.system/alarms` 包可用于按指定的频率触发触发器。这对于设置重复发生的作业或任务（例如，每小时调用一次系统备份操作）来说非常有用。

此包中包含以下订阅源。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | 包 | - | 警报和定期实用程序 |
| `/whisk.system/alarms/alarm` | 订阅源 | cron、trigger_payload 和 maxTriggers | 定期触发触发器事件 |


### 定期触发触发器事件

`/whisk.system/alarms/alarm` 订阅源将警报服务配置为按指定的频率触发触发器事件。参数如下所示：

- `cron`：字符串，基于 UNIX crontab 语法，用于指示何时触发触发器，时间采用全球标准时间 (UTC)。此字符串是 6 个字段组成的序列，字段之间用空格分隔：`X X X X X X `。有关使用 cron 语法的更多详细信息，请参阅 https://github.com/ncb000gt/node-cron。

- `trigger_payload`：此参数的值成为每次触发器触发时触发器的内容。

- `maxTriggers`：达到此限制时，停止触发触发器。缺省值为 1000。

下面是通过触发器事件中的 `name` 和 `place` 值创建每 20 秒将触发一次的触发器的示例。

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
  ```
  {: pre}

每次生成的事件将包含 `trigger_payload` 值中指定的属性作为参数。在本例中，每个触发器事件将包含参数 `name=Odin` 和 `place=Asgard`。


## 使用 Weather 包
{: #openwhisk_catalog_weather}

通过 `/whisk.system/weather` 包，可以方便地调用 The Weather Company API。

此包中包含以下操作。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/weather` | 包 | apiKey | 来自 The Weather Company 的服务 |
| `/whisk.system/weather/forecast` | 操作 | apiKey、latitude 和 longitude | Weather.com 10 天天气预报 |

建议使用 `apiKey` 值创建包绑定，但这并不是必需的。这样就无需在每次调用包中的操作时指定密钥。

### 获取某个位置的天气预报

`/whisk.system/weather/forecast` 操作通过从 The Weather Company 调用 API，返回某个位置的 10 天天气预报。参数如下所示：

- `apiKey`：The Weather Company 的 API 密钥，此密钥有权调用 10 天天气预报 API。
- `latitude`：位置的纬度坐标。
- `longitude`：位置的经度坐标。

下面是创建包绑定并获取 10 天天气预报的示例。

1. 使用 API 密钥创建包绑定。

  ```
  wsk package bind /whisk.system/weather myWeather --param apiKey 'MY_WEATHER_API'
  ```
  {: pre}

2. 调用包绑定中的 `forecast` 操作来获取天气预报。

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude '43.7' --param longitude '-79.4'
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

通过 `/whisk.system/watson` 包，可以方便地调用各种 Watson API。

此包中包含以下操作。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/watson` | 包 | username 和 password | Watson Analytics API 的操作 |
| `/whisk.system/watson/translate` | 操作 | translateFrom、translateTo、translateParam、username 和 password | 翻译文本 |
| `/whisk.system/watson/languageId` | 操作 | payload、username 和 password | 识别语言 |

建议使用 `username` 和 `password` 值创建包绑定，但这并不是必需的。这样就无需在每次调用包中的操作时指定这些凭证。

### 翻译文本

`/whisk.system/watson/translate` 操作将文本从一种语言翻译为另一种语言。参数如下所示：

- `username`：Watson API 用户名。
- `password`：Watson API 密码。
- `translateParam`：要翻译的输入参数。例如，如果 `translateParam=payload`，那么将翻译传递给该操作的 `payload` 参数的值。
- `translateFrom`：源语言的两位数代码。
- `translateTo`：目标语言的两位数代码。

下面是创建包绑定并翻译某些文本的示例。

1. 使用 Watson 凭证创建包绑定。

  ```
  wsk package bind /whisk.system/watson myWatson --param username 'MY_WATSON_USERNAME' --param password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. 调用包绑定中的 `translate` 操作，以将某些文本从英语翻译为法语。

  ```
  wsk action invoke myWatson/translate --blocking --result --param payload 'Blue skies ahead' --param translateParam 'payload' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  {: screen}


### 识别某些文本的语言

`/whisk.system/watson/languageId` 操作可识别某些文本的语言。参数如下所示：

- `username`：Watson API 用户名。
- `password`：Watson API 密码。
- `payload`：要识别的文本。

下面是创建包绑定并识别某些文本的语言的示例。

1. 使用 Watson 凭证创建包绑定。

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MY_WATSON_USERNAME' -p password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. 调用包绑定中的 `languageId` 操作来识别语言。

  ```
  wsk action invoke myWatson/languageId --blocking --result --param payload 'Ciel bleu a venir'
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


## 使用 Slack 包
{: #openwhisk_catalog_slack}

通过 `/whisk.system/slack` 包，可以方便地使用 [Slack API](https://api.slack.com/)。

此包中包含以下操作：

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/slack` | 包 | url、channel 和 username | 与 Slack API 进行交互 |
| `/whisk.system/slack/post` | 操作 | text、url、channel 和 username | 将消息发布到 Slack 通道 |

建议使用 `username`、`url` 和“channel”值创建包绑定，但这并不是必需的。通过绑定，就无需在每次调用包中的操作时指定这些值。

### 将消息发布到 Slack 通道

`/whisk.system/slack/post` 操作可将消息发布到指定的 Slack 通道。参数如下所示：

- `url`：Slack Webhook URL。
- `channel`：要将消息发布到的 Slack 通道。
- `username`：发布消息的用户的名称。
- `text`：要发布的消息。

下面是配置 Slack、创建包绑定并将消息发布到通道的示例。

1. 为您的团队配置 Slack [入局 Webhook](https://api.slack.com/incoming-webhooks)。

  配置 Slack 后，您应该会获得类似于以下内容的 Webhook URL：`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`。下一步中将需要此 URL。

2. 使用 Slack 凭证、要发布到的通道和执行发布的用户名来创建包绑定。

  ```
  wsk package bind /whisk.system/slack mySlack --param url 'https://hooks.slack.com/services/...' --param username 'Bob' --param channel '#MySlackChannel'
  ```
  {: pre}

3. 调用包绑定中的 `post` 操作，以将消息发布到 Slack 通道。

  ```
  wsk action invoke mySlack/post --blocking --result --param text 'Hello from OpenWhisk!'
  ```
  {: pre}


## 使用 GitHub 包
{: #openwhisk_catalog_github}

通过 `/whisk.system/github` 包，可以方便地使用 [GitHub API](https://developer.github.com/)。

此包中包含以下订阅源：

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/github` | 包 | username、repository 和 accessToken | 与 GitHub API 进行交互 |
| `/whisk.system/github/webhook` | 订阅源 | events、username、repository 和 accessToken | 对 GitHub 活动触发触发器事件 |

建议使用 `username`、`repository` 和 `accessToken` 值创建包绑定，但这并不是必需的。通过绑定，就无需在每次使用包中的订阅源时指定这些值。

### 使用 GitHub 活动触发触发器事件

`/whisk.system/github/webhook` 订阅源将服务配置为当指定的 GitHub 存储库中发生活动时触发触发器。参数如下所示：

- `username`：GitHub 存储库的用户名。
- `repository`：GitHub 存储库。
- `accessToken`：您的 GitHub 个人访问令牌。[创建令牌](https://github.com/settings/tokens)时，请确保选择 repo:status 和 public_repo 作用域。此外，请确保还没有为存储库定义任何 Webhook。
- `events`：相关的 [GitHub 活动类型](https://developer.github.com/v3/activity/events/types/)。

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

