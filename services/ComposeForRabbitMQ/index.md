---

copyright:
  years: 2016,2017
lastupdated: "2017-05-24"
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

  When you provision your {{site.data.keyword.composeForRabbitMQ}} instance you can choose the *Standard* or *Enterprise* plans. With the *Enterprise* plan, you can provision your {{site.data.keyword.composeForRabbitMQ}} instance into an available {{site.data.keyword.composeEnterprise}} cluster. {{site.data.keyword.composeEnterprise}} provides the security and isolation required by enterprise compliance and uses dedicated networking to ensure the performance of the deployed databases. See the [Compose Enterprise documentation](../ComposeEnterprise/index.html) for more details.

2. Connect to your {{site.data.keyword.composeForRabbitMQ}} service.

  To connect an app to your service, use the [credentials](./credentials.html) that are created along with the service. The sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForRabbitMQ}} service.

  Download the [compose-rabbitmq-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-rabbitmq-helloworld-nodejs) sample app and follow the instructions in the readme file. Then, in your application details page in Bluemix, click **View APP**.
