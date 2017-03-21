---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Projects
{: #projects}

The {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} combines the app user interface, data, and services in a complete *project*. By creating a project, all of the required parts of your app and the added capabilities are maintained on the {{site.data.keyword.Bluemix_notm}} server. You can download your app code and the required credentials and initializers if the services are configured into your project. You can view all of your projects by selecting **Projects**.  

You can view additional information about a single project by selecting it on the **Projects** page. This displays the **Project Overview** page, which includes the services that are configured and available for the project. Services are separate capabilities that extend your app by adding a function. Because they are added individually, you can add the services that you need, like push services, authentication, data and storage, or other services. When you add a service to your project on the **Project Overview** page and follow the instructions to configure it, it is automatically associated with your app. For more information about the Project Overview page, see [Project Overview page](project_overview_page.html).

To create your project, you must select a [pattern](patterns.html), followed by a [starter](starters.html).


## Project Overview page
{: #project_overview}

You can view and work with a single {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} project by selecting the project on the **Projects** page, which opens the Project Overview page. 
{: shortdesc}

The **Project Overview** page displays a tile for each capability that is configured or available for configuring with the selected project. The tile displays the type of the capability and an *actions* button with three vertically-aligned dots. Examples of capabilities that might be available or configured include {{site.data.keyword.mobilepushshort}}, Analytics, or Data and Storage. The compatible capabilities are dependent on the type of project and the capabilities that are available in that region, so not all capabilities will be available to associate with all projects. 

When a type of capability is not yet associated with the project, a **Create** button is displayed on the tile. The actions button options are to create an instance of the service or to add an existing service instance when the capability is not already associated. Selecting **Add Existing** provides a list of the service instances of that type within your space.

If the capability is already associated with this project, the name of the associated service instance is displayed on the tile after the type of capability. This makes it easy to find which service instance is related to this project on your {{site.data.keyword.dev_console}}. The actions that are available on the actions button are **View** and **Remove** when the capability is already associated with the project. Removing a service instance only removes the association to this project and does not delete the service instance from your {{site.data.keyword.dev_console}}. To delete a service instance, click the **Web and Mobile > Services** page to view and delete your service instances.

Select **Get the Code** on the **Code** tile to download the code for your project. For more information about downloading the code, see [Get code](get_code.html).


## Updating your project to use a new Starter
{: #update-starter}

1. From the **Projects** or the **Project Overview** page, click the **Overflow Menu** icon and select **Update Starter**.

2. Choose a new Starter and click **Update**.

3. Click **Get the Code** on the **Project Overview** page to select your language.

   You can alternatively click on the **Code** page.


## Updating your project to generate a new language
{: #update-language}

1. From the **Projects** or the **Project Overview** pages, click the **Overflow Menu** icon and select **Update Starter**.

2. Select a new language and click **Update**.

3. Click **Get the Code** on the **Project Overview** page to select your language.
