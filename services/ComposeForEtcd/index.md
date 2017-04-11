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

# Getting started with Compose for etcd
{: #getting-started-with-compose-for-etcd}

etcd is a key-value store that holds the always-correct data that you need to coordinate and manage your server cluster for distributed server configuration management. etcd uses the RAFT consensus algorithm to assure data consistency in your cluster. It  enforces the order in which operations take place on the data so that every node in the cluster arrives at the same result in the same way. {{site.data.keyword.composeForEtcd_full}} adds automatic backups of your configuration data that is stored in etcd. An intuitive administrative interface lets you monitor, scale, and administer your deployment with ease.
{:shortdesc}

**Note:** Any Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com/](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your Bluemix account.

Complete these steps to get started with {{site.data.keyword.composeForEtcd}}.

1. [Create a {{site.data.keyword.composeForEtcd}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-etcd/).

  When you create an instance of the service, ensure that you choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned. The various credential values are listed in the *Available credentials* section.

2. Connect to your {{site.data.keyword.composeForEtcd}} service.

To connect an app to your service, you use the credentials that are created along with the service. The sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForEtcd}} service.

Download the [compose-etcd-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-etcd-helloworld-nodejs) sample app and follow the instructions in the readme file. Then, in your application details page in Bluemix, click **View APP** to view the contents of _examples_.

## Available credentials

Field Name|Description
----------|-----------
`ca_certificate_base64`|A self-signed certificate that is used to confirm that an app is connecting to the appropriate server. The certificate is base64-encoded. You must decode the key before using it, as shown in the sample app.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by service; in this case `etcd`.
`name`|The database deployment name.
`uri`|The URI to be used when connecting to the service. `uri` includes the schema (`amqps:), admin user name and password, the host name of the server, the port number to connect to, and `vhost` name.
{: caption="Table 1. {{site.data.keyword.composeForEtcd}} credentials" caption-side="top"}
