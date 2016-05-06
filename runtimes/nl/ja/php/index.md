---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}
*最終更新日時: 2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} の PHP ランタイムには php_buildpack が採用されています。
php_buildpack は、PHP アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

php_buildpack は、以下のいずれかの条件下で使用されます。
* アプリケーションに composer.json ファイルが含まれている。
* アプリケーションに *.php ファイルが含まれている。
* アプリケーションの [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) ファイルで ${WEBDIR} 変数が定義され、その変数がアプリケーション内の既存ディレクトリーに設定されている。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、PHP スターター・アプリケーションが用意されています。PHP スターター・アプリケーションは、アプリケーションで使用可能なテンプレートを提供する、シンプルな PHP アプリケーションです。スターター・アプリケーションを試し、 {site.data.keyword.Bluemix}} 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../../cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

アプリケーションで使用する PHP のバージョンは、composer.json ファイルで変更できます。例えば、以下のように指定します。

```
{
    "version": "1.5"
}
```
{: codeblock}
詳しくは、[『Composer Platform packages』](https://getcomposer.org/doc/02-libraries.md#platform-packages)を参照してください。

バージョンを指定しない場合は、デフォルトでバージョン 5.5.30 が選択されます。

### 使用可能なバージョン:
{: #available_versions}

現在 {{site.data.keyword.Bluemix}} にインストールされている [PHP ビルドパック](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5)では、以下のバージョンの PHP が使用できます。

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.14

アプリケーションが、リストされていないバージョンの PHP を必要とする場合は、外部の [PHP ビルドパック](https://github.com/cloudfoundry/php-buildpack.git)を使用してアプリケーションをデプロイできます。

# 関連リンク
## サンプル
* [Build and deploy a REST API on IBM Bluemix with PHP and MySQL](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Build and deploy a mobile-friendly calorie counter on IBM Bluemix with PHP, MySQL, AngularJS, and the Nutritionix API](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## 一般
* [A Cloud Foundry Buildpack for PHP](https://github.com/cloudfoundry/php-buildpack.git)
