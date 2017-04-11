---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-24"

---
<!-- Copyright info and last updated date at top of file: REQUIRED
    The copyright and lastupdated info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    The value "lastupdated" must be followed by a machine date in quotes in the following format: "YYYY-MM-DD"
    The value for "years" must be indented 2 spaces under "copyright", followed by "lastupdated" which should start on its own non-indented line.

-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

<!-- Additional task topic: OPTIONAL
This is the template for additional task topics that are needed beyond the basic tasks in the getting started index.md.  As needed, other task topics can be included, with titles such as "Configuring x", "Administering y", "Managing z", etc. This topic is a peer of the getting started index.md in the <servicename>.ditamap. This topic can have one level of children and they also can be referenced in <servicename>.ditamap -->

# Managing connections
<!-- for example, Uploading your data -->
{: #cam_managing_connections}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

In the Connections view, manage your connections to define the parameters to connect to the cloud providers where you want to deploy your templates.
{:shortdesc}

<!--A connection to Bluemix is created by default. If you want to use Bluemix as cloud provider, edit the connection to specify the required parameters.-->

To add a new connection, follow these steps:

1. Click **Cloud Connections**.

2. Click **Create Connections**. 

3. Select the cloud provider to which you want you connect. The following cloud providers are supported:
 - IBM Cloud
 - Amazon EC2
 - vSphere (Beta)

4. Enter the connection name and description, and specify the required connection parameters depending on the cloud provider you selected.

 Cloud Automation Manager must have access to the provider cloud region where you want to deploy your templates.  The access is granted by supplying Cloud Automation Manager with access credentials. The method for obtaining access credentials depends on the cloud provider.

 For information about specifying IBM Cloud access credentials, see [Configuring an IBM Cloud connection](https://console.{DomainName}/docs/services/CloudAutomationManager/cam_creating_ibm_cloud_connection.html).
 
 For information about specifying Amazon EC2 access credentials, see [Configuring an Amazon EC2 connection](https://console.{DomainName}/docs/services/CloudAutomationManager/cam_creating_aws_connection.html).
 
 For information about specifying vSphere access credentials, see [Configuring a vSphere connection](https://console.{DomainName}/docs/services/CloudAutomationManager/cam_creating_vsphere_connection.html).

5. Click **Create**. The connection is added to the connection list.

To edit an existing connection, follow these steps:

1. Click **Cloud Connections**.

2. In the connection list, click the connection that you want to edit.

3. Modify the existing connection details and parameters.

4. Click **Update**.

To delete a connection, follow these steps:

1. Click **Cloud Connections**.

2. In the connection list, click the menu in the **ACTIONS** column for the connection that you want to delete.

3. In the action list, click **Delete Connection**. A confirmation window is opened.

4. Click **Delete** to confirm that you want to delete the connection.




