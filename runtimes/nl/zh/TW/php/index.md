---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}
*前次更新：2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} 上的 PHP 執行時期是採用 php_buildpack 技術。
php_buildpack 為 PHP 應用程式提供完整的執行時期環境。
{: shortdesc}

在下列狀況下將使用 php_buildpack：
* 應用程式包含 composer.json 檔案，或是
* 應用程式包含 *.php 檔案，或是
* 應用程式在其 [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) 檔案中定義了 ${WEBDIR} 變數，且該變數是設為應用程式內的現有目錄。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 PHP 入門範本應用程式。PHP 入門範本應用程式是簡單的 PHP 應用程式，提供可以讓您用於應用程式的範本。您可以用入門範本應用程式進行實驗，並進行及推送對 {{site.data.keyword.Bluemix}} 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 執行時期版本
{: #runtime_versions}

您可以在 composer.json 檔案中指定應用程式要使用的 PHP 版本。例如：

```
{
    "version": "1.5"
}
```
{: codeblock}
如需相關資訊，請參閱 [Composer Platform packages](https://getcomposer.org/doc/02-libraries.md#platform-packages)。

如果未指定版本，依預設會選擇 5.5.30 版。

### 可用的版本：
{: #available_versions}

目前安裝在 {{site.data.keyword.Bluemix}} 中的 [PHP 建置套件](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5)提供下列 PHP 版本：

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.14

如果您的應用程式需要未列出的 PHP 版本，您可以使用外部 [PHP 建置套件](https://github.com/cloudfoundry/php-buildpack.git)來部署該應用程式。

# 相關鏈結
## 範例
* [Build and deploy a REST API on IBM Bluemix with PHP and MySQL](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Build and deploy a mobile-friendly calorie counter on IBM Bluemix with PHP, MySQL, AngularJS, and the Nutritionix API](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## 一般
* [A Cloud Foundry Buildpack for PHP](https://github.com/cloudfoundry/php-buildpack.git)
