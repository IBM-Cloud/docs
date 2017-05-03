---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}

{{site.data.keyword.Bluemix}} の PHP ランタイムには php_buildpack が採用されています。
php_buildpack は、PHP アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

php_buildpack は、以下のいずれかの条件下で使用されます。
* アプリケーションに composer.json ファイルが含まれている。
* アプリケーションに *.php ファイルが含まれている。
* アプリケーションの [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) ファイルで ${WEBDIR} 変数が定義され、その変数がアプリケーション内の既存ディレクトリーに設定されている。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、PHP スターター・アプリケーションが用意されています。PHP スターター・アプリケーションは、アプリケーションで使用可能なテンプレートを提供する、シンプルな PHP アプリケーションです。スターター・アプリケーションを試し、{{site.data.keyword.Bluemix}} 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](/docs/cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

アプリケーションで使用する PHP のバージョンは、composer.json ファイルで変更できます。例えば、以下のように指定します。

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
詳しくは、[『Composer Package links』![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://getcomposer.org/doc/04-schema.md#package-links)を参照してください。
バージョンを指定しない場合は、デフォルトでバージョン 5.5.34 が選択されます。

### 使用可能なバージョン:
{: #available_versions}

現在 {{site.data.keyword.Bluemix}} にインストールされている [PHP ビルドパック](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.10)では、以下のバージョンの PHP が使用できます。

* 5.5.33
* 5.5.34
* 5.6.19
* 5.6.20
* 7.0.4
* 7.0.5

アプリケーションが、リストされていないバージョンの PHP を必要とする場合は、外部の [PHP ビルドパック](https://github.com/cloudfoundry/php-buildpack.git)を使用してアプリケーションをデプロイできます。

# 関連リンク
{: #rellinks notoc}
## チュートリアルおよびサンプル
{: #samples notoc}
* [Build and deploy a REST API on IBM Bluemix with PHP and MySQL](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Build and deploy a mobile-friendly calorie counter on IBM Bluemix with PHP, MySQL, AngularJS, and the Nutritionix API](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## 一般
{: #general notoc}
* [A Cloud Foundry Buildpack for PHP](https://github.com/cloudfoundry/php-buildpack.git)
