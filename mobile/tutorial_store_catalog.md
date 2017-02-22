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
{:note:.deprecated}

**UI Starters are deprecated:** Existing projects that were created from a UI Starter can be used until 30 April 2017. For more information about migration steps and removal dates, see the [deprecation announcement blog post ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-mobile-dashboard-update/).
{:deprecated}

# Tutorial - Store Catalog UI Starter
{: #tutorial_store_catalog}

The {{site.data.keyword.Bluemix}} Store Catalog UI Starter provides a basic sales app structure that you can customize, and gives you integration points for each of the {{site.data.keyword.Bluemix_notm}} Mobile services.


## Requirements
{: #tutorial_requirements notoc}

* A [Bluemix ![External link icon](../icons/launch-glyph.svg "External link icon")](http://bluemix.net) Account


## Getting Started
{: #tutorial_gs notoc}

To get up and running quickly with the Store Catalog UI Starter, follow these steps:

1. Create a Mobile dashboard project in {{site.data.keyword.Bluemix_notm}}.

   1. From the **Getting Started** page in the Mobile dashboard, click **Create Project**.

      You can alternatively click **Create Project** on the **Projects** page.

   2. Select **UI Starters**, if it is not already selected.

   3. Select **Store Catalog** and click **Create Project**.

   4. Enter your project name and click **Create**.

2. Optional: Add the {{site.data.keyword.mobilepushshort}} capability.

   1. Click **Add** for **{{site.data.keyword.mobilepushshort}}** on the **Project Overview** page.

      You can alternatively click **Create** on the **{{site.data.keyword.mobilepushshort}}** page.

   2. Enter your service name and click **Create**.

   3. For iOS, [configure Apple Push Notification Service ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. For Android, [configure Google Cloud Messaging ![External link icon](../icons/launch-glyph.svg "External link icon")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.

3. Optional: Add other capabilities.

   1. Click **Add** for the capability on the **Project Overview** page.

   2. Enter your service name and click **Create**.

   3. Follow the instructions that are provided with the service to set it up.

4. Design your app.

   1. Select **UI Builder** in the navigation menu to customize the design of your app.
   
		**Tip:** To view a quick overview of the UI Builder, select **Show me how it works** in the navigation after selecting the UI Builder.

   2. Select the **Design** tab in the navigation.

      There is a workspace for the design of your app and a simulated view of the appearance of your app.

   3. Optionally add new screens by selecting **Create Screen**. Name a new screen to make it easier to refer to in your app. New screens are created at the same level as the main screen, regardless of what is selected in the tree. You can select from the following types of screens:
      * Menu
      * List
      * Map
      * Custom
      * Chart	   

   4. You can change the menu title of your app by selecting the *Menu* text box in the **Layout** section of your interface and replacing the content in the **Data to display** field. View your updates in the simulated device section.

      Update the design items by selecting each one and updating the information, as necessary. These items are displayed in a tree format. You can change the order or location of the menu items by dragging an item to a new location. All of the children of the item are also moved with the parent. The textual information in the tree items that displays in the **Data to Display** fields reference content in the data source spreadsheet. *Do not change these items in the **Design** view because they are overwritten by the content in the Data Sources that are identifid in the **Data** view.*

		An item that is identified in the tree as a *Form* is independent and can be modified inline. It does not reference information from a Data Source.

   5. Select **Data** in the navigation to view the data that is being used by the app. There is default information in the template; however, you can change the source of the data by selecting **Create New**. You can reference more than one data source, so provide a name for each one that you use. You can select from the following data source options:
      * Cloud
      * Local
      * Cloudant
      * Google Sheet
      * Excel Online
      * Google Drive

      You can also import, export, or modify the content that is in the table, if it is local, by using the buttons and selecting the content in the table.

	  Notice: If you import data that does not match the structure of the default data, turn on the *Replace schema* slider. An example of this is a .csv file that has fewer columns than the data that is provided with your starter.
	  
   6. Select **Navigation** to customize the navigation actions in your app. This is optional because the navigation actions for many of the screens are automatically created based on the relationships of the screens. You can change the target screen by first selecting the screen or field that you want to navigate *from* in the Menu items list. Then select the screen that you want it to navigate *to* in the Target screen field. 

   7. Select **User Access** in the navigation to modify the access requirements of your project. You can toggle user access on and off with the switch. When user access is on, you can set the inactive user timeout and the credentials of users who can access the app.

   8. Select **Settings** in the navigation menu to modify the overall information about and colors for your project. This screen is where you enter your Google API key, if it is required for the services that you added to your project. This screen is also where you add your unique bundle identifier that is registered with the Apple Store or the Google Play Store.

      If you want to add the IBM MobileFirst Foundation SDK to your project, toggle the switch on.

   9. If you toggled the switch to add IBM MobileFirst Platform Foundation to your project in the *Settings* screen, a **Foundation** selection displays in the navigation. Select **Foundation** and complete the required information that is specific to IBM MobileFirst Platform Foundation.

   10. Select **Publish** in the navigation menu to enter the final information that is required to create your mobile app. You can enter your Bundle identifier for iOS and the Application identifier for Android.

       If you are creating an iOS app, you must obtain your Bundle Identifier, your Distribution Certificate as a *.p12* file, and your Provisioning Profile as a *.mobileprovision* file from the Apple provisioning portal. The three should be created at the same time and with the same computer that you plan to use when you post your app to the Apple store. The Distribution Certificate and the Provisioning Profile must be based on the Bundle Identifier. 	

5. Download your project.

   1. Click **Code** and select your preferred platform or programming language.

   2. For Android, you can choose from the following options after the code is generated:

      * Download Code

      * Download APK

      * Download with QR Code

   3. For iOS, you can choose the following option after the code is generated:

      * Download Code

6. Run your app on your device or simulator.


## What to do next
{: #tutorial_next notoc}

[Try it out! ![External link icon](../icons/launch-glyph.svg "External link icon")](http://console.{DomainName}/mobile/create-project?starter=fb5e31a9-1186-4d46-939e-2f620f35b83b){: new_window}


### UI Starter tutorials
{: #tutorials_UI notoc}

* [Tutorial - Store Catalog](tutorial_store_catalog.html)


### Code Starter tutorials
{: #tutorials_Code notoc}

* [Tutorial - Basic](tutorial.html)
* [Tutorial - Cloudant Sync](tutorial_cloudant_sync.html)
* [Tutorial - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutorial - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutorial - Watson {{site.data.keyword.coversationshort}}](tutorial_conversation.html)
* [Tutorial - Watson Language](tutorial_watson_language.html)
* [Tutorial - Weather](tutorial_weather.html)

