---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# SDK Generator Plug-in
{: #sdk-cli}

The {{site.data.keyword.IBM}} SDK Generator plug-in can be installed in the [{{site.data.keyword.Bluemix_notm}} CLI ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/cli/reference/bluemix_cli/index.html).

As a developer on {{site.data.keyword.Bluemix_notm}}, you can use this plug-in to generate SDKs from your [Open API Specification ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.openapis.org/) compliant REST API definition. As you make changes to your REST API definition, you can use this plug-in to regenerate only the SDK instead of regenerating the entire project.

You can also see if your Cloud Foundry apps in a given space have REST API definitions that are valid for SDK generation. Finally, you can use the {{site.data.keyword.IBM_notm}} SDK Generator plug-in to validate any REST API definitions to ensure that they comply with the SDK generator requirements.

This {{site.data.keyword.IBM_notm}} SDK Generator plug-in allows you to easily integrate your backend services to your app with a generated SDK. When a change to a REST API occurs, you can re-generate the SDK and replace the old one for a seamless SDK upgrade. You can also integrate the CLI into a devops pipeline and ensure that the SDK is always consistent with the API spec each time the app is built.

The REST API definition must be valid and either hosted on a live server endpoint or a local file on your system. If the REST API definition is hosted, the relative URL must be defined in the `OPENAPI_SPEC` environment variable.


## Requirements
{: #prereqs}

Ensure that you satisfy the following requirements.

* You have a [{{site.data.keyword.Bluemix_notm}} ![External link icon](../icons/launch-glyph.svg "External link icon")](http://bluemix.net) account
* A valid API definition that conforms to the [Open API ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.openapis.org/) specification


## Installation
{: #installation}

1. [Install the {{site.data.keyword.Bluemix}} CLI ![External link icon](../icons/launch-glyph.svg "External link icon")](http://clis.ng.bluemix.net/ui/home.html).

2. [Install the plug-in ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in).

	```
	bx plugin install sdk-gen -r Bluemix
	```
	{: codeblock}


## Commands
{: #commands}

Use the following commands to generate an SDK, validate Open API definition files, or list Cloud Foundry apps.


### Generating an SDK
{: #gen}

Use `bluemix sdk generate [arguments...] [command options]`.


#### Arguments
{: #gen-args}

* `APP_NAME` - the name of the Cloud Foundry app in your current space
* `OPENAPI_DOC_LOCATION` - a URL or a relative file path to the raw REST API definition JSON or Yaml
* `GENERATED_SDK_NAME` (optional) - the name of the generated SDK


#### Options
{: #gen-options}

* `PLATFORM` (required)
   * `--android` - generate an Android SDK
   * `--swift` - generate a Swift SDK for iOS apps
* `--output "YOUR_RELATIVE_PATH"` (optional) - places the generated SDK in the directory that is specified by `YOUR_RELATIVE_PATH` (overwrites if existing SDK is present)
* `--unzip` (optional) - extracts the generated SDK (overwrites if existing SDK artifacts are present)


#### Usage
{: #gen-usage}

To generate an SDK from a Cloud Foundry app that is running in {{site.data.keyword.Bluemix_notm}}, you can use the app's name as a parameter to the CLI. The following command uses the app's name as the `SDK_Name`.

```
bluemix sdk generate [APP_NAME] [PLATFORM]
```
{: codeblock}

To generate an SDK from a URL to an Open API definition file or a local JSON or Yaml file, use the following command.

```
bluemix sdk generate [OPENAPI_DOC_LOCATION] [SDK_Name] [Platform]
```
{: codeblock}


### Validating Open API definitions
{: #validating}

Use `bluemix sdk validate [argument]`.


#### Arguments
{: #val-args}

* `APP_NAME` - the name of the Cloud Foundry app in your current space
* `OPENAPI_DOC_LOCATION` - a URL or a relative file path to the raw REST API definition JSON or Yaml


#### Usage
{: #val-usage}

To validate a Cloud Foundry app's API spec that is running in {{site.data.keyword.Bluemix_notm}}, you can use the app's name as a parameter to the CLI.

```
bluemix sdk validate [APP_NAME]
```
{: codeblock}

To validate an SDK from the URL to an API spec document or a local JSON or Yaml file, use the following command.

```
bluemix sdk validate [OPENAPI_DOC_LOCATION]
```
{: codeblock}



### List Apps (Cloud Foundry)
{: #list-apps}

Use `bluemix sdk list [argument] [option]` to list apps and validate API specs. You must have the `OPENAPI_SPEC` environment variable set to relative url path hosting your spec.


#### Arguments
{: #list-args}

* `SPACE_NAME` (optional) - the name of the Cloud Foundry space within your current organization that you want to search for apps. If not provided, the current space is searched.


#### Options
{: #list-options}

* `--url` (optional) - to display a fully formed URL to the Open API definition for each app in the list


#### Usage
{: #list-usage}

To list apps in the current space, use the following command.

```
bluemix sdk list
```
{: codeblock}

To list apps in the current space and display the API spec URL, use the following command.

```
bluemix sdk list --url
```
{: codeblock}

To list apps in a specific space, use the following command.

```
bluemix sdk list [SPACE_NAME]
```
{: codeblock}

To list apps in a specific space and display the API spec URL, use the following command.

```
bluemix sdk list [SPACE_NAME] --url
```
{: codeblock}
