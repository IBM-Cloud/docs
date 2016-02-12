{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*前次更新：2016 年 1 月 4 日*

# PHP 執行時期
{: #php_runtime}

{{site.data.keyword.Bluemix}} 上的 PHP 執行時期採用 php_buildpack 技術。
php_buildpack 提供 PHP 應用程式的完整執行時期環境。
{: shortdesc}

在下列狀況下，會使用 php_buildpack：
* 您的應用程式包含 composer.json 檔案，或
* 您的應用程式包含 *.php 檔案，或
* 您的應用程式在其 [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) 檔案中定義 ${WEBDIR} 變數，而且該變數設為您應用程式內的現有目錄。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 PHP 入門範本應用程式。PHP 入門範本應用程式是一種簡單 PHP 應用程式，提供可用於應用程式的範本。您可以實驗入門範本應用程式，以及變更 {site.data.keyword.Bluemix}} 環境，並將變更推入其中。如需使用入門範本應用程式的說明，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 執行時期版本
{: #runtime_versions}

您可以在 composer.json 檔案中指定應用程式要使用的 PHP 版本。例如：

```
{
    "version": "1.5"
}
```
{: codeblock}
如需相關資訊，請參閱 [Composer
Platform packages](https://getcomposer.org/doc/02-libraries.md#platform-packages)。

未指定版本時，依預設會選擇 5.5.30 版。

### 可用的版本：
{: #available_versions}

目前安裝於 {{site.data.keyword.Bluemix}} 的 [PHP 建置套件](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5)提供下列 Python 版本：

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.714

如果您的應用程式需要未列出的 PHP 版本，可以使用外部 [PHP 建置套件](https://github.com/cloudfoundry/php-buildpack.git)來部署應用程式。

## 指導教學及範例
{: #tutorials_and_samples}
* [建置並部署 REST API](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [建置並部署手機可用的卡路里計算器](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)

## 相關鏈結
{: #related_links}
* [A CloudFoundry Build Pack for PHP](https://github.com/cloudfoundry/php-buildpack.git)
