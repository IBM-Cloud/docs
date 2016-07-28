---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.graphfull}}
{: #gettingstartedtemplate}
Last updated: 27 July 2016
{: .last-updated}

{{site.data.keyword.graphfull}} is a fully managed graph database service,
accessible through a REST-based HTTP API interface.
Use it to build your mobile and web applications that require graph database capabilities.
{:shortdesc}

{{site.data.keyword.graphfull}} is based on the [Apache TinkerPop](http://tinkerpop.incubator.apache.org/)&trade;
stack, for building high-performance graph applications that use a v3 compatible API.
The stack gives you extra flexibility and capabilities based on a familiar environment.
Using the {{site.data.keyword.Bluemix}} dashboard,
you can integrate the {{site.data.keyword.graphfull}} service with your {{site.data.keyword.Bluemix_short}} applications easily.

You can work with {{site.data.keyword.graphfull}} in two ways:

*	Using the {{site.data.keyword.graphfull}} simplified API commands.
*	Using the full Apache TinkerPop v3 query language (Gremlin).

{{site.data.keyword.graphfull}} features are available as an API by using HTTP REST endpoints.
These endpoints provide an easy way for your applications to connect to and use the {{site.data.keyword.graphfull}} service,
by using HTTP to make API requests and obtain results.
Use the HTTP functions that are provided by your chosen application programming language to access the endpoints.
Alternatively you might use a command interface or a `curl` script to achieve the same effects.
The API Reference describes the various functions provided by the {{site.data.keyword.graphfull}} service,
along with examples of their use.

Your application can also use the Apache TinkerPop query language,
called Gremlin,
for tasks that use the {{site.data.keyword.graphfull}} service.
Include the Gremlin query in a JSON document,
then pass the document to the `/gremlin` service endpoint.
Examples of using Gremlin with {{site.data.keyword.graphfull}} are provided in the [full documentation](https://ibm-graph-docs.ng.bluemix.net/api.html).

Complete these steps to get started with the {{site.data.keyword.graphfull}} service:

1.	[Create an instance](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance) of the {{site.data.keyword.graphfull}} service.
2.	Record the three essential values generated when the instance is created. The values are available from the `Service Credentials` tab after clicking the service tile.
	*	The IBM Graph endpoint: `apiURL`.
	*	The service instance user name `username`.
	*	The service instance password `password`.
3.	Use the three essential values in your applications or scripts for {{site.data.keyword.graphfull}} tasks. Examples are provided in the [full documentation](https://ibm-graph-docs.ng.bluemix.net/api.html).

# Related Links
{: #rellinks}

## Tutorials and Samples
{: #samples}

* [Examples](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}

## API Reference
{: #api}

* [REST API for IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [Using Gremlin with IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## Related Links
{: #general}

* [Full documentation](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [Apache Tinkerpop](http://tinkerpop.incubator.apache.org/){:new_window}
