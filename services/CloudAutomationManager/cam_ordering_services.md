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

# Ordering a service (Local)
<!-- for example, Uploading your data -->
{: #cam_ordering_service}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

You can search and order offerings from the Cloud Automation Manager catalog. You can customize the ordered offerings based on your requirement and use it in the overall application development. 
{:shortdesc}

To order a service, follow these steps:
1. In the left-side navigation bar, click **Catalog**. 
2. Click the service to preview its details. 
4. Verify the service details and features to understand if the service offering meets your requirement.
5. Click **Select to Order**. The  **Basic Parameters** tab is displayed. The parameters that are available in the **Basic Parameters** tab and **Additional Parameters** tab depend on the parameters selected by the service owner while creating the service. 
6. In the **Basic Parameters** tab, enter the required parameters as, for example, a name and the environment where to deploy the service.
7. Click **Next**.
8. In the **Additional Parameters** tab, enter the required parameters as, for example, the access key name and value.  
9. Click **Order**. A confirmation window is displayed.
10. Click **Go to Instances** to go in the Deployes Instances window and view the status of your order. If the order completes successfully,  the deployed instance status changes from `In Progress` to `Active`. From the actions menu of the deployed instance, you can view details of the service instance or terminate it. 
