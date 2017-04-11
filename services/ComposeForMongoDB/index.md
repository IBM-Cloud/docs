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

# Getting started with Compose for MongoDB
{: #getting-started-with-compose-for-mongodb}

{{site.data.keyword.composeForMongoDB_full}} uses the powerful indexing and querying, aggregation, and wide driver support of MongoDB that has made it the go-to JSON data store for many startups and enterprises. {{site.data.keyword.composeForMongoDB}} offers an easy, auto-scaling deployment system. It delivers high availability and redundancy, automated and on-demand no-stop backups, monitoring tools, integration into alert systems, performance analysis views, and much more, all in a clean, simple user interface.
{:shortdesc}

**Note:** Any Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com/](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your Bluemix account.

Complete these steps to get started with {{site.data.keyword.composeForMongoDB}}:

1. [Create a {{site.data.keyword.composeForMongoDB}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-mongodb/).

   When you create an instance of the service, ensure that you choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned.  The various credential values are listed in the *Available credentials* section.

2. Connect to your {{site.data.keyword.composeForMongoDB}} service.

   To connect an app to your service, use the credentials that are created along with the service. The sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForMongoDB}} service.

   Download the [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) sample app and follow the instructions in the readme file. Then, in your application details page in Bluemix, click **View APP**.


## Available credentials

Field Name|Description
----------|-----------
`uri`|The URI to be used when connecting to the service. `uri` includes the schema (`mongodb:`), admin user name and password, host name of server, port number to connect to, database name, and `?ssl=true` to enable SSL connections.
`uri_cli`|A `mongo` shell command line that connects to the database instance.
`ca_certificate_base64`|A self-signed certificate that is used to confirm that an app is connecting to the appropriate server. The certificate is base64-encoded. You must decode the key before using it, as shown in the sample app.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by the service: in this case, `mongodb`.
`name`|The database deployment name.
{: caption="Table 1. {{site.data.keyword.composeForMongoDB}} credentials" caption-side="top"}
