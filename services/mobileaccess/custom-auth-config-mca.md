---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-03"

---

# Configuring {{site.data.keyword.amashort}} for custom authentication
{: #custom-dash}


To use custom authentication with your mobile app, you must register a custom authentication realm and the base URL of your custom identity provider in the {{site.data.keyword.amashort}} service dashboard.

## Before you begin
{: #custom-dash-begin}
* An instance of an {{site.data.keyword.amafull}} service and {{site.data.keyword.Bluemix_notm}} application. For more information about how to create a {{site.data.keyword.Bluemix_notm}} back-end application, see [Getting started](index.html).
* The URL of your back-end application (**App Route**). You will need this values for sending requests to the protected endpoints of your back-end application.
* Your **TenantID** value. Open your service in the  {{site.data.keyword.amashort}} dashboard. Click the **Mobile Options** button. The `tenantId` (also known as `appGUID`)  value is displayed in the **App GUID / TenantId** field. You will need this value for intializing the Authorization Manager.
* Protect your back-end application with the {{site.data.keyword.amashort}} server SDK.  For more information see [Protecting resources](protecting-resources.html).
* Have a custom identity provider application running.

## Configure custom authentication in the {{site.data.keyword.Bluemix}} dashboard
{: #custom-dash-config}
Use the {{site.data.keyword.Bluemix}} dashboard to configure custom authentication.

1. Open your service in the {{site.data.keyword.amafull}} dashboard.
1. From the **Manage** tab, pull the **Authorization** lever to the **On** position.
1. Expand the **Custom** section.
1. Enter the **Realm name**, **Custom Identity Provider URL**. The **Your Web Application Redirect URIs** value is required only for Web applications.

## Next steps
{: #next-steps}
* [Configuring custom authentication for Android](custom-auth-android.html)
* [Configuring custom authentication for iOS](custom-auth-ios.html)
* [Configuring custom authentication for Cordova](custom-auth-cordova.html)
