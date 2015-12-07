{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Developing apps
{: #developingapps}

*Last updated: 4 December 2015*

You can develop applications by using an integrated development environment (IDE) or a text editor, or you can use {{site.data.keyword.Bluemix}} DevOps Services.
{:shortdesc}

##Developing applications with {{site.data.keyword.Bluemix_notm}} DevOps Services
{: #dev_ops}

You can use IBM {{site.data.keyword.Bluemix_notm}} DevOps Services to develop, track, and plan an application in the cloud, and then deploy it to {{site.data.keyword.Bluemix_notm}}. You can go from source code to a running application in minutes.

DevOps Services provides two services: Track & Plan and Delivery Pipeline. The Track & Plan service is used for agile planning. The Delivery Pipeline service automates builds and deployments. You can find these services in the {{site.data.keyword.Bluemix_notm}} Catalog. To learn more about how to use them, see [Getting started with Track & Plan](../services/TrackPlan/index.html#gettingstartedtemplate) and [Getting started with Delivery Pipeline](../services/DeliveryPipeline/index.html#getstartwithCD).

DevOps Services also provides Git hosting for source control and a Web IDE where you can edit, manage, and deploy your code. In an app, you enable Git hosting by clicking the **ADD GIT** link, which is in the upper-right corner of the app's Overview page. Then, you can edit your app's code in the Web IDE by clicking **EDIT CODE**. From the Web IDE shell, you can run cf commands with content assist. For example, you can get a list of all of the Cloud Foundry commands by typing the following command:
```
help cfo
```
