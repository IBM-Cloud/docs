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

# Using the Watson Translator package
{: #openwhisk_catalog_watson_translator}

The `/whisk.system/watson-translator` package offers a convenient way to call Watson APIs to translate.

The package includes the following actions.

| Entity | Type | Parameters | Description |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | package | username, password | Package for text translation and language identification  |
| `/whisk.system/watson-translator/translator` | action | payload, translateFrom, translateTo, translateParam, username, password | Translate text |
| `/whisk.system/watson-translator/languageId` | action | payload, username, password | Identify language |

**Note**: The package `/whisk.system/watson` is deprecated including the actions `/whisk.system/watson/translate` and `/whisk.system/watson/languageId`.

## Setting up the Watson Translator package in Bluemix

If you're using OpenWhisk from Bluemix, OpenWhisk automatically creates package bindings for your Bluemix Watson service instances.

1. Create a Watson Translator service instance in your Bluemix [dashboard](http://console.ng.Bluemix.net).
  
  Be sure to remember the name of the service instance and the Bluemix organization and space you're in.
  
2. Refresh the packages in your namespace. The refresh automatically creates a package binding for the Watson service instance that you created.
  
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
  
  
## Setting up a Watson Translator package outside Bluemix

If you're not using OpenWhisk in Bluemix or if you want to set up your Watson Translator outside of Bluemix, you must manually create a package binding for your Watson Translator service. You need the Watson Translator service user name, and password.

- Create a package binding that is configured for your Watson Translator service.

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


## Translating text

The `/whisk.system/watson-translator/translator` action translates text from one language to another. The parameters are as follows:

- `username`: The Watson API user name.
- `password`: The Watson API password.
- `payload`: The text to be translated.
- `translateParam`: The input parameter indicating the text to translate. For example, if `translateParam=payload`, then the value of the `payload` parameter that is passed to the action is translated.
- `translateFrom`: A two-digit code of the source language.
- `translateTo`: A two-digit code of the target language.

- Invoke the `translator` action in your package binding to translate some text from English to French.
  
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
  
  
## Identifying the language of some text

The `/whisk.system/watson-translator/languageId` action identifies the language of some text. The parameters are as follows:

- `username`: The Watson API user name.
- `password`: The Watson API password.
- `payload`: The text to identify.

- Invoke the `languageId` action in your package binding to identify the language.
  
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
  
