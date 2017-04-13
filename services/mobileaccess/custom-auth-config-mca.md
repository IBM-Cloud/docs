---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-07"

---

**Important: The {{site.data.keyword.amafull}} service is replaced with the {{site.data.keyword.appid_full}} service.**

# Configuring Mobile Client Access for custom authentication
{: #custom-dash}


To use custom authentication with your mobile app, you must register a custom authentication realm and the base URL of your custom identity provider in the {{site.data.keyword.amashort}} service dashboard.

## Before you begin
{: #custom-dash-begin}
You  must have:
* An instance of an {{site.data.keyword.amafull}} service.
* A custom identity provider application.

## Configure custom authentication in the dashboard
{: #custom-dash-config}

Use the {{site.data.keyword.amafull}} dashboard to configure custom authentication.

1. Open your service in the {{site.data.keyword.amafull}} dashboard.
1. From the **Manage** tab, toggle **Authorization** on.
1. Expand the **Custom** section.
1. Enter the **Realm name**, **Custom Identity Provider URL**. The **Your Web Application Redirect URIs** value is required only for Web applications.

## Next steps
{: #next-steps}
* [Configuring custom authentication for Android](custom-auth-android.html)
* [Configuring custom authentication for iOS](custom-auth-ios-swift-sdk.html)
* [Configuring custom authentication for Cordova](custom-auth-cordova.html)
