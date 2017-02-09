---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


#Exporting and sharing your Kibana dashboards
<!-- for example, Uploading your data -->
{: #exporting_sharing_kibana_dash}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Export your dashboard schema as a JSON file or share a URL to customized Kibana dashboards of your log data. 
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
With Kibana, you can collaborate with other stakeholders by exporting your dashboards as JSON files or sharing URLs of your dashboards.

Complete the following tasks to export a Kibana dashboard as a JSON file:

1. Click the **Save** icon ![Save icon](images/logging_save.jpg); then, click **Advanced** **>** **Export schema**.

    ![Export dashboard as a JSON file](images/logging_export_json.jpg)

2. Choose a meaningful name for your JSON file; then, click **Save**. Any user with this JSON file can open the file in their Kibana dashboard. 

Complete the following tasks to create and share a URL to a Kibana dashboard:

1. On the Kibana dashboard, click the **Folder** icon ![Folder icon](images/logging_folder.jpg) to display a menu that lists all recent dashboards. In addition to dashboards that you saved by name, the menu lists unnamed dashboards according to the following format: *ALCH_TENANT_ID_application_id*. 

    ![List of dashboards](images/logging_list_of_dashboards.jpg)

2. Click the **Share** icon ![Share icon](images/logging_create_url.jpg) for the dashboard that you wish to share. A shareable URL is created and displayed. 

    ![Shareable URL pane](images/logging_shareable_link_popup.jpg)

    Copy the URL to share your dashboard with other users. Click **Close** to return to your dashboard.
