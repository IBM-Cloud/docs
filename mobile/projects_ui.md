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

**UI Starters are deprecated:** Existing projects that were created from a UI Starter can be used until 30 April 2017. For more information about migration steps and removal dates, see the [deprecation announcement blog post ![External link icon](../icons/launch-glyph.svg "External link icon")]().
{:deprecated}

# Using a UI Starter to create a project
{: #projects_ui}

You can use a [UI Starter](starters.html#UI_Starter) in {{site.data.keyword.Bluemix}} Mobile dashboard to create a project in the {{site.data.keyword.Bluemix_notm}} environment. This procedure does not apply to projects that use the Code Starters. See [Creating a project with a Code Starter](projects_code.html) for instructions for Code Starters.
{:shortdesc}

Complete the following steps to create a project with a UI Starter:

1. Create a new Mobile dashboard project in {{site.data.keyword.Bluemix_notm}}.

 You start with the *Getting Started* tab after you select the Mobile catalog. There are descriptions of selected starters that you can use and different ways to create a project that depend on how much help you need. If you want to just get started with minimal help, select **Create Project**.

 If you already have projects, you can select the *Projects* tab while you are on the *Getting Started* tab. From the {{site.data.keyword.Bluemix_notm}} Mobile dashboard **Projects** view, you can select a project to work with, use the *Actions* for a project to delete it or download the code for it, or create a new project. If the project began from a UI Starter, you can also open the project in the UI Builder directly from the *Actions* menu. 

	1. On the {{site.data.keyword.Bluemix_notm}} Console, select **Mobile** after you expand the menu with the three lines next to the {{site.data.keyword.Bluemix_notm}} logo. 
	
	2. Select **Create Project**. 

	  You can alternatively select the **Projects** tab to view the projects that are already in your mobile environment and create a new project by clicking **Create Project**. 

	3. Select the starter that best matches the type of app that you want to create, and select **Create Project**. There are **UI Starters** and **Code Starters**. See [Starters](starters.html) for more information about starters and how to use them. 
	
	4. Enter a name for your project and select **Create**.
	
2. Make your selections on the **Project Overview** screen.  The **Project Overview** screen displays information about your project and the optional capabilities that you can add to your project, like {{site.data.keyword.mobilepushshort}}.  

	1. Optional: Select **Add** to add one of the listed capabilities to your project. Edit the **Service name** for your service and click **Create**. When you add services to your project, you link to the {{site.data.keyword.Bluemix_notm}} page for that service. Configure the service by providing the information that is required for the service.
	
	2. Optional: Repeat step *a* for any additional capabilities that you want to add to your project. 

3. Design your user interface using the UI Builder.

   **Note:** Because the Code Starters do not have a customizable user interface, the *Design* tab is not available.

    1. Select **UI Builder** in the navigation menu to customize the design of your app. 
	
		**Tip:** To view a quick overview of the UI Builder, select **Show me how it works** in the navigation after selecting the UI Builder. 
	
	2. Customize your app layout from the **Screens** tab.
	
	3. Add new screens by selecting **Create Screen**. Name a new screen to make it easier to refer to in your app. You can select from the following types of screens: 
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
	     
		**Note:** If you import data that does not match the structure of the default data, turn on the *Replace schema* slider. An example of this is a .csv file that has fewer columns than the data that is provided with your starter.
		 
	6. Select **Navigation** to customize the navigation actions in your app. This is optional because the navigation actions for many of the screens are automatically created based on the relationships of the screens. You can change the target screen by first selecting the screen or field that you want to navigate *from* in the Menu items list. Then select the screen that you want it to navigate *to* in the Target screen field. 
		 
	7. Select **User Access** in the navigation to modify the access requirements of your project. You can toggle user access on and off with the switch. When user access is on, you can set the inactive user timeout and the credentials of users who can access the app.
	
	8. Select **Settings** in the navigation menu to modify the overall information about and colors for your project. This screen is where you enter your Google API key, if it is required for the capabilities that you added to your project. This screen is also where you add your unique bundle identifier that is registered with the Apple Store or the Google Play Store.
	
		If you want to add the IBM MobileFirst Foundation SDK to your project, toggle the switch on.
		
	9. If you toggled the switch to add IBM MobileFirst Platform Foundation to your project in the *Settings* screen, a **Foundation** selection displays in the navigation. Select **Foundation** and complete the required information that is specific to IBM MobileFirst Platform Foundation.
	
	10. Select **Publish** in the navigation menu to enter the final information to create your mobile app. You can enter your Bundle identifier for iOS and the Application identifier for Android.
	
		If you are creating an iOS app, you must obtain your Bundle Identifier, your Distribution Certificate as a `.p12` file, and your Provisioning Profile as a `.mobileprovision` file from the Apple provisioning portal. The three should be created at the same time and with the same computer that you plan to use when you post your app to the Apple store. The Distribution Certificate and the Provisioning Profile must be based on the Bundle Identifier. 	
4. Go back to the *Project Overview* screen to retrieve the code for your app and try it out! You can download the code directly for the iOS or Android operating systems, or by scanning a QR code for the Android operating system. 


