---

copyright:
  years: 2016

---
{:shortdesc: .shortdesc}

# Customizing your app
{: #mobileappbuilder_screens}
*Last updated: 29 April 2016*

{: shortdesc}
Different screens let you customize your app, such as design, data, security, app settings, push, or publish.


## Design
{: #design}
The **Design** screen lets you control all aspects of the app design. The following actions are available:

* Add screens
* Add menu items
* Select layout
* Map elements on the screen with data sources
* View styles

Follow these steps to add a screen:

1. Click **+ Screen**.
2. Choose a screen type from the following choices:
	* Menu
	* List
	* Map
	* Custom
	* Chart
3. Enter your screen name.
4. Click **Add**.


## Data
{: #data}
The **Data** screen provides the following capabilities:

* Add new data sources
	* Create a cloud-based data source.
	* Create a local static data source that is installed on the device.
	* Use data on an IBM Cloudant database as a source.
	* Use spreadsheet data, such as Google Sheets or Excel Online.
	* Include data from your Google Drive.
* View existing data sources
* View screens that are linked to existing data sources.

Follow these steps to add a data source:

1. Click **+ Data Source**.
2. Choose a data source from the following choices:
	* Cloud
	* Local
	* Cloudant
	* Google Sheet
	* Excel Online
	* Google Drive
3. Enter your data source name.
4. Click **Add**.


## Security
{: #security}
You can add a login prompt to your app, and add login timeouts or add account credentials.

Follow these steps to enable security:

1. Click the toggle icon to **On**.
2. Choose when user sessions time out after being inactive from the following choices:
	* Never
	* 5 minutes
	* 1 hour
	* 8 hours
3. Click **Add User**.
4. Enter an email for the user name.
5. Add a password.


## App Settings
{: #app_settings}
The **App Settings** screen lets you customize your logo, app name, background image, app colors, app description, Google API Key, and bundle identifier. It also contains MobileFirst Platform Foundation settings to add MobileFirst Platform Foundation V7.1 SDKs and publish the app into a MobileFirst Server instance. Enabling this setting adds an **MFP Settings** screen to add your MobileFirst settings.

#### MFP Settings
{: #mfp_settings}
The **MFP Settings** screen lets you add your MobileFirst URL, runtime name, user, and password information.


## Push
{: #push}
You can include IBM Push Notifications into your app. If you have an IBM Push Notifications service instance, you must add the **App ID** and **App Route URL** values into the settings. The IBM Push Notification SDKs for iOS and Android are included when the app is built.

Follow these steps to enable push:

1. Click the toggle icon to **On**.
2. Enter your app ID.
3. Enter your app route URL.


## Publish
{: #publish}
The **Publish** settings are used for certificate information for app signing. For iOS, you must sign your app if you want the option to directly download and install the `ipa` file. For Android, `apk` files can still be downloaded and installed without being signed.


## Get My App
{: #get_my_app}
The **Get My App** screen lets you create your app. You can choose the iOS icon, the Android icon, or both.

