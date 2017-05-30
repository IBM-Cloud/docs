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

# Getting started with Compose for ScyllaDB
{: #getting-started-with-compose-for-scylladb}

ScyllaDB is an in-place replacement for the Cassandra wide-column distributed database. ScyllaDB is written in C++, rather than Cassandra's Java, for better resource usage that can result in 10 times better performance in benchmarks. In addition to retaining compatibility with Cassandra tool and data files, ScyllaDB adds self-tuning capabilities. {{site.data.keyword.composeForScyllaDB_full}} extends the capabilities of ScyllaDB by managing it for you, offering an easy, auto-scaling deployment system that delivers high availability and redundancy, plus automated backups.
{:shortdesc}

**Note:** {{site.data.keyword.composeForScyllaDB_full}} does not give access to the Compose UI. See [Compose on Bluemix Support](https://help.compose.com/docs/bluemix-compose-support) for more details.

Complete these steps to get started with {{site.data.keyword.composeForScyllaDB}}:

1. [Create a {{site.data.keyword.composeForScyllaDB}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-scylladb/).

   When you create an instance of the service, choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned. The various credential values are listed in the "Available credentials" section.

   When you provision your {{site.data.keyword.composeForScyllaDB}} instance you can choose the *Standard* or *Enterprise* plans. With the *Enterprise* plan, you can provision your {{site.data.keyword.composeForScyllaDB}} instance into an available {{site.data.keyword.composeEnterprise}} cluster. {{site.data.keyword.composeEnterprise}} provides the security and isolation required by enterprise compliance and uses dedicated networking to ensure the performance of the deployed databases. See the [Compose Enterprise documentation](../ComposeEnterprise/index.html) for more details.

2. Connect to your {{site.data.keyword.composeForScyllaDB}} service.

   To connect an application to your service, use the [credentials](./credentials.html) that are created along with the service.

   Download the [compose-scylladb-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-scylladb-helloworld-nodejs) sample application and follow the instructions in the readme file. Then, on the application details page in the Bluemix console, click **View APP**.

   The sample application demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForScyllaDB}} service.
