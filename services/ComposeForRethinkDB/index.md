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

# Getting started with Compose for RethinkDB
{: #getting-started-with-compose-for-rethinkdb}

{{site.data.keyword.composeForRethinkDB}} gives you a JSON document-based, distributed database with an integrated administration and exploration console. RethinkDB uses the ReQL query language, which is built around function chaining and is available in client libraries for Java, JavaScript, Python, and Ruby. With ReQL, it is possible to use RethinkDB server-side features such as distributed joins and subqueries across the cluster’s nodes. RethinkDB also supports secondary indexes for better read query performance. RethinkDB’s most powerful feature, changefeeds, allows many ReQL queries to be converted into real-time feeds.
{:shortdesc}

**Note:** Any Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com/](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your Bluemix account.

Complete these steps to get started with {{site.data.keyword.composeForRethinkDB}}.

1. [Create a {{site.data.keyword.composeForRethinkDB}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-rethinkdb/).

  When you create an instance of the service, ensure that you choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned. The various credential values are listed in the *Available credentials* section.

2. Connect to your {{site.data.keyword.composeForRethinkDB}} service.

   To connect an app to your service, use the credentials that are created along with the service. The sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForRethinkDB}} service.

   Download the [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) sample app and follow the instructions in the readme file. Then, in your application details page in Bluemix, click **View APP**.

## Available credentials

Field Name|Description
----------|-----------
`uri`|The URI to be used when connecting to the service. Includes the schema (rethinkdb:), admin user name and password, host name of server and port number to connect to.
`uri_admin`|A URI that should be visited in a browser to access the database's administration interface. Access requires the admin user name and password from the `uri` field.
`ca_certificate_base64`|A self-signed certificate that is used to confirm that an application is connecting to the appropriate server. This is base64 encoded. You need to decode the key before using it, as shown in the sample application.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by the service; in this case `rethink`.
`name`|The database deployment name.
{: caption="Table 1. {{site.data.keyword.composeForRethinkDB}} credentials" caption-side="top"}
