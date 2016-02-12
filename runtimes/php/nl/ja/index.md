{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*最終更新日: 2016 年 1 月 4 日*

# PHP ランタイム
{: #php_runtime}

{{site.data.keyword.Bluemix}} の PHP ランタイムでは、php_buildpack が採用されています。
php_buildpack は、PHP アプリのための完全なランタイム環境を提供します。
{: shortdesc}

php_buildpack は以下のいずれかの状況下において使用されます。
* ご使用のアプリに composer.json ファイルが含まれている。
* ご使用のアプリに *.php ファイルが含まれている。
* ご使用のアプリの [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) ファイル内で ${WEBDIR} 変数が定義されており、その変数が当該アプリ内の既存のディレクトリーに設定されている。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} は PHP スターター・アプリを提供します。PHP スターター・アプリケーションは、ご使用のアプリに使用できるテンプレートを提供するシンプルな PHP アプリです。このスターター・アプリを試し、{site.data.keyword.Bluemix}} 環境に変更を加えてプッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[「スターター・アプリケーションの使用 (Using the starter applications)」](../../cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

composer.json ファイルで、アプリが使用する PHP のバージョンを指定することができます。例えば、次のとおりです。

```
{
    "version": "1.5"
}
```
{: codeblock}
詳しくは、[Composer の
『Platform packages』](https://getcomposer.org/doc/02-libraries.md#platform-packages)を参照してください。

バージョンが指定されていない場合、デフォルトでバージョン 5.5.30 が選択されます。

### 使用可能なバージョン:
{: #available_versions}

{{site.data.keyword.Bluemix}} に現在インストールされている [PHP ビルドパック](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5)では、以下の PHP のバージョンを使用できます。

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.714

ご使用のアプリが必要とする PHP のバージョンがリストにない場合は、外部の
[PHP
ビルドパック](https://github.com/cloudfoundry/php-buildpack.git)を使用してアプリをデプロイできます。

## チュートリアルおよびサンプル
{: #tutorials_and_samples}
* [Build and deploy a REST API](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Build and deploy a mobile-friendly calorie counter ](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)

## 関連リンク
{: #related_links}
* [PHP 用 Cloud Foundry ビルドパック](https://github.com/cloudfoundry/php-buildpack.git)
