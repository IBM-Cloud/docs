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

{{site.data.keyword.Bluemix}} 上的 PHP 运行时由 php_buildpack 提供支持。php_buildpack 为 PHP 应用程序提供了一个完整的运行时环境。
{: shortdesc}

在以下情况下，将使用 php_buildpack：
* 您的应用程序包含 composer.json 文件，或者
* 您的应用程序包含 *.php 文件，或者
* 您的应用程序在其 [options.json](https://docs.cloudfoundry.org/buildpacks/php/gsg-php-config.html) 文件中定义了 ${WEBDIR} 变量，该变量设置为您应用程序内的一个现有目录。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供了 PHP 入门模板应用程序。PHP 入门模板应用程序是一个简单的 PHP 应用程序，它提供了一个可供您的应用程序使用的模板。您可以尝试使用该入门模板应用程序来进行更改并将更改推送到 {{site.data.keyword.Bluemix}} 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](/docs/cfapps/starter_app_usage.html)。

## 运行时版本
{: #runtime_versions}

您可以在 composer.json 文件中为您的应用程序指定要使用的 PHP 版本。例如：

```
{
    "require": {
        "php": "7.0.*"
    }
}
```
{: codeblock}
有关更多信息，请参阅 [Composer Package links ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://getcomposer.org/doc/04-schema.md#package-links)。
如果未指定版本，缺省情况下会选择 V5.5.34。

### 可用版本：
{: #available_versions}

{{site.data.keyword.Bluemix}} 中当前安装的 [PHP buildpack](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.3.10) 内提供了以下 PHP 版本：

* 5.5.33
* 5.5.34
* 5.6.19
* 5.6.20
* 7.0.4
* 7.0.5

如果您应用程序所需的 PHP 版本没有列在上述列表中，那么可以使用外部 [PHP buildpack](https://github.com/cloudfoundry/php-buildpack.git) 来部署应用程序。

# 相关链接
{: #rellinks notoc}
## 教程和样本
{: #samples notoc}
* [构建和部署 REST API](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [构建和部署移动友好的卡路里计数器](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## 常规
{: #general notoc}
* [用于 PHP 的 Cloud Foundry buildpack](https://github.com/cloudfoundry/php-buildpack.git)
