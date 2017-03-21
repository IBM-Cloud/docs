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

# 使用 Watson Translator 套件
{: #openwhisk_catalog_watson_translator}

`/whisk.system/watson-translator` 套件提供一種簡便的方式來呼叫要翻譯的 Watson API。

該套件包含下列動作。

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | 套件 | username、password | 文字翻譯及語言識別的套件  |
| `/whisk.system/watson-translator/translator` | 動作 (action) | payload、translateFrom、translateTo、translateParam、username、password | 翻譯文字 |
| `/whisk.system/watson-translator/languageId` | 動作 (action) | payload、username、password | 識別語言 |

**附註**：已淘汰套件 `/whisk.system/watson`（包括動作 `/whisk.system/watson/translate` 及 `/whisk.system/watson/languageId`）。

## 在 Bluemix 中設定 Watson Translator 套件

如果您是從 Bluemix 使用 OpenWhisk，則 OpenWhisk 會自動建立 Bluemix Watson 服務實例的套件連結。

1. 在 Bluemix [儀表板](http://console.ng.Bluemix.net)中，建立 Watson Translator 服務實例。
  
  請務必記住服務實例的名稱，以及您所在的 Bluemix 組織及空間。
  
2. 重新整理名稱空間中的套件。重新整理會自動建立您所建立之 Watson 服務實例的套件連結。
  
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
  
  
## 在 Bluemix 外部設定 Watson Translator 套件

如果您不是在 Bluemix 中使用 OpenWhisk，或者要在 Bluemix 外部設定 Watson Translator，則必須手動建立 Watson Translator 服務的套件連結。您需要 Watson Translator 服務使用者名稱及密碼。

- 建立針對 Watson Translator 服務所配置的套件連結。

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


## 翻譯文字

`/whisk.system/watson-translator/translator` 動作會將文字從某種語言翻譯成另一種語言。參數如下所示：

- `username`：Watson API 使用者名稱。
- `password`：Watson API 密碼。
- `payload`：要翻譯的文字。
- `translateParam`：指出要翻譯的文字的輸入參數。例如，如果 `translateParam=payload`，則會翻譯傳遞給動作的 `payload` 參數值。
- `translateFrom`：兩位數的來源語言代碼。
- `translateTo`：兩位數的目標語言代碼。

- 在套件連結中呼叫 `translator` 動作，以將某串文字從英文翻譯成法文。
  
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
  
  
## 識別某串文字的語言

`/whisk.system/watson-translator/languageId` 動作識別某串文字的語言。參數如下所示：

- `username`：Watson API 使用者名稱。
- `password`：Watson API 密碼。
- `payload`：要識別的文字。

- 在套件連結中呼叫 `languageId` 動作，以識別語言。
  
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
  
