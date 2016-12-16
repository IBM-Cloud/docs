---

copyright:
  years: 2016
lastupdated: "2016-12-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Using a Code Starter to create a project
{: #projects_code}

You can use a [Code Starter](starters.html#Code_Starter) in {{site.data.keyword.Bluemix}} Mobile dashboard to create a project in the {{site.data.keyword.Bluemix_notm}} environment. This procedure does not apply to projects that use the UI Starters. See [Creating a project with a UI Starter](projects_ui.html) for instructions for UI Starters. 
{:shortdesc}

Complete the following steps to create a project with a Code Starter:

1. Create a new Mobile dashboard project in {{site.data.keyword.Bluemix_notm}}.

 You start with the *Getting Started* tab after you select the Mobile catalog. There are descriptions of selected starters that you can use and different ways to create a project that depend on how much help you need. If you want to just get started, select **Create Project**.

 If you already have projects, you can also start with the *Projects* tab selected. From the {{site.data.keyword.Bluemix_notm}} Mobile dashboard **Projects** view, you can select a project to work with, use the *Actions* for a project to delete it or download the code for it, or create a new project.

	1. On the {{site.data.keyword.Bluemix_notm}} Console, select **Mobile** after you expand the menu with the three lines next to the {{site.data.keyword.Bluemix_notm}} logo. 
	
	2. Select **Create Project**. 

	  You can alternatively select the **Projects** tab to view the projects that are already in your mobile environment and create a new project by clicking **Create Project**.

	3. Click **Code Starters**.  

	4. Select the starter that best matches the type of app that you want to create, and select **Create Project**. There are **UI Starters** and **Code Starters**. See [Starters](starters.html) for more information about starters and how to use them. 
	
	5. Enter a name for your project and select **Create**.
	
2. Make your selections on the **Project Overview** screen.  The **Project Overview** screen displays information about your project and the optional services that you can add to your project, like {{site.data.keyword.mobilepushshort}} and Authentication.  

	1. Optional: Select **Add** to add one of the listed services to your project. Edit the **Service name** for your service and click **Create**. When you add services to your project, you link to the {{site.data.keyword.Bluemix_notm}} page for that service. Configure the service by providing the information that is required for for the service.
	
	2. Optional: Repeat step *a* for any additional capabilities that you want to add to your project.

3. Optional: Select **Data** to connect a Cloudant NoSQL database or Object Storage service.
	1. Click **Create** to configure a new Cloudant NoSQL DB or Object Storage service.
	
	Note: If you create an instance of the Object Storage service, you are guided outside of the project to create it and add the required credentials. Navigate back to the the project after creating it and select **Add Existing** to connect the service with the project.
	
	If you already have an existing instance that is not connected to another project that you want to connect to this one, select **Add Existing**. 
	
	2. Verify that the tile of the Cloudant NoSQL DB or the Object Storage service that you connected to is displayed on the Data tab of your project.

4.  Download your project and complete the setup.

    1. Click **Download Code** and select your preferred language.
   
    2. Extract the archive and view the `README.md` file in a Markdown viewer to complete the setup.

5.  Try out your app! 


