---

copyright:
  years: 2017
lastupdated: "2017-03-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with Natural Language Understanding
{: #natural-language-understanding}

With {{site.data.keyword.nlushort}}, developers can analyze semantic features of unstructured text to extract structured insights. The service returns information for categories, concepts, emotion, entities, keywords, metadata, relations, semantic roles, and sentiment.
{:shortdesc}

Follow these steps to get started with {{site.data.keyword.nlushort}}.

## Create a service instance

Go to the [{{site.data.keyword.nlushort}}](https://console.ng.bluemix.net/catalog/services/natural-language-understanding) page in the service catalog, log in to Bluemix, and click **Create**.

To view your service credentials, go to your [list of services](https://console.{DomainName}/dashboard/services/) and click the service instance you created. From your service instance page, click the "Service Credentials" tab, then click **View Credentials** to view your username and password.

## Make a request to the API

To get started with one of the Watson Developer Cloud SDKs, view the SDK repositories for installation instructions and example usage:

* [Node.js ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/node-sdk)
* [Python ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/python-sdk)
* [Swift ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/swift-sdk)

The following example shows how to call the API from a command line with curl. Copy the following example parameters object into a new file called `parameters.json`. This sample configuration instructs the service to analyze **concepts** and **sentiment**, and limits the number of concepts results to three.

```json
{
  "text": "Natural Language Understanding analyzes unstructured text to return structured insights",
  "features": {
    "concepts": {
      "limit": 3
    },
    "sentiment": {}
  }
}
```
{: codeblock}

Open a command prompt or terminal, and send a request to the API using the settings from the *parameters.json* file you created. Replace *username* and *password* with your service credentials.

```bash
curl -X POST -u "username":"password" -d @parameters.json https://gateway.watsonplatform.net/natural-language-understanding/api/v1/analyze
```
{: codeblock}

To specify different features and options, or process different input such as HTML or a public URL, just change your
`parameters.json` file. Here is an example that analyzes emotion and sentiment for each entity that is found on the IBM website:

```json
{
  "url": "www.ibm.com",
  "features": {
    "entities": {
      "emotion": true,
      "sentiment": true
    }
  }
}
```
{: codeblock}

To learn more about the API and see more examples, check out the [API reference![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/natural-language-understanding/api/v1/) and view the [external documentation![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/doc/natural-language-understanding/).


# Related Links
{: #rellinks notoc}

## Related Links
{: #general}
* [Documentation![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/doc/natural-language-understanding){:new_window}
* [{{site.data.keyword.nlushort}} home page![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/natural-language-understanding.html){:new_window}
* [Watson Developer Cloud Community![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/watson){:new_window}

## API Reference
{: #api}
* [API reference![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/natural-language-understanding/api/v1/){:new_window}

## Tutorials and Samples
{: #samples}
* [Live Demo![External link icon](../../icons/launch-glyph.svg "External link icon")](https://natural-language-understanding-demo.mybluemix.net){:new_window}
* [Sample application and instructions![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/natural-language-understanding-nodejs){:new_window}

## SDKs
{: #sdk}
* [Node.js![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/node-sdk){:new_window}
* [Python![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/python-sdk){:new_window}
* [Swift![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/watson-developer-cloud/swift-sdk){:new_window}
