---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 Watson Speech to Text 包
{: #openwhisk_catalog_watson_texttospeech}

通过 `/whisk.system/watson-speechToText` 包，可以方便地调用要将语音转换为文本的 Watson API。

此包中包含以下操作。

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | 包 | username 和 password | 用于将语音转换为文本的包 |
| `/whisk.system/watson-speechToText/speechToText` | 操作 | payload、content_type、encoding、username、password、continuous、inactivity_timeout、interim_results、keywords、keywords_threshold、max_alternatives、model、timestamps、watson-token、word_alternatives_threshold、word_confidence、X-Watson-Learning-Opt-Out | 将音频转换为文本 |

**注**：不推荐使用包含 `/whisk.system/watson/speechToText` 操作的 `/whisk.system/watson` 包。

## 在 Bluemix 中设置 Watson Speech to Text 包

如果是在 Bluemix 中使用 OpenWhisk，那么 OpenWhisk 将为 Bluemix Watson 服务实例自动创建包绑定。

1. 在 Bluemix [仪表板](http://console.ng.Bluemix.net)中创建 Watson Speech to Text 服务实例。
  
  确保记住服务实例的名称以及您所在的 Bluemix 组织和空间的名称。
  
2. 刷新名称空间中的包。刷新操作将自动为已创建的 Watson 服务实例创建包绑定。
  
  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_SpeechToText_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_SpeechToText_Credentials-1 private
  ```
  

## 在 Bluemix 外设置 Watson Speech to Text 包

如果不是在 Bluemix 中使用 OpenWhisk，或者如果要在 Bluemix 外部设置 Watson Speech to Text，那么必须为您的 Watson Speech to Text 服务手动创建包绑定。您需要 Watson Speech to Text 服务用户名和密码。

- 创建为您的 Watson Speech to Text 服务配置的包绑定。
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## 将语音转换为文本

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
  ```json
  {
        "data": "Hello Watson"
  }
  ```
  
