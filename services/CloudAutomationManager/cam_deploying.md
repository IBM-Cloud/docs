---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

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

# Deploying a template
<!-- for example, Uploading your data -->
{: #cam_deploying}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Create and deploy a template from scratch or deploy one of the pre-built templates.
{:shortdesc}

To deploy a template, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Click **Templates**.
2. Click **Bring your own template** if you want to create and deploy a template from scratch or click one of the pre-built templates.
3. If you selected a pre-built template, read the information about the template and click **Deploy an Instance**.
4. In the Deploy Instance pane, provide the required information as the instance name. If you are creating a template from scratch, specify the template format (JSON or HCL) and the type of the cloud provider where you want to deploy the template. 
5. Click **Next**. 
6. If you are deploying a template from scratch, enter the template code in the **Template Code Editor** or import the template code from a file or from a URL by clicking **Select source**. The template must be in HCL or JSON format depending on what you specified in the previous Deploy Instance pane.

 If you are deploying a pre-built template, you do not need to change the template code displayed in the **Template Code Editor**.
7. Click **Next**.
8. Enter the required deployment parameters as, for example, the connection to the cloud provider where you want to deploy the template.
 
 The cloud connection list only contains the connections defined for the type of cloud provider where you can deploy the template. For information about cloud connections, see [Managing connections](https://console.{DomainName}/docs/services/CloudAutomationManager/cam_managing_connections.html).

9. Click **Deploy**. The instance window is displayed.

 In the instance window, you can see the instance status, the instance information, and the related resource details. You can view or download the instance logs and you can also access the template from which the instance was deployed.

