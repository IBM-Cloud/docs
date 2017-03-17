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

# End-to-end tutorial of the Web Basic Starter
{: #tutorial}

The following end-to-end tutorial walks through the steps to create a project from the Web Basic Starter, including the tools that you must have installed, and subsequently, the steps to run the project code.

## Installing developer tools
{: #dev_tools}

Ensure that you have installed the [prerequisite developer tools ![External link icon](../icons/launch-glyph.svg "External link icon")](get_code.html#prereq-dev-tools){: new_window}.


## Creating a project using the {{site.data.keyword.dev_console}}
{: #create-devex}

1. Create a project in the {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}.

	1. From the **Getting Started** page in the {{site.data.keyword.dev_console}}, click **Create Project**.

		You can alternatively click **Create Project** from the **Projects** page.

	2. Select **Web App** and click **Next**.

	3. Select **Basic Web** and click **Next**.

	4. Enter your project name. For this tutorial, use `WebBasicProject`.   

	5. Enter a hostname. For this tutorial, use `devhost` 

	6. Select your language platform. For this tutorial, use `Swift`.
   
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

	* Select a pattern: 1 (for Web)
	* Select a starter: 1 (for Basic Web)
	* Select a language: 2 (for Swift)
	* Enter a name for your project: `WebBasicProjectCLI`
	* Enter a hostname for your project: `myhost`

4. If you want to add services to your project, type `y` at the question prompt and answer the remaining questions.

5. When your `WebBasicProjectCLI` project has been successfully saved, navigate to the `WebBasicProjectCLI` folder.

6. Add your own code, build the project, or run the project.
 
	1. Build the project with the following command:
   
		```
 		bx dev build
 		```     
		{: codeblock}

	2. Run the project with the following command:
 
		```
		bx dev run
		```
		{: codeblock}


## Running a web project
{: #run}

### Locally
{: #local notoc}

1. Install your node dependencies:

  ```
  npm install
  ```
  {: codeblock}

2. Bundle your frontend code into a module:

  ```
  node_modules/.bin/gulp
  ```
  {: codeblock}

3. Compile your server:

  ```
  swift build
  ```
  {: codeblock}

4. Run your application:

  ```
  .build/debug/WebBasicProjectCLI
  ```
  {: codeblock}

5. Open your browser to `http://localhost:8080`.


### Using the {{site.data.keyword.dev_cli_short}}
{: #dev notoc}

1. Install the node dependencies:

  ```
  npm install
  ```
  {: codeblock}

2. Bundle your frontend code into a module:

  ```
  gulp
  ```
  {: codeblock}

3. Run compilation:

  ```
  bx dev run
  ```
  {: codeblock}

4. Open your browser to `http://localhost:8080`.


## Running your project in Xcode
{: #Xcode}

1. Create an Xcode project.

	Before you can develop in Xcode, you need to use the Swift package manager to build an Xcode project.
	
	```
	swift project generate-xcodeproj
	```
	{: codeblock}

2. Change your active target to the executable:

	Next, open your project in Xcode and make sure your active target is the executable. You can hold down the option key while clicking on the drop down menu to select the desired active executable.

3. Press **run**.

4. Open your browser to `http://localhost:8080`.

