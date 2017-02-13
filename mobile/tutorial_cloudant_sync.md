---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-31"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# End-to-end tutorial of the Cloudant Sync Code Starter
{: #tutorial_cloudant_sync}

The following end-to-end tutorial walks through the steps to create a project from the Cloudant Sync Code Starter, including the tools that you must have installed, and subsequently, the steps to run the starter in Android Studio.


## Installing developer tools
{: #dev_tools notoc}

Ensure that you have installed the [prerequisite developer tools ![External link icon](../icons/launch-glyph.svg "External link icon")](get_code.html#prereq-dev-tools){: new_window}.


## Creating a project from the Cloudant Sync Code Starter
{: #create_project notoc}

1. Create a Mobile dashboard project in {{site.data.keyword.Bluemix}}.

   1. From the **Getting Started** page in the Mobile dashboard, click **Create Project**.

      You can alternatively click **Create Project** from the **Projects** page.

   2. Click **Code Starters**.

   3. Select **Cloudant Sync** and click **Create Project**.

   4. Enter your project name. For this tutorial, use `CloudantSyncProject`.
   
   5. Click **Create**.

2. Add the Data capability. You can create a new {{site.data.keyword.cloudant}} service instance or add an existing service instance.

   1. Click **View** on the **Data** tile on the **Project Overview** page.

      You can alternatively click **Create** or **Add Existing**, and then **Cloudant NoSQL DB** on the **Data** page.
      
   2. Optional: If you chose to create a new service instance, enter your service name and click **Create**.

   3. Optional: If you chose to add an existing service instance, select your service instance from the list and click **Add Existing**.

   4. Click the **Menu** icon in your service tile and select **Launch...** to launch your service instance.

      1. Click **LAUNCH** to launch your {{site.data.keyword.cloudant}} console.

      2. Click **Create Database**, enter your database name, and click **Create**.

      3. Click the **+** icon next to **All Documents** to add documents.

3. Optional: Add the {{site.data.keyword.mobilepushshort}} capability.

   1. Click **Add** for **{{site.data.keyword.mobilepushshort}}** in the **Project Overview** page.

      You can alternatively click **Create** from the **{{site.data.keyword.mobilepushshort}}** page.

   2. Enter your service name and click **Create**.

   3. For Android, [configure Firebase Cloud Messaging ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
4. Optional: Add the Analytics capability.

   1. Click **Add** for **Analytics** in the **Project Overview** page.

      You can alternatively click **Create** from the **Analytics** page.

   2. Enter your service name and click **Create**.
   
   3. Toggle off **Demo Mode** to see your analytics data after you run your app.
   
   4. See [Getting started with {{site.data.keyword.mobileanalytics_short}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobileanalytics/index.html){: new_window} for more information about configuring Analytics.
  
5. Optional: Add the Authentication capability.

   1. Click **Add** for **Authentication** on the **Project Overview** page.

      You can alternatively select **Create** on the **Authentication** page.

   2. Enter your service name and click **Create**.
   
   3. Toggle on **Authentication**.
   
   4. Select your identity provider and enter the required information to configure it. You can enable only one identity provider.

   5. See [Getting started with {{site.data.keyword.amashort}} ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobileaccess/index.html){: new_window} for more information about configuring Authentication.

6. Generate your project code.

   1. Click **Get Code** on the **Project Overview** page to select your platform and language.
   
      You can alternatively click on the **Code** page.
      
   2. For Android, click **Android**.
   
   3. When the project code is finished generating, click **Download Code** to download your project archive.


## Running your Android project in Android Studio
{: #run_android notoc}

1. Extract the `CloudantSyncProject-Android.zip` file.

2. Open the `README.md` file in a Markdown viewer to configure your project.

   1. Open your `CloudantSyncProject-Android` project in Android Studio.

   2. Add your Cloudant credentials.

      1. From the **Data** page, click the **Menu** icon in your service tile and select **Launch...** to launch your service instance.

         1. Click **LAUNCH** to launch your {{site.data.keyword.cloudant}} console.

         2. Click your database name, and click **Permissions**.

         3. Enter your database name in the `cloudant_dbname` string in the `res/values/cloudant_credentials.xml` file.

         4. Click **Generate API Key**.

             1. Copy the **Key** value and paste the value into the `cloudant_api_key` string in the `res/values/cloudant_credentials.xml` file.

             2. Copy the **Password** value and paste the value into the `cloudant_api_password` string in the `res/values/cloudant_credentials.xml` file.

             3. Select the **_admin** permission.
      
3. Run your app.


## What to do next
{: #what_next notoc}

View other tutorials.


### Code Starter tutorials
{: #tutorials_Code notoc}

* [Tutorial - Basic](tutorial.html)
* [Tutorial - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutorial - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutorial - Watson {{site.data.keyword.conversationshort}}](tutorial_conversation.html)
* [Tutorial - Watson Language](tutorial_watson_language.html)
* [Tutorial - Weather](tutorial_weather.html)
