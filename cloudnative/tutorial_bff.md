---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# End-to-end tutorial of the BFF Basic Starter
{: #tutorial}

The following end-to-end tutorial walks through the steps to create a project from the BFF Basic Starter, including the tools that you must have installed, and subsequently, the steps to run the project code.

## Installing developer tools
{: #dev_tools}

Ensure that you have installed the [prerequisite developer tools ![External link icon](../icons/launch-glyph.svg "External link icon")](get_code.html#prereq-dev-tools){: new_window}.


## Creating a project using the {{site.data.keyword.dev_console}}
{: #create-devex}

1. Create a project in the {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}.

	1. From the **Getting Started** page in the {{site.data.keyword.dev_console}}, click **Create Project**.

		You can alternatively click **Create Project** from the **Projects** page.

	2. Select **Backend for Frontend** and click **Next**.

	3. Select **Basic Backend** and click **Next**.

	4. Enter your project name. For this tutorial, use `BFFProject`.   

	5. Enter a hostname. For this tutorial, use `devhost` 

	6. Select your language platform. For this tutorial, use `Node`.
   
	7. Click **Create**.

2. Optional: Add the Data capability.

	1. Click **View** for **Data** on the **Project Overview** page.

      You can alternatively select **Create** or **Add Existing** on the **Capabilities > Data** page.

   2. Enter your service name and click **Create**.


3. Generate your project code.

	1. Click **Get the Code** on the **Project Overview** page to select your language.
   
		You can alternatively click on the **Code** page.
      
	2. Click **Generate Code**.
   
	3. When the project code is finished generating, click **Download Code** to download your project archive.

4. Optional: [Update your project](project_overview_page.html#update_language) to generate a new language.


## Creating a project using the {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Ensure that you have installed the [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. In your Terminal prompt, navigate to a local directory of your choice and run the following command.
  
	```
	bx dev create
	```
	{: codeblock}
	
3. Provide the following values when prompted:

	* Select a pattern: 3 (for Backend for Frontend)
	* Select a starter: 1 (for Basic Backend)
	* Select a language: 1 (for Node)
	* Enter a name for your project: `BFFProjectCLI`
	* Enter a hostname for your project: `myhost`

4. If you want to add services to your project, type `y` at the question prompt and answer the remaining questions.

5. When your `BFFProjectCLI` has been successfully saved, navigate to the `BFFProjectCLI` folder.

6. At this point you may add your own code, build or run the project.
 
	1. Build your project with the following command:
   
		```
		bx dev build
		```     
		{: codeblock}
  
	2. Run your project with the following command:

 		```
		bx dev run
		```
		{: codeblock}


## Running a BFF project
{: #running-bff}

### Locally
{: #bff-local}

1. Compile your server:

  ```
  swift build
  ```
  {: codeblock}

2. Run your application. For example, assuming your application is called `MyServer`:

  ```
  .build/debug/MyServer
  ```
  {: codeblock}

3. You can run curl on your server with `curl http://localhost:8080`


### Using the Bluemix Plugin
{: #using-blumix}

1. Run compilation

	```
	bx dev run
	```
	{: codeblock}

2. You can run curl on your server with 
  
	```
	curl http://localhost:8080
	```
	{: codeblock}
