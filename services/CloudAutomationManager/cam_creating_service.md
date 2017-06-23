---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-21"

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

# Creating and publishing a service
<!-- for example, Uploading your data -->
{: #cam_creating_service}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Create and publish a service to allow users to display the services in the catalog and order them to deploy the related resources.
{:shortdesc}

To create and publish a service, follow these steps:

1. In the left-side navigation bar, click **Library > Services**. The service library is displayed.
2. Click **Create a Service**.
3. In the Create a Service window, specify a service name and, optionally, select a category. 

    If you do not specify any category, the `Uncategorized` category is created and the service is assigned to this category.
    
    For information about categories, see [Creating a category](/docs/services/CloudAutomationManager/cam_creating_category.html).
4. Click **Create**. The service details pane is displayed.
5. Specify the required information for the service. 

    The information that you enter are stored in the `service_metadata` section of the service source code. This information is overwritten if you import a service file in the **Edit Source Code** tab.
    
6. Click the **Edit Source Code** tab to insert the source code for the service.
7. Enter the service source code or click **Import Source File** to import a service file from the local machine. For more information about the service file syntax, see [Editing a service file](/docs/services/CloudAutomationManager/cam_editing_service_file.html).
8. Save your changes. The service is displayed in a `Draft` status in the service library.
9. Click the service that you created to open the related service details pane. Before publishing the service, you can test it to ensure it works correctly.
10. Click **Order**. The Order a Service pane is displayed.
11. Specify the required parameters and click **Next**.
12. Specify additional paramenters as defined in the service file.
13. Click **Order**. A confirmation messages is displayed.
14. Click **Go to Deployed Instances** to verify the status of the service deployment.

    If the service deployment ends in `Error` status, you can check the deployment logs by clicking the deployed service instance and then the **Log File** tab. When you find out the cause of the error, edit the service by accessing it from the service library, save the changes and test the service again.
 
    If the service deployment ends successfully in `Active` status, you can publish the service to make it available for all the users.

15. To publish the service, click **Library > Services** to access the service library.
16. Click the service to be published to open the related service details pane.
17. Click **Publish**. A message is displayed.
18. Click **Publish** to confirm that you want to publish the service.
19. When the service is successfully published, click **View Published Service** to access the service details pane. The service is now in `Published` status and it is shown in the service catalog.



