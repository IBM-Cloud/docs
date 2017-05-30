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

# Getting started with Compose for PostgreSQL
{: #getting-started-with-compose-for-postgreSQL}

{{site.data.keyword.composeForPostgreSQL}} provides a powerful, open source object-relational database that is highly customizable. With Postgres, development is fast and easily scalable. You can develop in a language that you're comfortable with, such as C/C++, Perl, Python, TCL/TK, Delphi/Kylix, VB, PHP, ASP, and Java. You get a feature-rich enterprise database with JSON support, giving you the best of both the SQL and NoSQL worlds.
{:shortdesc}

**Note:** Any Compose service instances that were provisioned before 14 September 2016 that are still active can still be used and directly accessed at [https://www.compose.com/](https://www.compose.com). Any Compose service instance that is provisioned from this point forward is directly accessed and used within your Bluemix account.

Complete these steps to get started with Compose for PostgreSQL:

1. [Create a {{site.data.keyword.composeForPostgreSQL}} instance](https://console.ng.bluemix.net/catalog/services/compose-for-postgresql/).

  When you create an instance of the service, ensure that you choose both a name for your service and a credential name. Leave the service unbound; you can connect an application to your service later by using the credentials that are provided when the service is provisioned. The various credential values are listed in the *Available credentials* section.

  When you provision your {{site.data.keyword.composeForPostgreSQL}} instance you can choose the *Standard* or *Enterprise* plans. With the *Enterprise* plan, you can provision your {{site.data.keyword.composeForPostgreSQL}} instance into an available {{site.data.keyword.composeEnterprise}} cluster. {{site.data.keyword.composeEnterprise}} provides the security and isolation required by enterprise compliance and uses dedicated networking to ensure the performance of the deployed databases. See the [Compose Enterprise documentation](../ComposeEnterprise/index.html) for more details.

2. Connect to your {{site.data.keyword.composeForPostgreSQL}} service.

  To connect an app to your service, use the [credentials](./credentials.html) that are created along with the service. The sample app demonstrates how to use Node.js to connect to a {{site.data.keyword.composeForPostgreSQL}} service.

  Download the [compose-postgresql-helloworld-nodejs](https://github.com/IBM-Bluemix/compose-postgresql-helloworld-nodejs) sample app and follow the instructions in the readme file. Then, in your application details page in Bluemix, click **View APP** to view the contents of the _examples_ table.
