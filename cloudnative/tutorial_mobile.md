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

# End-to-end tutorial of the Mobile Basic Starter
{: #tutorial}

The following end-to-end tutorial walks you through the steps to create a project from the Mobile Basic Starter. This includes installing prerequisite tools and the steps to run the project in Xcode and Android Studio.

You can create a project using either the web-based [{{site.data.keyword.dev_console}}](#create-devex) or through the command-driven [{{site.data.keyword.dev_cli_notm}}](#create-cli).

## Installing developer tools
{: #dev_tools}

Ensure that you install the [prerequisite developer tools ![External link icon](../icons/launch-glyph.svg "External link icon")](get_code.html#prereq-dev-tools){: new_window}.


## Creating a project by using the {{site.data.keyword.dev_console}}
{: #create-devex}

1. Create a {{site.data.keyword.dev_console}} project in {{site.data.keyword.Bluemix}}.

   1. From the [**Getting Started** ![External link icon](../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/developer/getting-started/) page in the {{site.data.keyword.dev_console}}, click **Create Project**.

      You can alternatively click **Create Project** from the **Projects** page.

   2. Select **Mobile App** and click **Next**.

   3. Select **Basic** and click **Next**.

   4. Enter your project name. For this tutorial, use `MobileBasicProject`.

   5. Select your platform. For this tutorial, use `Swift`.
   
   6. Click **Create**.

2. Optional: Add the Authentication capability.

   1. Click **Add** for **Authentication** on the **Project Overview** page.

      You can alternatively select **Create** or **Add Existing** on the **Capabilities > Authentication** page.

   2. Enter your service name and click **Create**.
   
   3. Toggle on **Authentication**.
   
   4. Select your identity provider and enter the information to configure it. You can enable only one identity provider.
   
   5. See [Configuring identity providers} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/appid/identity-providers.html){: new_window} for more information about configuring Authentication.

3. Optional: Add the Analytics capability.

   1. Click **Add** for **Analytics** in the **Project Overview** page.

      You can alternatively click **Create** or **Add Existing** from the **Capabilities > Analytics** page.

   2. Enter your service name and click **Create**.
   
   3. Toggle off **Demo Mode** to see your analytics data after you run your app.
   
   4. See [Getting started with {{site.data.keyword.mobileanalytics_short}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobileanalytics/index.html){: new_window} for more information about configuring Analytics.

4. Optional: Add the {{site.data.keyword.mobilepushshort}} capability.

   1. Click **Add** for **{{site.data.keyword.mobilepushshort}}** in the **Project Overview** page.

      You can alternatively click **Create** or **Add Existing** from the **Capabilities > {{site.data.keyword.mobilepushshort}}** page.

   2. Enter your service name and click **Create**.

   3. For iOS, [configure Apple Push Notification Service ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. For Android, [configure Firebase Cloud Messaging ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.

5. Optional: Add the Data capability.

   1. Click **View** for **Data** on the **Project Overview** page.

      You can alternatively select **Create** on the **Data** page.
      
   2. Choose **{{site.data.keyword.cloudant_short_notm}}** or **{{site.data.keyword.objectstorageshort}}**.

   3. Enter your service name and click **Create**.

   4. See [Getting started with {{site.data.keyword.cloudant_short_notm}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/Cloudant/index.html){: new_window} for more information about configuring {{site.data.keyword.cloudant_short_notm}}.

   5. See [Getting started with {{site.data.keyword.objectstorageshort}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/ObjectStorage/index.html){: new_window} for more information about configuring {{site.data.keyword.objectstorageshort}}.

6. Generate your project code:

   1. Click **Get the Code** on the **Project Overview** page to select your language.
   
      You can alternatively click on the **Code** page.
      
   2. Click **Generate Swift**.
   
   3. When the project code is finished generating, click **Download Swift** to download your project archive.

7. Begin working with your downloaded project:

	1. Expand the archived file.
	
	2. Navigate to the new project directory.
	
	3. Use the {{site.data.keyword.dev_cli_notm}} to proceed.

8. Optional: [Update your project](project_overview_page.html#update_language) to generate a new language.


## Creating a project by using the {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Ensure that you install the [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. In your Terminal prompt, navigate to a local directory of your choice and run the following command.

	```
	bx dev create
	```
	{: codeblock}
	
3. Provide the following values when prompted:

	* Select a pattern: 2 (for Mobile)
	* Select a starter: 1 (for Basic)
	* Select a platform: 3 (for iOS Swift)
	* Enter a name for your project: `MobileBasicProjectCLI`

4. If you want to add services to your project, type `y` at the question prompt and answer the remaining questions.

5. When your `MobileBasicProjectCLI` is successfully saved, navigate to the `MobileBasicProjectCLI/MobileBasicProjectCLI-Swift` folder.


## Running your Swift project in Xcode
{: #run_swift}

1. Extract the `MobileBasicProject-Swift.zip` file.

2. Open the `README.md` file in a Markdown viewer to review the steps to configure your project.

   1. Open your Terminal and navigate to your project folder.
   
      1. Run `pod setup` if you need to set up your CocoaPods repository.
      
      2. Run `pod update` if you need to update you update your existing pods.
      
      3. Run `pod install` to install the pods that are required for your project.
      
   3. Open your `BasicProject.xcworkspace` Xcode workspace.
      
3. Run your app.


## Running your Cordova project in Xcode
{: #run_cordova_xcode}

1. Extract the `MobileBasicProject-Cordova.zip` file.

2. Open the `README.md` file in a Markdown viewer to configure your project.

   1. Open your `platforms/ios` project in Xcode.
      
3. Run your app.


## Running your Cordova project in Android Studio
{: #run_cordova_studio}

1. Extract the `BasicProject-Cordova.zip` file.

2. Open the `README.md` file in a Markdown viewer to configure your project.

   1. Open your `platforms/android` project in Android Studio.
      
3. Run your app.


## Running your Android project in Android Studio
{: #run_android}

1. Extract the `MobileBasicProject-Android.zip` file.

2. Open the `README.md` file in a Markdown viewer to configure your project.

   1. Open your `BasicProject-Android` project in Android Studio.
      
3. Run your app.