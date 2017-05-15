---

copyright:
  years: 2015, 2017
lastupdated: "2016-09-9"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Getting started with {{site.data.keyword.GlobalizationPipeline_short}}
{: #globalizationpipeline}

{{site.data.keyword.GlobalizationPipeline_full}} is a service that provides machine translation and editing capabilities for rapidly translating web or mobile UIs. With its dashboard, RESTful API, and integration with your app's delivery pipeline, you can release to global customers without having to rebuild or re-deploy your app.
{:shortdesc}

You can use the {{site.data.keyword.GlobalizationPipeline_short}} service with any app in {{site.data.keyword.Bluemix}}, or unbound, by itself. You can create, maintain, and revise translations rapidly, with minimal effort and without having to leave your DevOps environment.

From the {{site.data.keyword.GlobalizationPipeline_short}} interface, you can quickly translate your {{site.data.keyword.Bluemix_notm}} apps. For information about translating your apps by using the RESTful API, see [API Reference](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}. 


## Creating a bundle
{: #globalizationpipeline_creatingbundles}

With the {{site.data.keyword.GlobalizationPipeline_short}} service, you can create bundles, which include the resource files of your apps that will be translated. The resource files can be either Java Properties, AMD I18N, or JSON files and must contain content in the form of key/value pairs that represent the UI strings from your app.  For more details and examples of supported file types, see [Working with bundles](./bundles.html){: new_window}.

To create a bundle, complete the following steps:

<ol>
<li>From the <strong>Overview</strong> tab, click <strong>New Bundle</strong>.</li>

<li>Provide information about your bundle:</li>
<table>
<thead>
<tr>
<th>Field</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Bundle ID</strong></td>
<td>Yes</td>
<td>A unique name to identify the bundle.</td>
</tr>
<tr>
<td><strong>Source language</strong></td>
<td>Yes</td>
<td>The native language of the source file.</td>
</tr>
<tr>
<td><strong>Resource File</strong></td>
<td>No</td>
<td>A <a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/bundles.html>resource file</a> to translate. The maximum file size is limited to 2MB. Specified resource files will be uploaded.</td>
</tr>
<tr>
<td><strong>File format</strong></td>
<td>No</td>
<td>The file type that is being uploaded.</td>
</tr>
<tr>
<td><strong>Target language</strong></td>
<td>No</td>
<td>The languages that you want translations for.</td>
</tr>
</tbody>
</table>

<p><strong>Note:</strong> To change the language service that provides machine translation for your bundles, click the <a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/managing_translations.html#globalizationpipeline_service_to_service>MT Configuration</a> tab to view other supported machine translation engines.</p>

<li>Click <strong>save</strong></li></ol>


After the bundle is created, the uploaded resource file is translated into all of the target languages that you specified. The new bundle is added to the Bundles tab where you can:

* Add or remove languages
* Edit the generated translations
* Update the source file that is used in the bundle and regenerate the translations

## Importing translated bundles
{: #globalizationpipeline_importtranslatedbundlesintoservice}

Alternatively, if you already have translated resource files, you can import them to a new bundle. For more information see [Java Client Tools for {{site.data.keyword.GlobalizationPipeline_short}}](https://github.com/IBM-Bluemix/gp-java-tools).

**Note:**  If the original source file is updated, the keys and values that are defined in the file are synchronized with the most recent version of the source file so that only the changed keys and values are translated.

## Estimating {{site.data.keyword.GlobalizationPipeline_short}} Data Usage
{: #globalizationpipeline_documentpricing}

{{site.data.keyword.GlobalizationPipeline_short}} stores your translations in a backend database. To estimate active data size, you can refer to the data storage estimation formula:

`<expected resource data storage size in MB> ˜= 0.0005 * <number of key/value pairs in the source resource> * <number of languages including the source language>`

According to the formula, the size of a typical bundle is `(length of key + length of value in UTF-8 = ˜40 bytes)`.

For example, if you have 100 key/value pairs and translate them to 9 languages, the estimated storage size is 0.0005 100 (9+1) = 0.5 MB. The actual size may be different depending on actual key/value size and metadata stored along with the translation.

Use the Bluemix [pricing calculator](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet&orgGuid=127a45f4-4461-4d5b-a26b-6dc2fdd1a3a2&spaceGuid=208fb1ff-413b-4fd9-9615-e8226062d0f3) to determine your monthly service costs.


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

* [IBM Globalization Pipeline RESTful API](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}

## Related Links
{: #general}

* [Integrate Globalization Pipeline with Delivery Pipeline](https://hub.jazz.net/docs/deploy_ext/#globalize){: new_window}
* [IBM Bluemix Pricing Sheet](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
