---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# {{site.data.keyword.GlobalizationPipeline_full}}入門
{: #globalizationpipeline}

*最終更新日: 2016 年 7 月 6 日*
{: .last-updated}

{{site.data.keyword.GlobalizationPipeline_full}}は、Web またはモバイル UI を素早く翻訳できるように機械翻訳機能や編集機能を提供するサービスです。備えられているダッシュボード、RESTful API、アプリのデリバリー・パイプラインとの統合機能を利用して、アプリのビルドやデプロイをやり直すことなく世界中のお客様にリリースすることができます。
{:shortdesc}

{{site.data.keyword.GlobalizationPipeline_full}}のサービスは、{{site.data.keyword.Bluemix}} のアプリに使用することも、バインドせずに単独で使用することもできます。DevOps 環境を離れることなく、最小限の努力で、素早く翻訳を作成、保守、修正できます。

{{site.data.keyword.GlobalizationPipeline_full}}のインターフェースから、{{site.data.keyword.Bluemix_notm}} アプリを素早く翻訳することができます。RESTful API を使用してアプリを翻訳する方法については、[API リファレンス](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}を参照してください。 


## バンドルの作成
{: #globalizationpipeline_creatingbundles}

{{site.data.keyword.GlobalizationPipeline_full}}のサービスを使用して、バンドルを作成できます。バンドルには、翻訳対象のアプリのリソース・ファイルが含められます。リソース・ファイルとしては、Java プロパティー、AMD I18N、JSON ファイルを使用できます。このファイルには、アプリの UI 文字列を表すキー/値ペアの形式の内容が含まれていなければなりません。サポートされるファイル・タイプの詳細と例については、[バンドルの操作](./bundles.html){: new_window}を参照してください。

バンドルを作成するには、以下の手順を実行します。

1\. **「概要」**タブから、**「新しいバンドル (New Bundle)」**をクリックします。

2\. バンドルに関する情報を指定します。

| フィールド | 必須| 説明|
|-------|---------|------------|
| **バンドル ID (Bundle ID)** | Yes | バンドルを識別する固有の名前。 |
| **ソース言語 (Source language)** | Yes | ソース・ファイルのネイティブ言語。 |
| **リソース・ファイル (Resource File)** | No | 翻訳する[リソース・ファイル](bundles.html#globalizationpipeline_workingwithbundles)。最大ファイル・サイズは 2 MB に制限されます。指定されたリソース・ファイルがアップロードされます。  |
| **ファイル形式 (File format)** | No | アップロードするファイル・タイプ。 |
| **ターゲット言語 (Target language)** | No | 翻訳後の言語。 |

**注:** バンドルの機械翻訳を提供する言語サービスを変更するには、[**「MT 構成 (MT Configuration)」**](./managing_translations.html#globalizationpipeline_service_to_service)タブをクリックして、サポートされている他の機械翻訳エンジンを表示します。

3\. **「保存」**をクリックします。

バンドルを作成すると、アップロードしたリソース・ファイルが、指定したすべてのターゲット言語に翻訳されます。新しいバンドルが「バンドル」タブに追加されます。ここで、次の操作を実行できます。

* 言語を追加または除去する
* 生成された翻訳を編集する
* バンドルで使用されているソース・ファイルを更新し、翻訳を再生成する

## 翻訳後のバンドルをサービスにインポートする
{: #globalizationpipeline_importtranslatedbundlesintoservice}

あるいは、翻訳済みのリソース・ファイルが既に存在する場合は、それらを新しいバンドルにインポートすることもできます。詳しくは、[Java Client Tools for {{site.data.keyword.GlobalizationPipeline_full}}](https://github.com/IBM-Bluemix/gp-java-tools) を参照してください。

**注:** 元のソース・ファイルが更新された場合、ファイルの中で定義されているキーと値が、ソース・ファイルの最新バージョンと同期され、変更されたキーと値だけが翻訳されます。

## {{site.data.keyword.GlobalizationPipeline_full}}のデータ使用量の見積もり
{: #globalizationpipeline_documentpricing}

{{site.data.keyword.GlobalizationPipeline_full}}は、ユーザーの翻訳をバックエンド・データベースに格納します。アクティブ・データのサイズを見積もるには、以下の公式を使用します。

`<予期されるリソース・データのストレージ・サイズ (MB)> ˜= 0.0005 * <ソース・リソース中のキー/値ペアの数> * <ソース言語を含む言語の数>`

この公式では、典型的なバンドルのサイズは `(UTF-8 でのキーの長さ + 値の長さ = 40 バイト)` です。

例えば、100 個のキー/値ペアがあり、それらを 9 カ言語に翻訳する場合、ストレージ・サイズの見積もりは 0.0005 100 (9+1) = 0.5 MB になります。実際のサイズは、実際のキー/値のサイズや翻訳と共に保管されるメタデータに応じて異なります。

Bluemix の[料金カリキュレーター](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet&orgGuid=127a45f4-4461-4d5b-a26b-6dc2fdd1a3a2&spaceGuid=208fb1ff-413b-4fd9-9615-e8226062d0f3)を使用して、サービスの月額料金を計算してください。


# 関連リンク
{: #rellinks}
## チュートリアルとサンプル
{: #samples}

* [Node.js サンプル](https://github.com/IBM-Bluemix/gp-nodejs-sample){: new_window}
* [Ruby サンプル](https://github.com/IBM-Bluemix/gp-ruby-sample){: new_window}

## SDK
{: #sdk}

* [Java クライアント](https://github.com/IBM-Bluemix/gp-java-client){: new_window}
* [Java ツール](https://github.com/IBM-Bluemix/gp-java-tools){: new_window}
* [JavaScript クライアント](https://github.com/IBM-Bluemix/gp-js-client){: new_window}
* [AngularJS クライアント](https://github.com/IBM-Bluemix/gp-angular-client){: new_window}
* [Ruby クライアント](https://github.com/IBM-Bluemix/gp-ruby-client){: new_window}
* [Python クライアント](https://github.com/IBM-Bluemix/gp-python-client){: new_window}

## API リファレンス
{: #api}

* [IBM グローバリゼーション・パイプライン RESTful API](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}

## 関連リンク
{: #general}

* [グローバリゼーション・パイプラインをデリバリー・パイプラインに統合します。](https://hub.jazz.net/docs/deploy_ext/#globalize){: new_window}
* [IBM Bluemix の料金シート](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM Bluemix の前提条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
