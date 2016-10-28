---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# What's new in the Mobile dashboard
{: #what_is_new}

Last updated: 21 October 2016
{: .last-updated}

The October update of the {{site.data.keyword.Bluemix}} Mobile dashboard introduced the following changes:

   * You can now add Push Notifications and Analytics capabilities to your project directly from the dashboard.
   * [Code Starters](starters.html#Code_Starter) are now available.
   * You can add Authentication to your projects that you created from a Code Starter.
   * Swift is now supported.


### Analytics
{: #analytics}

   * Demo mode is enabled by default when you add the Analytics capability. You can toggle off demo mode to view your analytics after you run your app.


### UI Builder
{: #ui_builder}

   * The **Push Notifications** capability is now accessed from the project.
   * The **Project Settings** tab has been renamed to the **Settings** tab.
   * The **Authentication** tab has been renamed to **User Access** tab.


### Code
{: #code}

   * The generated Objective-C and Swift code for iOS now uses CocoaPods to manage dependencies. This means that you need to install CocoaPods. To install it, run `sudo gem install cocoapods`. After CocoaPods is installed, run `pod setup` to configure it (if not configured already). Finally, run `pod install` to download and install the required project dependencies prior to opening your `.xcworkspace` file in Xcode. Additional details are available in the `README.md` file in the downloaded code archive. Read about [Prerequisite Developer Tools](get_code.html#prereq-dev-tools) for more information.

Check back often to stay current with new updates.


# Related Links
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Blog Posts
{: #general}
* [Blog Post: Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Blog Post: Introducing the next generation of the Bluemix Mobile dashboard](https://www.ibm.com/blogs/bluemix/2016/10/next-gen-bluemix-mobile-dashboard/){: new_window}
* [Blog Post: Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [Blog Post: Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Blog Post: Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## Tutorials and Samples
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
