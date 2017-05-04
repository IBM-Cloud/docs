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

To connect an app to your service, use the credentials that are created along with the service. The [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForEtcd}} service using the credentials.

Field Name|Description
----------|-----------
`ca_certificate_base64`|A self-signed certificate that is used to confirm that an app is connecting to the appropriate server. The certificate is base64-encoded. You must decode the key before using it, as shown in the sample app.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by service; in this case `etcd`.
`name`|The database deployment name.
`uri`|The URI to be used when connecting to the service. `uri` includes the schema (`amqps:), admin user name and password, the host name of the server, the port number to connect to, and `vhost` name.
{: caption="Table 1. Compose for etcd credentials" caption-side="top"}
