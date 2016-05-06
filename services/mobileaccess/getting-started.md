---

copyright:
  years: 2015, 2016

---

# Getting started
{: #getting-started}
To get started with {{site.data.keyword.amashort}}, you can either add the {{site.data.keyword.amashort}} service to an existing {{site.data.keyword.Bluemix}} application, or you can create a new app with the boilerplate.  

## Creating an instance of the {{site.data.keyword.amashort}} service
{: #service-instance}

You can create a new instance of a {{site.data.keyword.amashort}} service from the {{site.data.keyword.Bluemix}} catalog.  If you do not use the boilerplate to create a new mobile backend, you must configure the server SDK on your existing backend.


  * **New app**: The instructions in the following sections describe how to create a new app that creates a mobile backend and protects with the {{site.data.keyword.amashort}} server SDK. Click the **MobileFirst Services Starter** boilerplate to create a new application with the {{site.data.keyword.amashort}} service.
  * **Existing app**: Click the {{site.data.keyword.amashort}} icon and create a new service instance that is bound to an existing application. To configure the server SDK on your existing app, see [Protecting Cloud Resources](protecting-resources.html).


## Creating a mobile backend with the MobileFirst Services Starter boilerplate
{: #create-backend}
When you use the MobileFirst Services Starter, you get an instance of a Node.js runtime that runs on IBM {{site.data.keyword.Bluemix_notm}} to implement your custom backend logic. A set of core mobile services that provide security, data, push, and monitoring functions are bound to that Node.js app. After the {{site.data.keyword.Bluemix_notm}} Node.js app is created, you can set up your development environment and start to use the {{site.data.keyword.Bluemix_notm}} Mobile Services SDKs. You can use the SDKs to access the services that are bound to your cloud app with simple API calls.

1. From the {{site.data.keyword.Bluemix_notm}} catalog, go to the **Boilerplates** section and click **MobileFirst Services Starter**.
1. Add information about your mobile backend including the space, name, host, and service plan.
1. Click **CREATE**.



## Next steps
{: #next-steps}
Several endpoints of the Node.js application that you created with the boilerplate are protected with {{site.data.keyword.amashort}}. To learn more about the default mobile backend application, see  [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

You can set up your mobile app to use the {{site.data.keyword.amashort}} SDK.  After you set up the SDK you can start setting up authentication and monitoring in your app.  Follow the instructions for your mobile development platform:

* [Android](getting-started-android.html)
* [iOS (Swift SDK)](getting-started-ios.html)
* [iOS (Objective-C SDK)](getting-started-ios.html)
* [Cordova](getting-started-cordova.html)
