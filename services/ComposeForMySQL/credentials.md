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

To connect an app to your service, use the credentials that are created along with the service. The [compose-mysql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-mysql-helloworld-nodejs) sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForMySQL}} service using the credentials.

Field Name|Description
----------|-----------
`db_type`|The type of database that is offered by the service, in this case `mysql`.
`name`|The database deployment name.
`uri_cli`|A `mysql` shell command line that connects to the database instance.
`ca_certificate_base64`|A self-signed certificate that is used to confirm an application is connecting to the appropriate server. The certificate is base64 encoded.
`deployment_id`|An internal identifier for the service as created within Compose.
`uri`|The URI that is used when connecting to the service, which includes the schema (`mysql:`), admin user name and password, host name of the server, port number to connect to and vhost name.
{: caption="Table 1. Compose for MySQL credentials" caption-side="top"}
