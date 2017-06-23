---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-22"

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

# Terminating a service instance
<!-- for example, Uploading your data -->
{: #cam_delete_service_instance}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

You can terminate a service instance from the deployed service instances.
{:shortdesc}

**Note:** You can terminate only instances related to the services that you ordered.

To terminate a service instance, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. In the left-side navigation bar, click **Deployed Instances > Services**.
2. In the service instance list, click the actions menu on the right of the instance that you want to delete. The action list is displayed.
3. Click **Terminate**. 
4. In the Terminate Service confirmation window, click **Terminate**. 

    The template instance related to this service instance is destroyed. For information about deleting template instances, see [Deleting a template instance](/docs/services/CloudAutomationManager/cam_delete_instance_local.html).
    
    The status of the service instance is changed to `Terminated` and the service instance is deleted from the list in 24 hours.
