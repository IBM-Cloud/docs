---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# End-to-end tutorial of the Microservice Basic Starter
{: #tutorial}

The following end-to-end tutorial walks you through the steps to create a project from the Microservice Basic Starter. This includes installing prerequisite tools and the steps to run the project code.

You can create a project by using either the web-based [{{site.data.keyword.dev_console}}](#create-devex) or through the command-driven [{{site.data.keyword.dev_cli_notm}}](#create-cli).

## Installing developer tools
{: #dev_tools}

Ensure that you install the [prerequisite developer tools ![External link icon](../icons/launch-glyph.svg "External link icon")](get_code.html#prereq-dev-tools){: new_window}.


## Creating a project by using the {{site.data.keyword.dev_console}}
{: #create-devex}

1. Create a project in the {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}.

	1. From the [**Getting Started** ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/developer/getting-started/) page in the {{site.data.keyword.dev_console}}, click **Create Project**.

		You can alternatively click **Create Project** from the **Projects** page.

	2. Select **Microservice** and click **Next**.

	3. Select **Basic** and click **Next**.

	4. Enter your project name. For this tutorial, use `MicroserviceProject`.   

	5. Enter a unique hostname. For this tutorial, use `devhost` 
   
	6. Click **Create**.

2. Optional: Add the Data capability.

	1. Click **View** for **Data** on the **Project Overview** page.

      You can alternatively select **Create** or **Add Existing** on the **Capabilities > Data** page.

   2. Enter your service name and click **Create**.

3. Generate your project code:

	1. Click **Get the Code** on the **Project Overview** page to select your language.
   
		You can alternatively click on the **Code** page.
      
	2. Click **Generate Code**.
   
	3. When the project code is finished generating, click **Download Code** to download your project archive.

4. Begin working with your downloaded project:

	1. Expand the archived file.
	
	2. Navigate to the new project directory.
	
	3. Use the {{site.data.keyword.dev_cli_notm}} to proceed.

5. Optional: [Update your project](project_overview_page.html#update_language) to generate a new language.


## Creating a project by using the {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Ensure that you install the [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. In your Terminal prompt, navigate to a local directory of your choice and run the following command.
  
	```
	bx dev create
	```
	{: codeblock}

3. Provide the following values when prompted:

	* Select a pattern: 4 (for Microservices)
	* Select a starter: 1 (for Basic)
	* Select a platform: 3 (for Java)
	* Enter a name for your project: `MicroserviceProjectCLI`

4. If you want to add services to your project, type `y` at the question prompt and answer the remaining questions.

5. When your `MicroserviceProjectCLI` is successfully saved, navigate to the `MicroserviceProjectCLI` folder.

6. Now you may add your own code, build, or run the project.
 
 
## Running the project by using the {{site.data.keyword.dev_cli_notm}}
{: #running-dev-plugin}

1. To build the project in your current project directory, enter the following command:

	```
	bx dev build
	```     
	{: codeblock}

2. To build and run the project in your current project directory, enter the following command:

	```
	bx dev run
	```
	{: codeblock}	

3. You can access the application by using `curl` on your server:

	```
	curl http://localhost:8080	
	```
	{: codeblock}
