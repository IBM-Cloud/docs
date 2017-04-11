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

# Getting started with Compose for RabbitMQ
{: #getting-started-with-compose-for-rabbitmq}

RabbitMQ asynchronously handles the messages between your applications and databases, enabling the separation of the data and application layers. RabbitMQ enables developers to route, track, and queue messages with customizable persistence levels, delivery settings, and confirmed publication. By using {{site.data.keyword.composeForRabbitMQ_full}}, you get access to the easy-to-use administrative interface with a host of management features such as deployment monitoring, click-of-a-button scaling, user setup, and log file access.
{:shortdesc}

**Note:** Any Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com/](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your Bluemix account.

Complete these steps to get started with {{site.data.keyword.composeForRabbitMQ}}.

1. [Create a {{site.data.keyword.composeForRabbitMQ}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-rabbitmq/).

  When you create an instance of the service, ensure that you choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned.  The various credential values are listed in the *Available credentials* section.

2. Connect to your {{site.data.keyword.composeForRabbitMQ}} service.

  To connect an app to your service, use the credentials that are created along with the service. The sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForRabbitMQ}} service.

  Download the [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) sample app and follow the instructions in the readme file. Then, in your application details page in Bluemix, click **View APP**.

## Available credentials

Field Name|Description
----------|-----------
`uri`|The URI to be used when connecting to the service. Includes the schema (`amqps:), admin user name and password, host name of server, port number to connect to and vhost name.
`uri_direct_1`|An alternate URI that can be used when connecting to the service. Formatted as per `uri`.
`uri_admin`|A URI that should be visited in a browser to access the database's administration interface. Access requires the admin user name and password from the `uri` field.
`uri_admin_1`|An alternative administration URI - see `uri_admin`.
`uri_admin_2`|An alternative administration URI - see `uri_admin`.
`uri_admin_3`|An alternative administration URI - see `uri_admin`.
`uri_admin_4`|An alternative administration URI - see `uri_admin`.
`ca_certificate_base64`|A self-signed certificate that is used to confirm that an application is connecting to the appropriate server. This is base64 encoded. You need to decode the key before using it, as shown in the sample application.
`deployment_id`|An internal identifier for the service as created within Compose.
`db_type`|The type of database that is offered by the service; in this case `rabbitmq`.
`name`|The database deployment name.
{: caption="Table 1. {{site.data.keyword.composeForRabbitMQ}} credentials" caption-side="top"}
