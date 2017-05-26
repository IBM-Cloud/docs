---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Watson Translator 包
{: #openwhisk_catalog_watson_translator}

通过 `/whisk.system/watson-translator` 包，可以方便地调用 Watson API 以进行翻译。

此包中包含以下操作。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | 包 | username 和 password | 用于文本翻译和语言识别的包  |
| `/whisk.system/watson-translator/translator` | 操作 | payload、translateFrom、translateTo、translateParam、username、password | 翻译文本 |
| `/whisk.system/watson-translator/languageId` | 操作 | payload、username 和 password | 识别语言 |

**注**：不推荐使用包含 `/whisk.system/watson/translate` 和 `/whisk.system/watson/languageId` 操作的 `/whisk.system/watson` 包。

## 在 Bluemix 中设置 Watson Translator 包

如果是在 Bluemix 中使用 OpenWhisk，那么 OpenWhisk 将为 Bluemix Watson 服务实例自动创建包绑定。

1. 在 Bluemix [仪表板](http://console.ng.Bluemix.net)中创建 Watson Translator 服务实例。
  
  确保记住服务实例的名称以及您所在的 Bluemix 组织和空间的名称。
  
2. 刷新名称空间中的包。刷新操作将自动为已创建的 Watson 服务实例创建包绑定。
  
  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  
  
## 在 Bluemix 外设置 Watson Translator 包

如果不是在 Bluemix 中使用 OpenWhisk，或者如果要在 Bluemix 外部设置 Watson Translator，那么必须为您的 Watson Translator 服务手动创建包绑定。您需要 Watson Translator 服务用户名和密码。

- 创建为您的 Watson Translator 服务配置的包绑定。

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


## 翻译文本

`/whisk.system/watson-translator/translator` 操作将文本从一种语言翻译为另一种语言。参数如下所示：

- `username`：Watson API 用户名。
- `password`：Watson API 密码。
- `payload`：要翻译的文本。
- `translateParam`：指示要翻译文本的输入参数。例如，如果 `translateParam=payload`，那么将翻译传递给该操作的 `payload` 参数的值。
- `translateFrom`：源语言的两位数代码。
- `translateTo`：目标语言的两位数代码。

- 调用包绑定中的 `translator` 操作，以将某些文本从英语翻译为法语。
  
  ```
  wsk action invoke myWatsonTranslator/translator \
  --blocking --result \
  --param payload "Blue skies ahead" --param translateFrom "en" \
  --param translateTo "fr"
  ```
  {: pre}
  ```json
  {
      "payload": "Ciel bleu a venir"
  }
  ```
  
  
## 识别某些文本的语言

`/whisk.system/watson-translator/languageId` 操作可识别某些文本的语言。参数如下所示：

- `username`：Watson API 用户名。
- `password`：Watson API 密码。
- `payload`：要识别的文本。

- 调用包绑定中的 `languageId` 操作来识别语言。
  
  ```
  wsk action invoke myWatsonTranslator/languageId \
  --blocking --result \
  --param payload "Ciel bleu a venir"
  ```
  {: pre}
  ```json
  {
    "payload": "Ciel bleu a venir",
    "language": "fr",
    "confidence": 0.710906
  }
  ```
  
