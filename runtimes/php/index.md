---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# PHP
{: #php_runtime}
*Last Updated: 10 June 2016*
{: .last-updated}

The PHP runtime on {{site.data.keyword.Bluemix}} is powered by the php_buildpack.
The php_buildpack provides a complete runtime environment for PHP
apps.
{: shortdesc}

The php_buildpack is used in the following conditions:
* Your app contains a composer.json file, or
* your app contains a *.php file, or
* your app defines a ${WEBDIR} variable in its [options.json](https://github.com/cloudfoundry/php-buildpack/blob/master/docs/config.md) file, and that variable is set to an existing directory within your app.

## Starter application
{: #starter_application}

{{site.data.keyword.Bluemix}} provides a PHP starter app.  The PHP starter application is a simple PHP app that provides a template that you can use for your app. You can experiment with the starter app, and make and push changes to the {site.data.keyword.Bluemix}}
environment.  See [Using the starter applications](../../cfapps/starter_app_usage.html) for help with using the starter app.

## Runtime versions
{: #runtime_versions}

You can specify the version of PHP to be used by your app in the composer.json file. For example:

```
{
    "require": {
        "php": "5.6.*"
    }
}
```
{: codeblock}
For more information, see [Composer Package links](https://getcomposer.org/doc/04-schema.md#package-links).

When a version is not specified, version 5.5.30 is chosen by default.

### Available versions:
{: #available_versions}

The following PHP versions are available in the
[PHP buildpack](https://github.com/cloudfoundry/php-buildpack/releases/tag/v4.1.5)
currently installed in {{site.data.keyword.Bluemix}}:

* 5.4.44
* 5.4.45
* 5.5.29
* 5.5.30
* 5.6.30
* 5.6.13
* 5.6.14

If your app requires a PHP version that is not listed,
you can use the external
[PHP buildpack](https://github.com/cloudfoundry/php-buildpack.git) to
deploy the app.

# rellinks
## samples
* [Build and deploy a REST API](http://www.ibm.com/developerworks/library/wa-deployrest-app/)
* [Build and deploy a mobile-friendly calorie counter](http://www.ibm.com/developerworks/library/mo-bluemix-php-nutritionix-angularjs/)
## general
* [Cloud Foundry buildpack for PHP](https://github.com/cloudfoundry/php-buildpack.git)
