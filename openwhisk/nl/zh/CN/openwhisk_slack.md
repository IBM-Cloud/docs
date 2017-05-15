---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Slack 包
{: #openwhisk_catalog_slack}

通过 `/whisk.system/slack` 包，可以方便地使用 [Slack API](https://api.slack.com/)。

此包中包含以下操作：

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/slack` | 包 | url、channel 和 username | 与 Slack API 进行交互 |
| `/whisk.system/slack/post` | 操作 | text、url、channel 和 username | 将消息发布到 Slack 通道 |

建议使用 `username`、`url` 和 `channel` 值创建包绑定。通过绑定，就无需在每次调用包中的操作时指定这些值。

## 将消息发布到 Slack 通道

`/whisk.system/slack/post` 操作可将消息发布到指定的 Slack 通道。参数如下所示：

- `url`：Slack Webhook URL。
- `channel`：要将消息发布到的 Slack 通道。
- `username`：发布消息的用户的名称。
- `text`：要发布的消息。
- `token`：（可选）Slack [访问令牌](https://api.slack.com/tokens)。请参阅[下文](./catalog.md#using-the-slack-token-based-api)，以获取有关使用 Slack 访问令牌的更多详细信息。

下面是配置 Slack、创建包绑定并将消息发布到通道的示例。

1. 为您的团队配置 Slack [入局 Webhook](https://api.slack.com/incoming-webhooks)。
  
  配置 Slack 后，您会获得类似于以下内容的 Webhook URL：`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`。下一步中将需要此 URL。
  
2. 使用 Slack 凭证、要发布到的通道和执行发布的用户名来创建包绑定。
  
  ```
  wsk package bind /whisk.system/slack mySlack \
    --param url "https://hooks.slack.com/services/..." \
    --param username "Bob" \
    --param channel "#MySlackChannel"
  ```
  {: pre}
  
3. 调用包绑定中的 `post` 操作，以将消息发布到 Slack 通道。
  
  ```
  wsk action invoke mySlack/post --blocking --result \
    --param text "Hello from OpenWhisk!"
  ```
  {: pre}
  

## 使用基于 Slack 令牌的 API

如果您愿意，可选择性使用基于 Slack 令牌的 API，而不使用 Webhook API。如果选择这样做，请传递包含 Slack [访问令牌](https://api.slack.com/tokens)的 `token` 参数。然后，您可使用任一 [Slack API 方法](https://api.slack.com/methods)作为 `url` 参数。例如，要发布消息，使用的 `url` 参数值将为 [slack.postMessage](https://api.slack.com/methods/chat.postMessage)。
