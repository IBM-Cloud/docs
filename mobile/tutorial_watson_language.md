---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Tutorial - Watson Language Code Starter
{: #tutorial_watson_language}

The {{site.data.keyword.Bluemix}} Mobile Code Starter for Watson Language showcases the Text To Speech and Language Translation services from Watson and gives you integration points for each of the {{site.data.keyword.Bluemix_notm}} Mobile services.


## Requirements
{: #tutorial_requirements}

* A [Bluemix](http://bluemix.net) Account
* [Language Translator](https://console.{DomainName}/catalog/services/language-translator/) and [Text to Speech](https://console.{DomainName}/catalog/services/text-to-speech/) service instances obtained from the [Bluemix Catalog](https://console.{DomainName}/catalog/)


## Getting Started
{: #tutorial_gs}

To get up and running quickly with the Watson Language Code Starter, follow these steps:

1. Create a Mobile dashboard project in {{site.data.keyword.Bluemix_notm}}.

   1. From the **Getting Started** page in the Mobile dashboard, click **Create Project**.

      You can alternatively click **Create Project** from the **Projects** page.

   2. Click **Code Starters**.

   3. Select **Watson Language** and click **Create Project**.

   4. Enter your project name and click **Create**.

2. Optional: Add the Push Notifications capability.

   1. Click **Add** for **Push Notifications** in the **Project Overview** page.

      You can alternatively click **Create** from the **Push Notifications** page.

   2. Enter your service name and click **Create**.

   3. For iOS, [configure Apple Push Notification Service](../services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. For Android, [configure Google Cloud Messaging](../services/mobilepush/t_push_provider_android.html){: new_window}.
   
3. Optional: Add the Analytics capability.

   1. Click **Add** for **Analytics** in the **Project Overview** page.

      You can alternatively click **Create** from the **Analytics** page.

   2. Enter your service name and click **Create**.
   
   3. Toggle off **Demo Mode** to see your analytics data after you run your app.

4. Optional: Add the Authentication capability.

   1. Click **Add** for **Authentication** on the **Project Overview** page.

      You can alternatively select **Create** on the **Authentication** page.

   2. Enter your service name and click **Create**.
   
   3. Toggle on **Authentication**.
   
   4. Select your identity provider and enter the required information to configure it. You can enable only one identity provider.

   5. See [Getting started with Mobile Client Access](../services/mobileaccess/index.html){: new_window} for more information about configuring authentication.

5. Download your project.

   1. Click **Code** and select your preferred language.

   2. Click **Download Code**.

6. Extract the archive and view the `README.md` file in a Markdown viewer to complete the setup.


## What to do next
{: #tutorial_next}

[Try it out!](http://console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375){: new_window}


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
* [developerWorks Recipe: Receive weather updates in your own language using IBM Bluemix Push Notification Service and Language Translator](https://developer.ibm.com/recipes/tutorials/receive-weather-updates-in-your-own-language-using-ibm-bluemix-push-notification-service-and-language-translator/){: new_window}

## Tutorials and Samples
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
