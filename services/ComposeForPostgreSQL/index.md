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

# Getting started with Compose for PostgreSQL
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}} provides a powerful, open source object-relational database that is highly customizable. With Postgres, development is fast and easily scalable. You can develop in a language that you're comfortable with, such as C/C++, Perl, Python, TCL/TK, Delphi/Kylix, VB, PHP, ASP, and Java. You get a feature-rich enterprise database with JSON support, giving you the best of both the SQL and NoSQL worlds.
{:shortdesc}

**Note:** Any Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com/](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your Bluemix account.

Complete these steps to get started with Compose for PostgreSQL:

1. [Create a {{site.data.keyword.composeForPostgreSQL}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/).

  When you create an instance of the service, ensure that you choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned. The various credential values are listed in the *Available credentials* section.

2. Connect to your {{site.data.keyword.composeForPostgreSQL}} service.

  To connect an app to your service, use the credentials that are created along with the service. The sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForPostgreSQL}} service.

  Download the [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) sample app and follow the instructions in the readme file. Then, in your application details page in Bluemix, click **View APP** to view the contents of the _examples_ table.

## Available credentials

Field Name|Description
----------|-----------
`uri`|The URI to be used when connecting to the service. Includes the schema (`postgres:`), admin user name and password, host name of server, port number to connect to, database name and "?ssl=true" to enable SSL connections.
`uri_cli`|A `psql` shell command line that connects to the database instance.
`ca_certificate_base64`|A self-signed certificate that is used to confirm that an application is connecting to the appropriate server. This is base64 encoded. You need to decode the key before using it, as shown in the sample application.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by the service; in this case `postgresql`.
`name`|The database deployment name.
{: caption="Table 1. {{site.data.keyword.composeForPostgreSQL}} credentials" caption-side="top"}
