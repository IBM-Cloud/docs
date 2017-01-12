---

copyright:
  years: 2017
lastupdated: "2017-01-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.Bluemix}} CLI SDK plug-in
{: #sdk-cli}

{{site.data.keyword.Bluemix_notm}} users can use this plug-in to generate SDKs from their Swagger documents. Users can also see whether their Cloud Foundry (CF) apps in a given space are valid, and choose to generate an SDK from a CF app that is hosting Swagger docs. Finally, users can use the {{site.data.keyword.Bluemix_notm}} CLI plug-in to validate their Swagger docs to ensure that they comply with the SDK generator requirements.


## Requirements
{: #prereqs}

Ensure that you satisfy the following requirements.

* A [{{site.data.keyword.Bluemix_notm}}](http://bluemix.net) account
* [Swagger](http://swagger.io/) documentation for your API


## Installation
{: #installation}

1. Install the [{{site.data.keyword.Bluemix}} CLI](http://clis.ng.bluemix.net/ui/home.html).

2. Download the latest [SDK Gen plug-in](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins).
   
   1. Extract the downloaded file.

   2. Open your Terminal and navigate to the directory where you extracted the downloaded file.
   
      1. Run the following command to change the file permissions.

         ```
         sudo chmod 755 mobile-sdk-bx-<os>-<architecture>-<version>
         ```
         {: codeblock}
   
      2. Run the following command to install the plug-in.

         ```
         bluemix plugin install mobile-sdk-bx-<os>-<architecture>-<version>
         ```
         {: codeblock}
         
         * Mac OS: `mobile-sdk-bx-darwin-amd64-<version>
         * Linux 386: `mobile-sdk-bx-linux-386-<version>`
         * Linux AMD64: `mobile-sdk-bx-linux-amd64-<version>`
         * Windows AMD64: `mobile-sdk-bx-windows-amd64-<version>`
         * Windows 386: `mobile-sdk-bx-windows-386-<version>`


## Commands
{: #commands}

Use the following commands to generate an SDK, validate Swagger docs, or list Cloud Foundry apps.


### Generating an SDK
{: #gen}

Use `bluemix sdk generate [arguments...] [command options]`.


#### Arguments
{: #gen-args}

* `APP_NAME` - the name of the Cloud Foundry app in your current space
* `SWAGGER_DOC_LOCATION` - a URL or a relative path to raw Swagger JSON or Yaml
* `GENERATED_SDK_NAME` (optional) - the name of the generated SDK
* `DOWNLOAD_LOCATION` - relative path to where the SDK will extract (overwrites if existing SDK is present)


#### Options
{: #gen-options}

* `PLATFORM` (required)
   * `--android` - generate an Android SDK
   * `--swift` - generate a Swift SDK for iOS apps
* `--output "YOUR_RELATIVE_PATH"` (optional) - generates the SDK and downloads it in the directory that is specified by `YOUR_RELATIVE_PATH` (overwrites if existing SDK is present)
* `--unzip` (optional) - extracts the generated SDK (overwrites if existing SDK artifacts are present)


#### Usage
{: #gen-usage}

To generate an SDK from a Cloud Foundry app that is running in {{site.data.keyword.Bluemix_notm}}, you can use the app's name as a parameter to the CLI. The following command uses the app's name as the `SDK_Name`.

```
bluemix sdk generate [APP_NAME] [PLATFORM]
```
{: codeblock}

To generate an SDK from the URL to Swagger documentation or a local Swagger JSON or Yaml file, use the following command.

```
bluemix sdk generate [SWAGGER_DOC_LOCATION] [SDK_Name] [Platform]
```
{: codeblock}


### Validating Swagger docs
{: #validating}

Use `bluemix sdk validate [argument]`.


#### Arguments
{: #val-args}

* `APP_NAME` - the name of the Cloud Foundry app in your current space
* `SWAGGER_DOC_LOCATION` - a URL or a relative path to raw Swagger JSON or Yaml


#### Usage
{: #val-usage}

To validate a Cloud Foundry app's Swagger doc that is running in {{site.data.keyword.Bluemix_notm}}, you can use the app's name as a parameter to the CLI.

```
bluemix sdk validate [APP_NAME]
```
{: codeblock}
      
To validate an SDK from the URL to Swagger documentation or a local Swagger JSON or Yaml file, use the following command.

```
bluemix sdk validate [SWAGGER_DOC_LOCATION]
```
{: codeblock}



### List Apps (Cloud Foundry)
{: #list-apps}

Use `bluemix sdk list [argument] [option]` to list apps and validate Swagger docs. You must have the `OPENAPI_DEF` environment variable set to the Swagger docs path.


#### Arguments
{: #list-args}

* `SPACE_NAME` (optional) - the name of the Cloud Foundry space within your current organization that you want to search for apps. If not provided, the current space is searched.


#### Options
{: #list-options}

* `--url` (optional) - to display the URL of the Swagger docs


#### Usage
{: #list-usage}

To list apps in the current space, use the following command.

```
bluemix sdk list
```
{: codeblock}

To list apps in the current space and display the Swagger URL, use the following command.

```
bluemix sdk list --url
```
{: codeblock}

To list apps in a specific space, use the following command.

```
bluemix sdk list [SPACE_NAME]
```
{: codeblock}

To list apps in a specific space and display the Swagger URL, use the following command.

```
bluemix sdk list [SPACE_NAME] --url
```
{: codeblock}
