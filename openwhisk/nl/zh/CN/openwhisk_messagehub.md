---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Message Hub 包
{: #openwhisk_catalog_message_hub}

通过此包，您可与 [Message Hub](https://developer.ibm.com/messaging/message-hub) 实例进行通信，以借助本机高性能 Kafka API 来使用消息。
{: shortdesc}

## 创建用于侦听 IBM Message Hub 实例的触发器
{: #openwhisk_catalog_message_hub_trigger}

为了创建用于在消息发布到 Message Hub 实例时做出反应的触发器，您需要使用名为 `/messaging/messageHubFeed` 的订阅源。此订阅源操作支持以下参数：

|名称|类型|描述|
|---|---|---|
|kafka_brokers_sasl|字符串的 JSON 数组|此参数是 `<host>:<port>` 字符串的数组，字符串中包含 Message Hub 实例中的代理程序|
|user|字符串|您的 Message Hub 用户名|
|password|字符串|您的 Message Hub 密码|
|topic|字符串|希望触发器侦听的主题|
|kafka_admin_url|URL 字符串|Message Hub Admin REST 接口的 URL|
|isJSONData|布尔值（可选 - 缺省值为 false）|设置为 `true` 时，提供程序在将消息值作为触发器有效内容传递之前，会先尝试将其解析为 JSON。|


此参数列表可能看起来让人望而生畏，但可以使用包刷新 CLI 命令自动设置这些参数：

1. 在正用于 OpenWhisk 的当前组织和空间下创建 Message Hub 服务实例。
  
2. 验证要侦听的主题在 Message Hub 中是否已存在，或者创建新主题，例如 `mytopic`。
  
3. 刷新名称空间中的包。刷新操作将自动为已创建的 Message Hub 服务实例创建包绑定。
  
  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```
  
  现在，包绑定包含与 Message Hub 实例关联的凭证。

4. 现在，您只需创建将在新消息发布到 Message Hub 主题时触发的触发器即可。
  
  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

## 在 Bluemix 外设置 Message Hub 包

如果要在 Bluemix 外部设置 Message Hub，那么必须为 Message Hub 服务手动创建包绑定。您需要 Message Hub 服务凭证和连接信息。

1. 创建为 Message Hub 服务配置的包绑定。
  
  ```
  wsk package bind /whisk.system/messaging myMessageHub -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443
  ```
  
2. 现在，您可以使用新包创建将在新消息发布到 Message Hub 主题时触发的触发器。
  
  ```
  wsk trigger create MyMessageHubTrigger -f myMessageHub/messageHubFeed -p topic mytopic -p isJSONData true
  ```
  {: pre}
  

## 侦听消息
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

```json
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

```json
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

## 消息将批量处理
您会注意到触发器有效内容包含消息数组。这意味着如果向消息传递系统生成消息的速度非常快，订阅源将尝试在单次触发触发器时对发布的消息进行批量处理。这将允许消息更快速、更高效地发布到触发器。

请记住，对触发器所触发的操作编写代码时，有效内容中的消息数在技术上是无限的，但始终会大于 0。下面是批量消息的示例（请注意 *offset* 值的变化）：
 
 ```json
 {
   "messages": [
    {
      "partition": 0,
         "key": null,
         "offset": 100,
         "topic": "mytopic",
         "value": {
             "amount": 5
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 101,
         "topic": "mytopic",
         "value": {
             "amount": 1
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 102,
         "topic": "mytopic",
         "value": {
             "amount": 999
         }
       }
   ]
 }
 ```
