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

# 使用 Watson Speech to Text 套件
{: #openwhisk_catalog_watson_texttospeech}

`/whisk.system/watson-speechToText` 套件提供一種簡便的方式來呼叫要將語音轉換為文字的 Watson API。

該套件包含下列動作。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | 套件 | username、password | 將語音轉換為文字的套件 |
| `/whisk.system/watson-speechToText/speechToText` | 動作 | payload、content_type、encoding、username、password、continuous、inactivity_timeout、interim_results、keywords、keywords_threshold、max_alternatives、model、timestamps、watson-token、word_alternatives_threshold、word_confidence、X-Watson-Learning-Opt-Out | 將音訊轉換為文字 |

**附註**：已淘汰套件 `/whisk.system/watson`（包括動作 `/whisk.system/watson/speechToText`）。

## 在 Bluemix 中設定 Watson Speech to Text 套件

如果您是從 Bluemix 使用 OpenWhisk，則 OpenWhisk 會自動建立 Bluemix Watson 服務實例的套件連結。

1. 在 Bluemix [儀表板](http://console.ng.Bluemix.net)中，建立 Watson Speech to Text 服務實例。
  
  請務必記住服務實例的名稱，以及您所在的 Bluemix 組織及空間。
  
2. 重新整理名稱空間中的套件。重新整理會自動建立您所建立之 Watson 服務實例的套件連結。
  
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
  

## 在 Bluemix 外部設定 Watson Speech to Text 套件

如果您不是在 Bluemix 中使用 OpenWhisk，或者要在 Bluemix 外部設定 Watson Speech to Text，則必須手動建立 Watson Speech to Text 服務的套件連結。您需要 Watson Speech to Text 服務使用者名稱及密碼。

- 建立針對 Watson Speech to Text 服務所配置的套件連結。
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## 將語音轉換為文字

`/whisk.system/watson-speechToText/speechToText` 動作會將音訊語音轉換為文字。參數如下所示：

- `username`：Watson API 使用者名稱。
- `password`：Watson API 密碼。
- `payload`：要轉換為文字的已編碼語音二進位資料。
- `content_type`：音訊的 MIME 類型。
- `encoding`：語音二進位資料的編碼。
- `continuous`：指出是否傳回代表以長間歇分隔之連續詞組的多個最終結果。
- `inactivity_timeout`：時間（秒），如果在所提交的音訊中只偵測到靜音，將在此期限之後結束連線。
- `interim_results`：指出服務是否要傳回臨時結果。
- `keywords`：要在音訊中標示的關鍵字清單。
- `keywords_threshold`：信任值，其為標示關鍵字的下限。
- `max_alternatives`：要傳回之替代記錄的數目上限。
- `model`：要用於識別要求的模型 ID。
- `timestamps`：指出是否要為每個單字傳回時間校準。
- `watson-token`：提供服務的鑑別記號，以作為提供服務認證的替代方案。
- `word_alternatives_threshold`：信任值，其為將假設識別為可能替代字的下限。
- `word_confidence`：指出是否要為每個單字傳回範圍從 0 到 1 之間的信任測量值。
- `X-Watson-Learning-Opt-Out`：指出是否要拒絕呼叫的資料收集。
 

- 在套件連結中呼叫 `speechToText` 動作，以轉換已編碼的音訊。
  
  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
        "data": "Hello Watson"
  }
  ```
  
