---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Getting started with {{site.data.keyword.GlobalizationPipeline_short}} (BETA)
{: #globalizationpipeline}

*Last updated: 25 March 2016*

{{site.data.keyword.GlobalizationPipeline_full}} is a service that provides machine translation and editing capabilities for rapidly translating web or mobile UIs. With its dashboard, RESTful API, and integration with your app's delivery pipeline, you can release to global customers without having to rebuild or re-deploy your app.
{:shortdesc}

You can use the {{site.data.keyword.GlobalizationPipeline_short}} service with any app in {{site.data.keyword.Bluemix}}, or unbound, by itself. You can create, maintain, and revise translations rapidly, with minimal effort and without having to leave your DevOps environment.

The {{site.data.keyword.GlobalizationPipeline_short}} service is a beta offering, and is provided as-is for development and experimentation purposes only. Capabilities will be added as the service continues to evolve.

From the {{site.data.keyword.GlobalizationPipeline_short}} interface, you can quickly translate your {{site.data.keyword.Bluemix_notm}} apps. For information about translating your apps by using the RESTful API, see the [API Reference](https://gp-beta-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}. 


## Creating a bundle
{: #globalizationpipeline_creatingbundles}

With the {{site.data.keyword.GlobalizationPipeline_short}} service, you can create bundles, which include the source files of your apps that will be translated. The source files can be either Java.properties, AMD I18N, or JSON files and must contain content in the form of key/value pairs that represent the UI strings from your app.  For more details and examples of supported file types, see [Working with bundles](bundles.html#globalizationpipeline_workingwithbundles).

To create a bundle, complete the following steps:

1\. From the **Overview** tab, click **New Bundle**.

2\. Provide information about your bundle:

| Field | Required| Description|
|-------|---------|------------|
| **Bundle ID** | Yes | A unique name to identify the bundle. |
| **Source language** | Yes | The native language of the source file. |
| **Resource File** | No | A [resource file](bundles.html#globalizationpipeline_workingwithbundles) to translate. You upload this file from your computer. |
| **File format** | No | The file type that is being uploaded. |
| **Target language** | No | The languages that you want translations for. |

3\. Click **Save**

After the bundle is created, the uploaded resource file is translated into all of the target languages that you specified. The new bundle is added to the Bundles tab where you can:

* Add or remove languages
* Edit the generated translations
* Update the source file that is used in the bundle and regenerate the translations

**Note** If the original source file is updated, the keys and values that are defined in the file are synchronized with the most recent version of the source file so that only the changed keys and values are translated.


# Related Links
{: #rellinks}
## Tutorials and Samples
{: #samples}

* [Node.js Sample](https://github.com/IBM-Bluemix/gp-nodejs-sample){: new_window}
* [Ruby Sample](https://github.com/IBM-Bluemix/gp-ruby-sample){: new_window}

## SDK
{: #sdk}

* [Java Client](https://github.com/IBM-Bluemix/gp-java-client){: new_window}
* [Java Tools](https://github.com/IBM-Bluemix/gp-java-tools){: new_window}
* [JavaScript Client](https://github.com/IBM-Bluemix/gp-js-client){: new_window}
* [AngularJS Client](https://github.com/IBM-Bluemix/gp-angular-client){: new_window}
* [Ruby Client](https://github.com/IBM-Bluemix/gp-ruby-client){: new_window}
* [Python Client](https://github.com/IBM-Bluemix/gp-python-client){: new_window}

## API Reference
{: #api}

* [IBM Globalization Pipeline RESTful API](https://gp-beta-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}

## Related Links
{: #general}

* [Integrate Globalization Pipeline with Delivery Pipeline](https://hub.jazz.net/docs/deploy_ext/#globalize){: new_window}
* [IBM Bluemix Pricing Sheet](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
