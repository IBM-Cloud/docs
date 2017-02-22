---

copyright:
  years: 2017
lastupdated: "2017-02-01"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Modern digital channel application architectures
{: #sdk-compute}

When you are building a cloud native digital channel application for mobile and Web, the best practice is to have a Backend for Frontend (BFF) that is either dedicated to your digital channel or offers the same data and logic integration support for both Web and mobile client apps. For more information about this architecture, see [Microservices for web and mobile ![External link icon](../icons/launch-glyph.svg)](https://www.ibm.com/devops/method/content/architecture/omnichannelArchitecture).

The following diagram shows an overview of the BFF architecture.

![BFF architecture](images/bff-arch.png)

Figure 1: BFF architecture

The concept of a BFF is to abstract away common business logic and integration logic from you microservices or high-value {{site.data.keyword.Bluemix}} cloud services.With this architecture, you can deploy and release updates to your mobile or Web application and deploy new versions of your BFF by using continous delivery pipelines with the dev ops service.

If you have one BFF for iOS and a separate BFF for Android, the engineering teams that are delivering the function for these apps are not constrained to release features by a centralized API release schedule. This is a common goal for microservice and digital channel architectures - to free the teams to release function and features often, without being tightly coupled to another team's release schedule.


## Backend for Frontends (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, really help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.


## Integrating a mobile client with a Backend for Frontend
{: #integration}

To enable easy integration between a mobile client and a BFF, {{site.data.keyword.Bluemix_notm}} supports mobile client SDK generation for iOS and Android in Swift and Java languages, respectively. To enable this feature, you must expose your BFF integration using an Open API specification (Swagger) document. This document can be in the form of JSON or YAML.

The client SDK generator uses the Open API definition file to define a client-optimized developer SDK that is easy to consume in your native mobile application. It will speed up your integration of your BFF into your mobile application.


## Defining an API
{: #definition}

The BFF needs to expose an API definition file that conforms to the Open API specification that is running on a live server endpoint. To enable the {{site.data.keyword.Bluemix_notm}} Developer Experience and the {{site.data.keyword.Bluemix_notm}} SDK CLI (Command Line Interface) to discover this endpoint, you must add an environment variable to your Cloud foundry application called `OPENAPI_SPEC`. This environment variable must reference the specification using a relative path.

To add the `OPENAPI_SPEC` environment variable in {{site.data.keyword.Bluemix_notm}}, follow these steps:

1. Log in to [{{site.data.keyword.Bluemix_notm}} ![External link icon](../icons/launch-glyph.svg)](http://bluemix.net).
2. Select a Cloud Foundry App.
3. Select **Runtime**.
4. Select **Environment variables**.
5. Click **Add** in the **User defined** section.
6. Specify `OPENAPI_SPEC` for **NAME** and a relative URL path to your Open API definition file.
7. Click **Save**.

<!--
To add the `OPENAPI_SPEC` environment variable locally and push your changes to {{site.data.keyword.Bluemix_notm}} with the [Cloud Foundry CLI ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli#getting-started), follow these steps:

1. Open Terminal and navigate to your project directory.
2. Add the following code to the `manifest.yml` file.

   ```
   env:
       "OPENAPI_SPEC": "<relative URL path to your Open API definition file>"
   ```
   {: codeblock}
3. Save your changes to the `manifest.yml` file.
4. Run `cf push` to deploy the changes to {{site.data.keyword.Bluemix_notm}}.
-->

For example:

```
OPENAPI_SPEC='/explorer/swagger.json'
```
{: codeblock}

{{site.data.keyword.apiconnect_long}} and Loopback application work particularly well using this approach. You can use Loopback and {{site.data.keyword.apiconnect_short}} to define a persistent model and expose the CRUD (Create, Read, Update, and Delete) operation using the Open API definition file.

You can also define business logic operations as well.


### Supported elements of Open API specification
{: #supported-elements notoc}

The only portion of the Open API specification that is not fully supported is the file structure. The specification allows for portions of the definition to be split into different files and referenced using the json `$ref` field. Your entire definition must be contained within one file.


## Example Backend for Frontend using Bluegen
{: #bff-bluegen}

{{site.data.keyword.Bluemix_notm}} has created a reference BFF using {{site.data.keyword.apiconnect_short}} and Strongloop, which maps a product model to a {{site.data.keyword.cloudant}} and an image API for referencing images in {{site.data.keyword.objectstorageshort}}.

You can use this BFF pattern to rapidly get started with provisioning a fully working BFF into {{site.data.keyword.Bluemix_notm}} and use it to help  understand how easy it is to integrate a BFF into a mobile project and generate native SDKs for iOS and Android in Swift and Java, respectively.

Follow the [README ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/backend-for-frontend-node) instructions for creating a project and installing it.


## Using Backend for Frontend with a Developer Experience project
{: #bff-devex}

The {{site.data.keyword.Bluemix_notm}} Mobile Developer Experience is designed to make it simple to define a mobile project with a number of cloud services associated. You can easily add [{{site.data.keyword.mobilepushshort}} ![External link icon](../icons/launch-glyph.svg)](/docs/services/mobilepush/index.html), [Analytics ![External link icon](../icons/launch-glyph.svg)](/docs/services/mobileanalytics/index.html), and Data or Storage services. 

The {{site.data.keyword.Bluemix_notm}} Mobile dashboard introduced the ability to integrate a BFF into a mobile project in the **Compute** page. You can add existing Compute service instances to your mobile project. After they are added, you can either generate a native SDK for your language choice or you can generate the full project and the SDK will be integrated into the source package of the project in the **Code** page. This is particularly useful when you are integrating with BFFs that are already well-defined.

After you have downloaded your project, you can open it with Xcode or Android Studio and compile your project with the client SDK.


## Using the CLI
{: #cli}

As you are developing your BFF, the API specification could change. To support these changes, you have the following two options.

* Regenerate the whole project into a new GitHub branch and merge the changes into your development branch.
* Regenerate the SDK directly by using the command-line (CLI) tool and update only the SDK part of the mobile project.

To use the CLI, you must [install](sdk_cli.html#installation) it.

Use the following command to list the actions that you can perform.

```
bluemix sdk
```
{: codeblock}

Use the following command to list the running Cloud Foundry instances in your current {{site.data.keyword.Bluemix_notm}} space.

```
bluemix sdk list
```
{: codeblock}

Each app is listed and the API is validated if the `OPENAPI_SPEC` environment variable is set. In the `VALID` column, you will see a green checkmark or a red `X`. A checkmark in the `VALID` column for the application means that a valid Open API definition is present. An `X` in the `VALID` column for the application means one of two things:

* an `OPENAPI_SPEC` environment variable is not defined for your application OR
* the API definition is not valid with respect to the Open API specification

Use the following command to view the fully-formed URL for the API. The fully-formed route and uri to the API specification is listed. You can view the raw specification in a browser, directly consume it in the CLI, or verify that the BFF `OPENAPI_SPEC` environment variable is set correctly.

```
bluemix sdk list --url
```
{: codeblock}

Use the following command to validate the Open API definition file of the `<AppName>` to determine if it can be used to generate an SDK. The command finds `<AppName>` in your current space and uses the relative path in the `OPENAPI_SPEC` environment variable to locate the specification for validation.

```
bluemix sdk validate <AppName>
```
{: codeblock}

Use the following command to generate an SDK for the native `<Platform>` of your choice and place a compressed file into your current working directory.

```
bluemix sdk generate <AppName> <SDKName> --<Platform>
```
{: codeblock}

Using the `--unzip` option will automatically extract the SDK into your current working directory. You can optionally specify the location to extract the SDK by using the `--output` option. You can manage your source code with GitHub and create a new branch specifically for updating the SDK. Using this approach makes it easier to view the changes and merge in the updated SDK to your development branch.


## Working with SDK generated models and APIs
{: #models-apis}

Now that your BFF is integrated into your mobile app using a generated SDK, you can start working with it. 

The SDK comes with fully generated documentation in the `docs` directory and the `source` directory. You can open the `README.html` file for a web view of the docs or open the `README.md` file for a Markdown view of the docs. The Markdown docs are useful when you are publishing the SDK into Cocoapods or Maven Central.

Within the documentation, you can see a list of APIs that are generated. You can click on the API to see a code snippet that you can directly paste into your mobile app.
