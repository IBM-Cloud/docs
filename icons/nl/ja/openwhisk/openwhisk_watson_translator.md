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

# Watson Translator パッケージの使用
{: #openwhisk_catalog_watson_translator}

`/whisk.system/watson-translator` パッケージを利用して、変換するための Watson API を簡単に呼び出すことができます。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | パッケージ | username、password | テキスト翻訳および言語識別のパッケージ  |
| `/whisk.system/watson-translator/translator` | アクション | payload、translateFrom、translateTo、translateParam、username、password | テキストの変換 |
| `/whisk.system/watson-translator/languageId` | アクション | payload、username、password | 言語の識別 |

**注:** パッケージ `/whisk.system/watson` は、アクション `/whisk.system/watson/translate` および `/whisk.system/watson/languageId` を含め、非推奨です。

## Bluemix での Watson Translator パッケージのセットアップ

Bluemix から OpenWhisk を使用している場合、Bluemix Watson サービス・インスタンスのパッケージ・バインディングは OpenWhisk が自動的に作成します。

1. Bluemix [ダッシュボード](http://console.ng.Bluemix.net)で Watson Translator のサービス・インスタンスを作成します。
  
  サービス・インスタンスの名前、およびユーザーが所属している Bluemix の組織とスペースの名前を忘れないようにしてください。
  
2. 名前空間でパッケージを最新表示します。最新表示により、ユーザーが作成した Watson サービス・インスタンスのパッケージ・バインディングが自動的に作成されます。
  
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
  
  
## Bluemix 外部での Watson Translator パッケージのセットアップ

Bluemix で OpenWhisk を使用していない場合、または Bluemix の外部で Watson Translator をセットアップしたい場合は、Watson Translator サービスのパッケージ・バインディングを手動で作成する必要があります。Watson Translator サービスのユーザー名とパスワードが必要になります。

- Watson Translator サービス用に構成されるパッケージ・バインディングを作成します。

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


## テキストの変換

`/whisk.system/watson-translator/translator` アクションは、テキストをある言語から別の言語に変換します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `payload`: 変換するテキスト。
- `translateParam`: 変換するテキストを示す入力パラメーター。例えば、`translateParam=payload` の場合は、アクションに渡される `payload` パラメーターの値が変換されます。
- `translateFrom`: ソース言語の 2 桁のコード。
- `translateTo`: ターゲット言語の 2 桁のコード。

- パッケージ・バインディングの `translator` アクションを起動して、テキストを英語からフランス語に変換します。
  
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
  
  
## テキストの言語の識別

`/whisk.system/watson-translator/languageId` アクションは、テキストの言語を識別します。パラメーターは次のとおりです。


- `username`: Watson API ユーザー名。
- `password`: Watson API パスワード。
- `payload`: 識別するテキスト。

- パッケージ・バインディングの `languageId` アクションを起動して、言語を識別します。
  
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
  
