---

copyright:
  years: 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with IBM® Graph
{: #gettingstartedtemplate}
Last updated: 27 April 2017
{: .last-updated}

{{site.data.keyword.graphfull}} is a fully managed graph database service, accessible through the {{site.data.keyword.graphfull}} console in {{site.data.keyword.Bluemix_short}} or a REST-based HTTP API interface. Use it to build your mobile and web applications that require graph database capabilities. [Unfamiliar with graph databases?](https://developer.ibm.com/clouddataservices/docs/graph/)
{:shortdesc}

{{site.data.keyword.graphfull}} is based on the Apache TinkerPop&trade;, for building high-performance graph applications that use a V3 compatible API.
{{site.data.keyword.graphfull}} gives you extra flexibility and capabilities you won't find in the open source. The [API documentation](https://ibm-graph-docs.ng.bluemix.net/api.html) describes the various functions provided by the {{site.data.keyword.graphfull}} service, along with examples of their use.

Complete these steps to get started with the {{site.data.keyword.graphfull}} service:

1. To accesss {{site.data.keyword.graphfull}}, you need to have a {{site.data.keyword.Bluemix_short}} ID.  Using the {{site.data.keyword.Bluemix}} dashboard,
you can integrate the {{site.data.keyword.graphfull}} service with your {{site.data.keyword.Bluemix_short}} applications easily.
{{site.data.keyword.Bluemix_short}} is an open standards, cloud platform for building, running, and managing apps and services. {{site.data.keyword.Bluemix_short}} enables developers to rapidly build, deploy, and manage their cloud applications, while tapping a growing ecosystem of available services and run-time frameworks.

  - If you already have a {{site.data.keyword.Bluemix_short}} ID, log in and [create an instance](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance) of the {{site.data.keyword.graphfull}} service.

  - If you do not have a {{site.data.keyword.Bluemix_short}} ID, follow these steps:
    1. Register for a free {{site.data.keyword.Bluemix_short}} account: Follow the screens to fill out the registration form, confirm the account using the link sent to your email, and log in to Bluemix.
    2. Set up your {{site.data.keyword.Bluemix_short}} account: Follow the forms to create a new organization and space, and click on **I’m Ready**.
    3. Go directly to [{{site.data.keyword.graphfull}}]( https://console.ng.bluemix.net/catalog/services/ibm-graph/?cm_mc_uid=70214621144714763644460&cm_mc_sid_50200000=1476432359), or find it in the {{site.data.keyword.Bluemix_short}} catalog: Go to **Products** > **Data and analytics** > **{{site.data.keyword.graphfull}} service**.
2. Start working with {{site.data.keyword.graphfull}}: Provision a new {{site.data.keyword.graphfull}} instance by clicking **Create** using your {{site.data.keyword.Bluemix_short}} account and then click **Open** to open the {{site.data.keyword.graphfull}} console. The {{site.data.keyword.graphfull}} [API documentation](https://ibm-graph-docs.ng.bluemix.net/api.html) is available to help you connect from your command line.
3. Record the three essential values generated when the instance is created to connect your application to the service using a command interface. The values are available from the **Service Credentials** tab after clicking the service tile.
	*	The {{site.data.keyword.graphfull}} endpoint: `apiURL`.
	*	The service instance user name `username`.
	*	The service instance password `password`.

Use the three essential values in your applications or scripts for {{site.data.keyword.graphfull}} tasks. Examples are provided in the [API documentation](https://ibm-graph-docs.ng.bluemix.net/api.html).

You can work with {{site.data.keyword.graphfull}} in three ways:

* Using the {{site.data.keyword.graphfull}} console in {{site.data.keyword.Bluemix_short}}.

  The {{site.data.keyword.graphfull}} console helps first-time users to understand the value of {{site.data.keyword.graphfull}} and to get up and running with the service. Therefore, start working with the service through the {{site.data.keyword.graphfull}} console available through {{site.data.keyword.Bluemix_short}}. The console provides tutorials on graph databases, sample data and queries, and allows you to visualize your data.

*	Using the full [Apache TinkerPop](http://tinkerpop.incubator.apache.org/) query language (Gremlin) in your application.

  The API provides a `/gremlin` service endpoint, which is Apache TinkerPop query language, for tasks that use the {{site.data.keyword.graphfull}} service. Include the Gremlin query in a JSON document, then pass the document to the `/gremlin` service endpoint. Using Gremlin is the most common way to work with {{site.data.keyword.graphfull}}. It gives you the fastest performance, especially when executing more complex tasks. Examples of using Gremlin with {{site.data.keyword.graphfull}} are provided in the [API documentation](https://ibm-graph-docs.ng.bluemix.net/api.html).

*	Using the {{site.data.keyword.graphfull}} simplified [API commands](https://ibm-graph-docs.ng.bluemix.net/api.html).

  {{site.data.keyword.graphfull}} features are also available as an [API](https://ibm-graph-docs.ng.bluemix.net/api.html) by using HTTP REST endpoints. These endpoints provide an easy way for your applications to connect to and use the {{site.data.keyword.graphfull}} service, by using HTTP to make [API](https://ibm-graph-docs.ng.bluemix.net/api.html) requests and obtain results. Use the HTTP functions that are provided by your chosen application programming language to access the endpoints. Alternatively, you might use a command interface or a `curl` script to achieve the same effects. The [API documentation](https://ibm-graph-docs.ng.bluemix.net/api.html) describes the various functions provided by the {{site.data.keyword.graphfull}} service, along with examples of their use.




# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Examples](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}
* [Tutorial: Introducing {{site.data.keyword.graphfull}} Concepts](https://developer.ibm.com/clouddataservices/docs/graph/get-started#intro){:new_window}
* [How can I try out Graph databases](https://developer.ibm.com/clouddataservices/docs/graph/get-started#tryout){:new_window}

## API Reference
{: #api}

* [REST API for {{site.data.keyword.graphfull}}](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [Using Gremlin with {{site.data.keyword.graphfull}}](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## Related Links
{: #general}

* [Full documentation](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [{{site.data.keyword.graphfull}} Slack channel](http://ibm-graph-slackinvite.mybluemix.net/){:new_window}
* [{{site.data.keyword.graphfull}} Learning Center](https://developer.ibm.com/clouddataservices/docs/graph/){:new_window}
* [Apache TinkerPop](http://tinkerpop.incubator.apache.org/){:new_window}
