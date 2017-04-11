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

# 使用 Watson Text to Speech 套件
{: #openwhisk_catalog_watson_texttospeech}

`/whisk.system/watson-textToSpeech` 套件提供一種簡便的方式來呼叫要將文字轉換為語音的 Watson API。

該套件包含下列動作。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | 套件 | username、password | 將文字轉換為語音的套件 |
| `/whisk.system/watson-textToSpeech/textToSpeech` | 動作 (action) | payload、voice、accept、encoding、username、password | 將文字轉換為音訊 |

**附註**：已淘汰套件 `/whisk.system/watson`（包括動作 `/whisk.system/watson/textToSpeech`）。

## 在 Bluemix 中設定 Watson Text to Speech 套件

如果您是從 Bluemix 使用 OpenWhisk，則 OpenWhisk 會自動建立 Bluemix Watson 服務實例的套件連結。

1. 在 Bluemix [儀表板](http://console.ng.Bluemix.net)中，建立 Watson Text to Speech 服務實例。
  
  請務必記住服務實例的名稱，以及您所在的 Bluemix 組織及空間。
  
2. 重新整理名稱空間中的套件。重新整理會自動建立您所建立之 Watson 服務實例的套件連結。
  
  ```
wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  ```
wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  
  
## 在 Bluemix 外部設定 Watson Text to Speech 套件

如果您不是在 Bluemix 中使用 OpenWhisk，或者要在 Bluemix 外部設定 Watson Text to Speech，則必須手動建立 Watson Text to Speech 服務的套件連結。您需要 Watson Text to Speech 服務使用者名稱及密碼。

- 建立針對 Watson Speech to Text 服務所配置的套件連結。
  
  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}
  

## 將某串文字轉換為語音

`/whisk.system/watson-speechToText/textToSpeech` 動作會將某串文字轉換為音訊語音。參數如下所示：

- `username`：Watson API 使用者名稱。
- `password`：Watson API 密碼。
- `payload`：要轉換為語音的文字。
- `voice`：說話者的聲音。
- `accept`：語音檔的格式。
- `encoding`：語音二進位資料的編碼。


- 在套件連結中呼叫 `textToSpeech` 動作，以轉換文字。
  
  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```json
  {
        "payload": "<base64 encoding of a .wav file>"
  }
  ```
  
