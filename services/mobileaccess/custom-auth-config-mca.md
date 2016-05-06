---

copyright:
  years: 2015, 2016
  
---

# Configuring {{site.data.keyword.amashort}} for custom authentication
{: #custom-dash}
To use custom authentication with your mobile app, you must register a custom authentication realm and the base URL of your custom identity provider in the {{site.data.keyword.amashort}} service dashboard.

## Before you begin
{: #custom-dash-begin}
* Read [Getting Started](getting-started.html).
* Protect your backend application with the {{site.data.keyword.amashort}} server SDK.  For more information see [Protecting resources](protecting-resources.html).
* Have a custom identity provider application running.

## Configure custom authentication in the {{site.data.keyword.Bluemix}} dashboard
{: #custom-dash-config}
Use the {{site.data.keyword.amashort}} dashboard to configure custom authentication.

1. Open your app in the {{site.data.keyword.Bluemix}} dashboard.

1. Click **Mobile Options** and take note of your **Route** (`applicationRoute`) and **App GUID** (`applicationGUID`). You need these values when you initialize the SDK.

1. Click the {{site.data.keyword.amashort}} tile. The {{site.data.keyword.amashort}} dashboard loads.

1. Click the **Custom** tile.

1. Enter the **Realm name** and **Base URL** of your custom identity provider and save your changes.

## Next steps
{: #next-steps}
* [Configuring custom authentication for Android](custom-auth-android.html)
* [Configuring custom authentication for iOS](custom-auth-ios.html)
* [Configuring custom authentication for Cordova](custom-auth-cordova.html)
