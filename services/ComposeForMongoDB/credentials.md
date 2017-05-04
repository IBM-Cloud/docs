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

To connect an app to your service, use the credentials that are created along with the service. The [compose-mongodb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mongodb-helloworld-nodejs) sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForMongoDB}} service using the credentials.

Field Name|Description
----------|-----------
`uri`|The URI to be used when connecting to the service. `uri` includes the schema (`mongodb:`), admin user name and password, host name of server, port number to connect to, database name, and `?ssl=true` to enable SSL connections.
`uri_cli`|A `mongo` shell command line that connects to the database instance.
`ca_certificate_base64`|A self-signed certificate that is used to confirm that an app is connecting to the appropriate server. The certificate is base64-encoded. You must decode the key before using it, as shown in the sample app.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by the service: in this case, `mongodb`.
`name`|The database deployment name.
{: caption="Table 1. Compose for MongoDB credentials" caption-side="top"}
