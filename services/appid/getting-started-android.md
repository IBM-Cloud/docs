---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}

# Setting up the Android SDK
{: #android-sdk}

Build your Android apps with the {{site.data.keyword.appid_short}} client SDK, initialize the SDK, authenticate users, and make requests to protected and unprotected resources.
{:shortdesc}


## Before you begin
{: #before-you-begin}

You need the following information:
  * An instance of the {{site.data.keyword.appid_short_notm}} service.
  * Your tenant ID.
    * In the **Service Credentials** tab of your service dashboard, click **View Credentials**. Your tenant ID is displayed in the **tenant ID** field. This value is used for initializing your app.
  * Your {{site.data.keyword.Bluemix}} region. You can find your region by looking in the UI. The value is used for initializing your app.
    <table> <caption> Table 1. {{site.data.keyword.Bluemix_notm}} regions and corresponding SDK values </caption>
    <tr>
      <th> Bluemix Region </th>
      <th> SDK value </th>
    </tr>
    <tr>
      <td> US South </td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> Sydney </td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> United Kingdom </td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * An Android Studio project, set up to work with Gradle.
    * For more information about how to set up your Android development environment, see <a href="https://developers.google.com/web/tools/setup/" target="_blank">the Google Developer Tools docs <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.

## Installing the client SDK
{: #install-appid-sdk}

1. Create an Android Studio project, or open an existing project.
2.  Add the JitPack repository to your root `build.gradle` file.

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {:pre}

3. Open the `build.gradle` file for your application.

    **Note**: Be sure to open the file for your app, not the project `build.gradle` file.
4. Find the dependencies section of the file and add a compile dependency for the {{site.data.keyword.appid_short_notm}} client SDK:

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {:pre}

5. Find the defaultConfig section and add the following lines of code:

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {:pre}

6. Synchronize your project with Gradle. Click **Tools** > **Android** > **Sync Project with Gradle Files**.

## Initializing the Client SDK
{: #initialize-client-sdk}

Initialize the client SDK by passing the context, tenant ID, and region parameters to the initialize method. A common, though not mandatory, place to put the initialization code is in the onCreate method of the main activity in your Android application.

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {:pre}

1. Replace "tenantId" with the {{site.data.keyword.appid_short_notm}} service tenantId.
2. Replace the AppID.REGION_UK with your {{site.data.keyword.Bluemix_notm}} region.


## Authenticate users by using the login widget
{: #authenticate-login-widget}

The login widget default configuration requires the use of both Facebook and Google for authentication. If you configure only one of them, the login widget does not launch and the user is redirected to the configured IDP authentication screen.

After the {{site.data.keyword.appid_short_notm}} client SDK is initialized, you can authenticate your users by running the login widget.

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
        }

        @Override
        public void onAuthorizationCanceled () {
          //Authentication canceled by the user
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //User authenticated
        }
      });
  ```
  {:pre}


## Accessing user attributes
{: #accessing}

When you obtain an access token, it is possible to gain access to the user protected attributes endpoint. You can gain access by using the following API methods:

  ```   
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {:pre}

When an access token is not explicitly passed, {{site.data.keyword.appid_short_notm}} uses the last received token.

For example, you can invoke this code to set a new attribute, or override an existing one:

  ```
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//attributes received in JSON format on successful response
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Exception occurred
		}
	});
  ```
  {:pre}

### Anonymous login
{: #anonymous notoc}

With {{site.data.keyword.appid_short_notm}} you can log in anonymously, see [anonymous user](/docs/services/appid/user-profile.html#anonymous).

  ```
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
		}

		@Override
		public void onAuthorizationCanceled() {
			//Authentication canceled by the user
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//User authenticated
		}
	});
  ```
  {:pre}

### Progressive authentication
{: #progressive notoc}

When the user holds an anonymous access toke, they can become identified by passing it to the `loginWidget.launch` method.

  ```
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {:pre}

After an anonymous login, progressive authentication occurs even if the login widget is called without passing an access token because the service used the last received token. If you want to clear your stored tokens, run the following command:

  ```
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {:pre}


## Next steps
{: #next-steps}

{{site.data.keyword.appid_short_notm}} provides a default configuration when you initially set up your identity providers. You can use the default configuration in development mode only. Before you publish your application, update the default [Facebook](/docs/services/appid/identity-providers.html#facebook) and [Google](/docs/services/appid/identity-providers.html#google) configuration to your own credentials.
