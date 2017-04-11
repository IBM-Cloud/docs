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

# Getting started with Compose for MySQL
{: #getting-started-with-compose-for-mysql}

With a broad subset of ANSI SQL 99 and a wide set of its own extensions, including JSON document, full text search and updatable views, MySQL offers a rich palette for developers to draw on in their applications. Administrators can also find a wide selection of database management tools that can work with MySQL. {{site.data.keyword.composeForMySQL_full}} makes MySQL extends the capabilities of MySQL by managing it for you, offering an easy, auto-scaling deployment system that delivers high availability and redundancy, and automated backups.
{:shortdesc}

**Note:** {{site.data.keyword.composeForMySQL_full}} does not give access to the Compose UI. See [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) for more details.

Complete these steps to get started with {{site.data.keyword.composeForMySQL}}:

1. [Create a {{site.data.keyword.composeForMySQL}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-mysql/).

   When you create an instance of the service, choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned.  The various credential values are listed in the "Available credentials" section.

2. Connect to your {{site.data.keyword.composeForMySQL}} service.

  To connect an application to your service, use the credentials that are created along with the service.

  Download the [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) sample application and follow the instructions in the readme file. Then, on the application details page in the Bluemix console, click **View APP**.

  The sample application demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForMySQL}} service.


## Available credentials

Field Name|Description
----------|-----------
`db_type`|The type of database that is offered by the service, in this case `mysql`.
`name`|The database deployment name.
`uri_cli`|A `mysql` shell command line that connects to the database instance.
`ca_certificate_base64`|A self-signed certificate that is used to confirm an application is connecting to the appropriate server. The certificate is base64 encoded.
`deployment_id`|An internal identifier for the service as created within Compose.
`uri`|The URI that is used when connecting to the service, which includes the schema (`mysql:`), admin user name and password, host name of the server, port number to connect to and vhost name.
{: caption="Table 1. {{site.data.keyword.composeForMySQL}} credentials" caption-side="top"}
