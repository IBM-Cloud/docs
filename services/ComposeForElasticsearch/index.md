---

copyright:
  years: 2016
lastupdated: "2017-04-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with Compose for Elasticsearch
{: #getting-started-with-compose-for-elasticsearch}

{{site.data.keyword.composeForElasticsearch_full}} combines the power of a full text search engine with the indexing strengths of a JSON document database. Together they create a powerful tool for rich data analysis on large volumes of data. With Elasticsearch, your searching can be scored for exactness, letting you dig through your data set for those close matches and near misses that you might be missing.
{:shortdesc}

**Note:** Any Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com/](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your Bluemix account.

Complete these steps to get started with {{site.data.keyword.composeForElasticsearch}}:

1. [Create a {{site.data.keyword.composeForElasticsearch}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-elasticsearch/).

  When you create an instance of the service, ensure that you choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned. The various credential values are listed in the *Available credentials* section.

2. Connect to your {{site.data.keyword.composeForElasticsearch}} service.

  To connect an app to your service, use the credentials that are created along with the service. The sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForElasticsearch}} service.

  Download the [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) sample app and follow the instructions in the readme file. Then, in your application details page in Bluemix, click **View APP** to view the contents of the _examples_ index.

## Available credentials

Field Name|Description
----------|-----------
`uri`|The URI to be used when connecting to the service. Includes the schema (`https:`), admin user name and password, host name of server and port number to connect to.
`uri_direct_1`|An alternate URI that can be used when connecting to the service. Formatted as for `uri`.
`uri_health`|A `curl` command that requests the cluster health from the first haproxy.
`uri_health_1`|A `curl` command that requests the cluster health from the second haproxy.
`ca_certificate_base64`|A self-signed certificate that is used to confirm that an application is connecting to the appropriate server. This is base64 encoded. You need to decode the key before using it, as shown in the sample application.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by the service; in this case `elastic_search`.
`name`|The database deployment name.
{: caption="Table 1. {{site.data.keyword.composeForElasticsearch}} credentials" caption-side="top"}

**Note:** Two `haproxy` portals provide access to the Elasticsearch cluster. Both `uri` and `uri_direct_1` can be used to connect to the cluster. In your applications, switch between `uri` and `uri_direct_1` to manage responses to connection failures.
