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

To connect an app to your service, use the credentials that are created along with the service. The [compose-rethinkdb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rethinkdb-helloworld-nodejs) sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForRethinkDB}} service using the credentials.

Field Name|Description
----------|-----------
`uri`|The URI to be used when connecting to the service. Includes the schema (rethinkdb:), admin user name and password, host name of server and port number to connect to.
`uri_admin`|A URI that should be visited in a browser to access the database's administration interface. Access requires the admin user name and password from the `uri` field.
`ca_certificate_base64`|A self-signed certificate that is used to confirm that an application is connecting to the appropriate server. This is base64 encoded. You need to decode the key before using it, as shown in the sample application.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by the service; in this case `rethink`.
`name`|The database deployment name.
{: caption="Table 1. Compose for RethinkDB credentials" caption-side="top"}
