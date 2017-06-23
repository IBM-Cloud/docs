---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-19"

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

# Deleting a template instance
<!-- for example, Uploading your data -->
{: #cam_delete_instance}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

You can delete a template instance and all its related resources when you do not need them any more.
{:shortdesc}

To delete a template instance, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. In the left-side navigation bar, click **Deployed Instances > Templates**.
2. In the instance list, click the menu in the **ACTIONS** column for the instance that you want to delete. The action list is displayed.
3. In the action list, click **Destroy Instance** to delete all the resources related to the instance from the cloud provider. This option does not delete the instance from the Cloud Automation Manager environment. 
4. Enter `destroy` to confirm and click **Destroy**. The instance status is changed to `Destroyed`.
5. In the action list, click **Delete Instance** to delete the instance from the Cloud Automation Manager environment. 
6. Enter `delete` to confirm and click **Delete**. The instance is deleted from the instance list.


