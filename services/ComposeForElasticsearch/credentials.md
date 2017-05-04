---

copyright:
  years: 2016,2017
lastupdated: "2017-04-27"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Available Credentials
{: #available-credentials}

To connect an app to your service, use the credentials that are created along with the service. The [compose-elasticsearch-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-elasticsearch-helloworld-nodejs) sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForElasticsearch}} service using the credentials.

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
{: caption="Table 1. Compose for Elasticsearch credentials" caption-side="top"}

**Note:** Two `haproxy` portals provide access to the Elasticsearch cluster. Both `uri` and `uri_direct_1` can be used to connect to the cluster. In your applications, switch between `uri` and `uri_direct_1` to manage responses to connection failures.
