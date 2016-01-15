# Configuring {{site.data.keyword.amashort}} for custom authentication
{: #custom-dash}
To use custom authentication with your mobile app, you must register a custom authentication realm and the base URL of your custom identity provider in the {{site.data.keyword.amashort}} service dashboard.

## Before you begin
{: #custom-dash-begin}
* Read [Getting Started](getting-started.html).
* Protect your backend application with the {{site.data.keyword.amashort}} Server SDK.  For more information see [Protecting resources](protecting-resources.html).
* Have a custom identity provider application running.

## Configure custom authentication in the {{site.data.keyword.Bluemix}} dashboard
{: #custom-dash-config}
Use the {{site.data.keyword.amashort}} dashboard to configure custom authentication.

1. Go to the {{site.data.keyword.amashort}} dashboard. In the {{site.data.keyword.Bluemix_notm}} dashboard, click your application. Click the	{{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}} dashboard loads.

1. Click **Set up authentication > Custom**.

1. Enter the **Realm name** and **Base URL** of your custom identity provider and save your changes.

## Next steps
{: #next-steps}
* [Configuring custom authentication for Android](custom-auth-android.html)
* [Configuring custom authentication for iOS](custom-auth-ios.html)
* [Configuring custom authentication for Cordova](custom-auth-cordova.html)
