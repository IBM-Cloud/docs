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

# Getting started with Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB is an in-place replacement for the Cassandra wide-column distributed database. ScyllaDB is written in C++, rather than Cassandra's Java, for better resource usage that can result in 10 times better performance in benchmarks. In addition to retaining compatibility with Cassandra tool and data files, ScyllaDB adds self-tuning capabilities. {{site.data.keyword.composeForScyllaDB_full}} extends the capabilities of ScyllaDB by managing it for you, offering an easy, auto-scaling deployment system that delivers high availability and redundancy, plus automated backups.
{:shortdesc}

**Note:** {{site.data.keyword.composeForScyllaDB_full}} does not give access to the Compose UI. See [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) for more details.

Complete these steps to get started with {{site.data.keyword.composeForScyllaDB}}:

1. [Create a {{site.data.keyword.composeForScyllaDB}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/).

   When you create an instance of the service, choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned. The various credential values are listed in the "Available credentials" section.

2. Connect to your {{site.data.keyword.composeForScyllaDB}} service.

   To connect an application to your service, use the credentials that are created along with the service.

   Download the [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) sample application and follow the instructions in the readme file. Then, on the application details page in the Bluemix console, click **View APP**.

   The sample application demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForScyllaDB}} service.


## Available credentials

Field Name|Description
----------|-----------
`db_type`|The type of database that is offered by the service, in this case `scylla`.
`uri_cli_1`|An alternative `cqlsh` shell command line that connects to the database instance.
`maps`|A ScyllaDB connection map that provides the information that is needed by various drivers to associate internal IP addresses with the external DNS names of a ScyllaDB database.
`name`|The database deployment name.
`uri_cli`|A `cqlsh` shell command line that connects to the database instance.
`uri_direct_2`|An alternative URI that can be used to connect to the service. Formatted as for `uri`.
`uri_direct_1`|An alternative URI that can be used to connect to the service. Formatted as for `uri`.
`ca_certificate_base64`|A self-signed certificate that is used to confirm an application is connecting to the appropriate server. The certificate is base64 encoded.
`deployment_id`|An internal identifier for the service as created within Compose.
`uri_cli_2`|An alternative `cqlsh` shell command line that connects to the database instance.
`uri`|The URI that is used when connecting to the service, which includes the schema (`scylla:`), password, host name of server, port number to connect to, and database name.
{: caption="Table 1. {{site.data.keyword.composeForScyllaDB}} credentials" caption-side="top"}
