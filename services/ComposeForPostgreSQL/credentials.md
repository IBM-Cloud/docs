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

To connect an app to your service, use the credentials that are created along with the service. The [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForPostgreSQL}} service using the credentials.

Field Name|Description
----------|-----------
`uri`|The URI to be used when connecting to the service. Includes the schema (`postgres:`), admin user name and password, host name of server, port number to connect to, database name and "?ssl=true" to enable SSL connections.
`uri_cli`|A `psql` shell command line that connects to the database instance.
`ca_certificate_base64`|A self-signed certificate that is used to confirm that an application is connecting to the appropriate server. This is base64 encoded. You need to decode the key before using it, as shown in the sample application.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by the service; in this case `postgresql`.
`name`|The database deployment name.
{: caption="Table 1. Compose for PostgreSQL credentials" caption-side="top"}
